# Instance IP Address

IP addresses are used to connect to vServer instances. There are two types of IP addresses can be used with vServer instances in VPC: private IP addresses and public IP addresses

## Private IP address <a href="#instanceipaddress-privateipaddress" id="instanceipaddress-privateipaddress"></a>

Each new vServer instance in a VPC is assigned a private IP address based on the CIDR block of the VPC and the CIDR block of the subnet to which the instance is connected.

Private IP addresses can be used in the following scenarios:

* Communication over the internal network between instances within the same VPC
* Communication over the internal network between instances and other cloud services such as vLB and vDB within the same VPC

Private IP address are automatically assigned via DHCP service and fixed to the instance until it is terminated.

## Public IP address <a href="#instanceipaddress-publicipaddress" id="instanceipaddress-publicipaddress"></a>

vServer instances in VPC support the following types of public IP addresses:

* Floating IP addresses: the public IP addresses that assigned to the instance by NAT 1:1 at GreenNode Gateway.
* External Interface: the public IP address that directly attached to the instance

The following table describes the major differences between the two types of public IP addresses.

| Item                                                              | Floating IP                                                                                                                                                                                   | External Interface                                                                                                                                                                                                     |
| ----------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Scenario                                                          | If you want an instance to have a public IP address that will not be attached (plug-in).                                                                                                      | If you want to direct attach a public IP address to instance as an interface                                                                                                                                           |
| Description                                                       | If you select **Floating IP** when you create an instance, a public IP address is assigned by NAT to the instance.                                                                            | After an External Interface is created, it can be attached with an instance that is not assigned a Floating IP address.                                                                                                |
| Method to view a media access control (MAC) address or IP address | Floating IP can not be discovered from within the instance because it is NAT at GreenNode gateway.                                                                                            | <p>Because this is attached interface, you can execute the External Interface directly from within the instance.</p><p>You must configure to use its IP address from within instance (configure static IP or DHCP)</p> |
| Method to disassociate an IP address                              | <p>After a Floating IP address is assigned to an instance, the FIP can only be disassociated from GreenNode view.</p><p>Billing for Floating IP will based on reservation request if any.</p> | <p>After a External Interface is attached to an instance, the External Interface can only be detach from GreenNode.</p><p>Billing still active until External Interface released</p>                                   |
| Method to release an IP address                                   | When Floating IP are disassociated from any instances, you can delete it from Floating IP page.                                                                                               | When External Interface are detached from any instances, you can delete it from External Interface page.                                                                                                               |
