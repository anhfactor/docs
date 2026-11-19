# Attach Multi External Interface vào Server

Tính năng attach multi external interface vào Server nhằm mục đích phân tách services/traffic, failover interface, tiết kiệm chi phí hơn khi không cần phải mua nhiều Server.

Tính năng này hiện đã hỗ trợ trên cả 2 region HCM và HAN.

Hướng dẫn triển khai use case phổ biến: Hosting 2 Website trên 2 Public Interface khác nhau (cần Server, hai hoặc nhiều External Interface available)

**Kiến trúc mục tiêu:**

VM Ubuntu/CentOS\
├── eth1 (IP: 103.245.255.167) → website1.com\
├── eth2 (IP: 103.245.255.166) → website2.com\
└── Nginx/Apache phân biệt traffic theo IP

**Bước 1: Attach multi external interface trên UI portal**

1. Truy cập portal vServer (ví dụ HCM): [https://hcm-3.console.greennode.ai/vserver/overview](https://hcm-3.console.greennode.ai/vserver/overview)
2. Vào detail của Server, chọn tab Network Interface và attach nhiều external interface.

**Bước 2: Cấu hình Network Interfaces**

Kiểm tra interfaces hiện tại:

`ip addr show`

Sửa file netplan (Ubuntu 22.04)

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

Lưu ý: Server có thể đã tồn tại file netplan, để đảm bảo apply file netplan mới không lỗi, cần thực hiện thêm các bước sau:

**a. Disable cloud-init network**

Tạo file:

`sudo nano /etc/cloud/cloud.cfg.d/99-disable-network-config.cfg`

Thêm:

`network: {config: disabled}`

**b. Disable file 50-cloud-init.yaml**

`mv /etc/netplan/50-cloud-init.yaml /etc/netplan/50-cloud-init.yaml.disabled`

Apply cấu hình và verify

```
# Apply cấu hình
sudo netplan apply

# Verify
ip addr show
ping -I eth1 8.8.8.8
```

**Sau khi apply, nếu đã login bằng SSH qua floating IP trước đó, cần re-login SSH bằng External interface (ví dụ eth1 hoặc eth2)**

**Bước 3: Cấu hình Policy-Based Routing**

```
# Tạo routing table mới
echo "200 rt_eth1" | sudo tee -a /etc/iproute2/rt_tables

# Add routes
sudo ip route add default via 103.245.255.1 dev eth1 table rt_eth1
sudo ip rule add from 103.245.255.167/32 table rt_eth1

# Verify
ip rule show
ip route show table rt_eth1
```

**Bước 4: Cài đặt Web Server (ví dụ Nginx)**

```
# Install Nginx
sudo apt update && sudo apt install nginx -y  # Ubuntu
# sudo yum install nginx -y  # CentOS

# Tạo thư mục websites
sudo mkdir -p /var/www/website1
sudo mkdir -p /var/www/website2

# Tạo file test
echo "<h1>Website 1 - IP: 103.245.255.167</h1>" | sudo tee /var/www/website1/index.html
echo "<h1>Website 2 - IP: 103.245.255.166</h1>" | sudo tee /var/www/website2/index.html
```

Cấu hình Website 1:

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
    
    # PHP support (nếu cần)
    location ~ \\.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
    }
}
```

Cấu hình Website 2:

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

Enable sites:

```
sudo ln -s /etc/nginx/sites-available/website1 /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/website2 /etc/nginx/sites-enabled/

# Test cấu hình
sudo nginx -t

# Restart Nginx
sudo systemctl restart nginx
sudo systemctl enable nginx
```

Ngoài ra còn có thể cấu hình thêm SSL/HTTPS (Let's Encrypt) và cần mở thêm Security Group rule cho inbound và outbound: tcp/80 (HTTP), tcp/443 (HTTPS).

Kiểm tra:

```
# Test kết nối từ server
curl -H "Host: website1.com" http://103.245.255.167
curl -H "Host: website2.com" http://103.245.255.166

# Test từ máy khác
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
