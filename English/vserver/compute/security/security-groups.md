# Security Groups

A security group acts as a virtual firewall to control the inbound and outbound traffic of VM instances to improve security.

When you launch a VM instance, you can specify one or more security groups. If you don't specify a security group, it uses the default security group. You can add rules to each security group that allow traffic to or from its associated VM instances. You can modify the rules for a security group at any time. New and modified rules are automatically applied to all VM instances that are associated with the security group.

Security groups provide stateful packet filtering capabilities. When this virtual firewall decides whether to allow traffic to reach VM instance, it evaluates all of the rules from all of the security groups that are associated with the VM instance.

## Security group rules <a href="#securitygroups-securitygrouprules" id="securitygroups-securitygrouprules"></a>

The rules of a security group control the inbound traffic that's allowed to reach the VM instances that are associated with the security group. The rules also control the outbound traffic that's allowed to leave them.

The following are the characteristics of security group rules:

* By default, security groups contain outbound rules that allow all outbound traffic. You can delete these rules.
* Security group rules are always permissive, it means deny access always, you can't create denied rules.
* Security group rules enable you to filter traffic based on protocols, port numbers and the remote address.
* Security groups are stateful, if you send a request from your VM instance, the response traffic for that request is allowed to flow in regardless of inbound security group rules. This also means that responses to allowed inbound traffic are allowed to flow out, regardless of outbound rules.
* When you associate multiple security groups with a VM instance, the rules from each security group are effectively aggregated. Therefore, a VM instance can have hundreds of rules that apply. This might cause problems when you access the VM instance. We recommend that you condense your rules as much as possible.

For each rule, you specify the following:

* **Rule**: predefined of well-known rule such as SSH, HTTP, HTTPS, ICMP…
* **Protocol**: The protocol to allow. The most common protocols are 6 (TCP), 17 (UDP), and 1 (ICMP).
* **Port range**: For TCP, UDP, or a custom protocol, the range of ports to allow. You can specify a single port number (for example, **22**), or range of port numbers (for example, **7000 - 8000**).
* **CIDR of remote address**: The remote address means the source (inbound rules) or destination (outbound rules) for the traffic to allow. Specify one of the following:
  * A single IPv4 address. You must use the **/32** prefix length. For example, **203.113.1/32**.
  * A range of IPv4 addresses, in CIDR block notation. For example, **203.0.113.0/24**.
* **(Optional) Description**: You can add a description for the rule, which can help you identify it later.

## Default security group <a href="#securitygroups-defaultsecuritygroup" id="securitygroups-defaultsecuritygroup"></a>

Each VM instance must belong to one or more security groups. When you create VM instances using console portal or API, you can use the default security group. The default security group contains default rules:

Outbound rules:

* Allow all outbound traffic

Inbound rules:

* Allow access from all IP address to port 234 (SSH) and 3490 (RDP)
* Allow access from all IP address to port 80 (HTTP), 443 (HTTPS)
* Allow ICMP access from all IP address to all ports
* You can modify or delete any of these rules later.

## Work with security group <a href="#securitygroups-workwithsecuritygroup" id="securitygroups-workwithsecuritygroup"></a>

You can perform the following operations to use security groups to control traffic for VM instances:

#### Create security group <a href="#securitygroups-createsecuritygroup" id="securitygroups-createsecuritygroup"></a>

1. Go to GreenNode Portal console, navigate to Security Group
2. Create a Security Group with name and description as your need

#### View the security group <a href="#securitygroups-viewthesecuritygroup" id="securitygroups-viewthesecuritygroup"></a>

1. Go to GreenNode Portal console, navigate to Security Group
2. Select the Security Group and click View Detail, you can view the detail rules of inbound and outbound. Tab Server show VM instances that associated with this security group.

#### Add/delete rules to/from the security groups <a href="#securitygroups-add-deleterulesto-fromthesecuritygroups" id="securitygroups-add-deleterulesto-fromthesecuritygroups"></a>

1. Go to GreenNode Portal console, navigate to Security Group
2. Select the Security Group and click View Detail
3. Navigate to tab Inbound or Outbound to add or delete rules
4. To add new rule, you must provide either protocol, port range, CIDR as your needs

#### Assign/remove security groups to/from the VM instance <a href="#securitygroups-assign-removesecuritygroupsto-fromthevminstance" id="securitygroups-assign-removesecuritygroupsto-fromthevminstance"></a>

1. Go to GreenNode Portal console, navigate to VM Instance page
2. Select the VM Instance to change, click Update Security in expanded Menu on the right side
3. Assign or remove from existing Security Groups

<br>
