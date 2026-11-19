# Floating IP

An floating IP address (FIP) is a public IP address that you can reserve and use as an independent resource. FIPs can be retained independently and associated with or disassociated from primary interface of instances in virtual private clouds (VPCs).

### **Overview** <a href="#floatingip-overview" id="floatingip-overview"></a>

FIPs are NAT IP addresses that are located in the gateway of GreenNode. By means of NAT, FIPs are mapped to the primary network interfaces of the vServer instances. You can associate FIPs with vServer instances that are located in VPCs to enable the instances to communicate over the Internet. FIPs is invisible inside the operating systems of vServer instances.

{% hint style="warning" %}
When using a Floating IP for outbound Internet access, keep the packet MTU **<= 4000** to reduce the risk of packet loss.

For MTU/DF-flag sensitive workloads (VPN tunnels, SIP/UDP, etc.), see [MTU & “DF flag” best practice on GreenNode](../../vmarketplace/network-software-installation/pfsense-on-hcm03/mtu-and-df-flag-best-practice-on-vng-cloud.md).
{% endhint %}

### **Limits** <a href="#floatingip-limits" id="floatingip-limits"></a>

FIPs can be associated with vServer instances. An FIP can be associated only with an vServer instance that meets the following requirements:

* The vServer instance is located in a VPC.
* The vServer instance is located in the same zone as the FIP.
* The vServer instance is in the **Running** or **Stopped** state.
* No External Interface are attached.

***

### **Operations** <a href="#floatingip-operations" id="floatingip-operations"></a>

#### Create an Floating IP

A Floating IP is created along with the Server initialization. However, you can view the list of Floating IPs attached to the Server in the vServer control panel at the following link: [https://hcm-3.console.greennode.ai/vserver/network/wan-ip](https://hcm-3.console.greennode.ai/vserver/network/wan-ip)

#### Associate an Floating IP with an vServer instance

* You can log on to the [Server page](https://hcm-3.console.greennode.ai/vserver/v-server/cloud-server) and associate an Floating IP with an vServer instance that is located in a VPC and is not attached External Interface.
* You can also go to the [Floating IP page](https://hcm-3.console.greennode.ai/vserver/network/wan-ip) and associate an Floating IP with an vServer instance that is located in a VPC and is not attached External Interface.

#### Disassociate an Floating IP from an vServer instance

* If your vServer instance no longer needs an Floating IP, you can disassociate the Floating IP from the instance in the [Server page](https://hcm-3.console.greennode.ai/vserver/v-server/cloud-server).
* You can also disassociate the Floating IP from the vServer instance on the [Floating IP page](https://hcm-3.console.greennode.ai/vserver/network/wan-ip)

#### Release an Floating IP

* Billing of an Floating IP continues after it is disassociated. If you no longer need the Floating IP, go to the [Floating IP page](https://hcm-3.console.greennode.ai/vserver/network/wan-ip) to release the Floating IP

<br>
