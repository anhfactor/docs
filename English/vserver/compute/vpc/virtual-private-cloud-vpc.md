# Virtual Private Cloud (VPC)

The development of cloud computing technologies leads to higher requirements for virtual networks, such as scalability, security, reliability, privacy, and robust connectivity performance. To resolve these problems, various network virtualization technologies emerged.

VPC is a virtual Private network environment that belongs to the defined enterprise and is independent of other businesses on GreenNode. A VPC network provides variety of network services such as DHCP, Route Table, Internet Gateway, Floating IP, External Interface, Load Balancing, VPN gateway... You have full control over your VPC. For example, you can specify the subnet and configure route tables and gateways.

Furthermore, you can connect your VPC to other VPCs or on-premises networks through VPC Peering or InterConnect service to create a custom network environment. This way, you can hybrid your applications to the cloud or extend data centers.

## VPC Basic <a href="#virtualprivatecloud-vpc-vpcbasic" id="virtualprivatecloud-vpc-vpcbasic"></a>

<figure><img src="https://docs.vngcloud.vn/download/attachments/49648036/image2023-9-7_11-1-37.png?version=1&#x26;modificationDate=1694059375000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

VPC consist of subnets which shared the same routing space, each VPC is identified by a unique routing space ID. Subnets are isolated from each other based on tunneling technology.

* Data packets are encapsulated and transmitted over a physical network between vServer instances.
* Data packets transmitted over vServer instances in different VPCs are in different routing space. Therefore, vServer instances in different VPCs cannot communicate with each other.

GreenNode developed VPCs that are integrated with virtual routers by adopting the tunneling and Software Defined Network (SDN) technologies.

### VPC and Subnet CIDR blocks <a href="#virtualprivatecloud-vpc-vpcandsubnetcidrblocks" id="virtualprivatecloud-vpc-vpcandsubnetcidrblocks"></a>

In this environment, it is necessary to create at least one VPC and one subnet that can be assigned to a virtual server or many GreenNode resources created later.

Each VPC is defined as one private CIDR block with address mask 16 and consists of at least one private CIDR/24 block or CIDR/28 block, a Subnet. You must use one of the private CIDR/16 blocks listed in the following table to define your VPC and smaller blocks /24 for Subnets (belong to VPC /16 block).

| CIDR blocks                   | Description                                                                                                      |
| ----------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| 192.168.0.0/16                | Number of available private IP addresses (excluding IP addresses reserved by the system): over 65K IP addresses  |
| 172.16.0.0/16 - 172.24.0.0/16 | Number of available private IP addresses (excluding IP addresses reserved by the system): over 500K IP addresses |
| 10.0.0.0/16 - 10.255.0.0/16   | Number of available private IP addresses (excluding IP addresses reserved by the system): over 16M IP addresses  |

A VPC is belong to only one Availability Zone in the Region. In order to span your network to multiple AZ or Region, you can use VPC Peering. See more at {VPC Peering page}

#### CIDR allocation for services

The system reserves CIDR blocks for the following services:

* **vDNS**
  * HCM: up to three `/28` subnets across three zones.
  * HAN: up to two `/28` subnets across two zones.
* **Peering**
  * Each peering connection uses two `/24` subnets, one from each connected VPC.
* **NAT**
  * HCM: up to three `/24` subnets across three zones.
  * HAN: up to two `/24` subnets across two zones.

### Route table <a href="#virtualprivatecloud-vpc-routetable" id="virtualprivatecloud-vpc-routetable"></a>

Your VPC has an implicit router with one main route table. All subnets in VPC is automatically routed to each others. You only use Route Table to control static routes where network traffic is directed as your needed.

When you create a VPC, it automatically has a main route table. By default, a route table is empty and you add static routes as needed. The static route will override dynamic route in case of route overlapping. See more at {Route Table page}

## Work with VPC <a href="#virtualprivatecloud-vpc-workwithvpc" id="virtualprivatecloud-vpc-workwithvpc"></a>

### Create a VPC <a href="#virtualprivatecloud-vpc-createavpc" id="virtualprivatecloud-vpc-createavpc"></a>

Follow the steps in this section to create a VPC:

1. Go to GreenNode console and navigate to VPC page
2. Create VPC and define CIDR/16 block

### View VPC detail and create or delete Subnet for VPC <a href="#virtualprivatecloud-vpc-viewvpcdetailandcreateordeletesubnetforvpc" id="virtualprivatecloud-vpc-viewvpcdetailandcreateordeletesubnetforvpc"></a>

In order to work with subnet in VPC, follow these steps:

1. Go to GreenNode console and navigate to VPC page
2. Select your VPC, click **View Detail** to expand the detail panel and Subnet tab view
3. Go to Subnet tab to work with subnets
4. You can create a subnet with defined CIDR/24 block or CIDR/28 block or delete existing subnet (if no resources is associated with the subnet)

### Delete a VPC <a href="#virtualprivatecloud-vpc-deleteavpc" id="virtualprivatecloud-vpc-deleteavpc"></a>

Before you can delete a VPC, you must first terminate or delete any resources that created a network interface in the VPC. For example, you must terminate your vServer instances, vLB, Internet Gateway... that related with the VPC.

Beside that, we will delete the following VPC components for you:

* Network ACLs
* Route tables
* Subnets

Procedure:

1. Go to GreenNode console and navigate to VPC page
2. Determine your VPC to delete, click **Delete** button on the right side and confirm.
