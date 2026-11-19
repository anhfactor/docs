# Starts with Interconnect

GreenNode Interconnect provides direct Layer 3 network connectivity. Interconnect connections do not use public internet. Instead, we offer direct connections that can provide higher reliability, faster and more stable speeds, and higher security levels.

***

### Key Points: <a href="#batdauvoiinterconnect-ychinh" id="batdauvoiinterconnect-ychinh"></a>

Interconnect establishes Layer 3 network connections between your on-premises network and the GreenNode network through a partner network provider.\
Dynamic routing is performed using the standard Border Gateway Protocol (BGP).\
You need to consider and select a failover capability to ensure you use an approach that suits your recovery needs. The option you choose will affect the Service Level Agreement (SLA) for your connection uptime.\
Connectivity is provided by using a cross-connect between devices owned by GreenNode and devices owned by the customer.

<figure><img src="https://docs.vngcloud.vn/download/attachments/64553619/image2023-9-8_14-30-47.png?version=1&#x26;modificationDate=1694158248000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

If you want to connect from your premises, you need to work with us to select a reasonable connection configuration, and then you'll need to directly contract to request an Interconnect connection.

During deployment, we will proceed based on:

**Dedicated Connection:**&#x45;xclusive access to the cross-connect, providing 1 Gbps or 10 Gbps bandwidth options (depending on the available bandwidth at your Direct Connect location). Multiple logical virtual interfaces can be created for each physical connection at selected Interconnect locations.

Next, set up the virtual connection type in one of the following ways:

**Virtual Routing Interface**: Use a virtual routing interface to access one or more GreenNode Transit Gateways associated with the Direct Connect port. You can use a virtual routing interface with any GreenNode Interconnect connection at any speed.\
**Public Virtual Interface:** Public virtual interfaces can access GreenNode public services using public IP addresses.\
**Private Virtual Interface:** Use a private virtual interface to access GreenNode VPC using private IP addresses.

***

### Creating Interconnect Connection: <a href="#batdauvoiinterconnect-taoketnoiinterconnect" id="batdauvoiinterconnect-taoketnoiinterconnect"></a>

Follow these steps to create an Interconnect connection to your location:

**Step 1: Select your Interconnect location:**

Determine your Interconnect location, the number of connections you want to use, and the port size. Multiple ports can be used simultaneously to increase bandwidth or redundancy.

**Step 2: Select your physical connection type:**

Choose between a dedicated connection or hosted connection. A dedicated connection provides you with exclusive access to the cross-connect and provides multiple virtual interfaces. With a hosted connection, partners share the cross-connect with multiple customers and only provide a single virtual interface. However, we currently only support dedicated connections for our customers.

**Step 3: Choose bandwidth:**

Depending on your usage needs, you can choose the bandwidth for your Interconnect connection. Currently, we offer two bandwidth options: 1Gb and 10Gb.

**Step 4: Choose the type of Interconnect connection:**

Currently, in addition to providing basic Direct Connect connections, we also deploy other types of connections such as Multicloud Connect, Hybrid Cloud Interconnect, VPN Interconnect to help you address diverse data management issues. For more detailed information, please see the [Interconnect Features](interconnect-features.md)

**Step 5: Create the Interconnect connection:**

he Interconnect creation feature has not been implemented in the user interface yet. To perform the creation operation, please send us a request at [https://support.vngcloud.vn/#/app/dashboard](https://support.vngcloud.vn/#/app/dashboard) with the information from Steps 1, 2, 3. Then we will help you proceed with the next steps to complete the connection.
