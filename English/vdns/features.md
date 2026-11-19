# Features

### A Powerful DNS Solution for Private Cloud Infrastructure

vDNS is a DNS service specifically designed for Private Cloud environments on GreenNode, providing secure, flexible, and efficient domain management and resolution within Virtual Private Clouds (VPCs).

### Core Features of vDNS

#### Enable Private DNS Server for VPCs

This feature allows you to enable a dedicated DNS server within your VPC. It ensures that virtual machines (VMs) inside the VPC can resolve domain names privately without using the public internet.

Enabling the Private DNS Server will create one or more dedicated IP addresses for the DNS server within the VPC. These addresses will be automatically configured for VMs in the VPC via DHCP.

This is a prerequisite step for using other vDNS features within the VPC.

{% hint style="info" %}
**Important Note:** Enabling Private DNS will modify the DHCP Option Set of VMs in the network. Therefore, after enabling the feature, you need to update DHCP on the VMs so they can receive the new DNS configuration. Please refer to the DHCP update guide [here.](../vserver/compute/vpc/dhcp-options-sets/)
{% endhint %}

### Create Hosted Zone

A Hosted Zone is a container for DNS records of a specific domain (for example: `example.com`).

vDNS allows you to create two types of Hosted Zones:

* **Public Hosted Zone:** Used for public domains that can be resolved from the internet. _(Currently not supported in this version.)_
* **Private Hosted Zone:** Used for internal domains that can only be resolved within associated VPCs.

#### Important Point

When creating a Private Hosted Zone, vDNS only allows association with VPCs that have the Private DNS Server feature enabled. This ensures network security and isolation.

### Edit Hosted Zone

#### Attach or Detach VPCs from a Hosted Zone

After creating a Hosted Zone (especially a Private Hosted Zone), you can easily modify it by adding or removing associated VPCs.

This allows you to control the resolution scope of a domain. For example, you can allow an internal domain to be resolved by multiple VPCs or restrict it to a single VPC only.

### Create Records

Supports 6 record types and 3 routing policies.

vDNS fully supports common DNS record types:

* **A:** Maps a domain name to an IPv4 address.
* **CNAME:** Creates an alias for another domain name.
* **MX:** Specifies mail servers.
* **SRV:** Specifies the location of specific services.
* **TXT:** Stores arbitrary text.
* **PTR:** Performs reverse DNS lookup, mapping an IP address back to a domain name.

vDNS also provides flexible routing policies:

* **Simple Routing:** Simple routing that returns a set of resources in order.
* **Geolocation Routing:** Routes traffic based on the user’s geographic location.
* **Weighted Routing (with Sticky Session):** Distributes traffic based on weights while maintaining session persistence.

_(Terraform integration for vDNS is currently not supported.)_
