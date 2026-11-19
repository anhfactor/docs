# Attach Multi External Interface

Attaching multiple external interfaces to a server helps you:

* Separate services/traffic by public IP
* Add interface-level failover options
* Reduce cost when you don't need multiple servers

This feature is currently supported in both HCM and HAN regions.

Common use case: host 2 websites on 2 different public interfaces (requires 1 server and 2+ available external interfaces).

**Kiến trúc mục tiêu:**

VM Ubuntu/CentOS\
├── eth1 (IP: 103.245.255.167) → website1.com\
├── eth2 (IP: 103.245.255.166) → website2.com\
└── Nginx/Apache phân biệt traffic theo IP

**Step 1: Attach multiple external interfaces in the portal UI**

1. Truy cập portal vServer (ví dụ HCM): [https://hcm-3.console.greennode.ai/vserver/overview](https://hcm-3.console.greennode.ai/vserver/overview)
2. Open the server details, go to the **Network Interface** tab, then attach additional external interfaces.

**Step 2: Configure network interfaces**

Check current interfaces:

`ip addr show`

Edit the netplan file (Ubuntu 22.04):

`sudo nano /etc/netplan/01-netcfg.yaml`

```
network:
  version: 2
  ethernets:
    eth1:
      addresses:
        - 103.245.255.167/24
      routes:
        - to: default
          via: 103.245.255.1
      nameservers:
        addresses: [8.8.8.8, 8.8.4.4]

    eth2:
      addresses:
        - 103.245.255.166/24
      routes:
        - to: 0.0.0.0/0
          via: 103.245.255.1
          table: 200
      routing-policy:
        - from: 103.245.255.166/32
          table: 200
```

Note: the server may already have a netplan config. To avoid errors when applying the new config, do the following:

**a. Disable cloud-init network**

Create this file:

`sudo nano /etc/cloud/cloud.cfg.d/99-disable-network-config.cfg`

Add:

`network: {config: disabled}`

**b. Disable 50-cloud-init.yaml**

`mv /etc/netplan/50-cloud-init.yaml /etc/netplan/50-cloud-init.yaml.disabled`

Apply and verify:

```
# Apply
sudo netplan apply

# Verify
ip addr show
ping -I eth1 8.8.8.8
```

**After applying, if you previously SSH’ed via a floating IP, re-login via an external interface IP (eth1 or eth2).**

**Step 3: Configure Policy-Based Routing (PBR)**

If you already configured `routing-policy` in netplan (Step 2), you can skip this step. Use this step if you prefer configuring PBR via `iproute2`.

```
# Create a routing table
echo "200 rt_eth2" | sudo tee -a /etc/iproute2/rt_tables

# Add routes/rules for eth2 (IP 103.245.255.166)
sudo ip route add default via 103.245.255.1 dev eth2 table rt_eth2
sudo ip rule add from 103.245.255.166/32 table rt_eth2

# Verify
ip rule show
ip route show table rt_eth2
```

**Step 4: Install a web server (example: Nginx)**

```
# Install Nginx
sudo apt update && sudo apt install nginx -y  # Ubuntu
# sudo yum install nginx -y  # CentOS

# Create website folders
sudo mkdir -p /var/www/website1
sudo mkdir -p /var/www/website2

# Create test pages
echo "<h1>Website 1 - IP: 103.245.255.167</h1>" | sudo tee /var/www/website1/index.html
echo "<h1>Website 2 - IP: 103.245.255.166</h1>" | sudo tee /var/www/website2/index.html
```

Configure Website 1:

```
sudo nano /etc/nginx/sites-available/website1
```

```
server {
    listen 103.245.255.167:80;
    server_name website1.com www.website1.com;
    
    root /var/www/website1;
    index index.html index.php;
    
    access_log /var/log/nginx/website1_access.log;
    error_log /var/log/nginx/website1_error.log;
    
    location / {
        try_files $uri $uri/ =404;
    }
    
    # PHP support (optional)
    location ~ \\.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
    }
}
```

Configure Website 2:

```
sudo nano /etc/nginx/sites-available/website2
```

```
server {
    listen 103.245.255.166:80;
    server_name website2.com www.website2.com;
    
    root /var/www/website2;
    index index.html index.php;
    
    access_log /var/log/nginx/website2_access.log;
    error_log /var/log/nginx/website2_error.log;
    
    location / {
        try_files $uri $uri/ =404;
    }
    
    location ~ \\.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
    }
}
```

Enable the sites:

```
sudo ln -s /etc/nginx/sites-available/website1 /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/website2 /etc/nginx/sites-enabled/

# Test config
sudo nginx -t

# Restart Nginx
sudo systemctl restart nginx
sudo systemctl enable nginx
```

You can also add SSL/HTTPS (Let’s Encrypt). Make sure your Security Group allows inbound/outbound: `tcp/80` (HTTP) and `tcp/443` (HTTPS).

Validation checks:

```
# Test from the server
curl -H "Host: website1.com" http://103.245.255.167
curl -H "Host: website2.com" http://103.245.255.166

# Test from another machine
curl http://103.245.255.167
curl http://103.245.255.166

# Check listening ports
sudo ss -tulpn | grep -E ':(80|443)'

# Verify routing
ip route get 8.8.8.8 from 103.245.255.167
ip route get 8.8.8.8 from 103.245.255.166

# Check logs
sudo tail -f /var/log/nginx/website1_access.log
sudo tail -f /var/log/nginx/website2_access.log
```
