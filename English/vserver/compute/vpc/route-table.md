# Route Table

In a cloud environment, the Route table is an essential component of network management services, allowing network traffic routing between resources within a virtual network or a private network in the cloud.

**Route table** is a data table in a computer network used to decide how to route network traffic between networks, computers, or devices within a network system. It contains routing entries that describe network paths and linked network interfaces. Each routing entry in the route table includes information about the destination network address, the outgoing interface, and other parameters to decide the network path the packet will take.

**Route** is a specific entry in the route table that determines how network packets will be routed from the source to the destination. It includes information such as the destination network address, the next-hop address, and other attributes like metrics (priority measures) and the outgoing interface. Each routing entry in the route table represents a unique route, deciding how packets will be forwarded from the source to the destination through the network interfaces.

Overall, the route table is a data structure containing routing entries, while a route is a specific entry in the route table describing how to route network traffic from source to destination. The combination of the route table and its entries helps coordinate and manage network packet routing within the network system.

***

### Working with Route tables <a href="#routetable-lamviecvoiroutetable" id="routetable-lamviecvoiroutetable"></a>

#### Creating a Route table <a href="#routetable-taoroutetable" id="routetable-taoroutetable"></a>

Use the guide below to create a new Route table:

1. Open the vServer homepage at: [https://hcm-3.console.greennode.ai/vserver/overview](https://hcm-3.console.greennode.ai/vserver/overview).
2. In the navigation menu, select the **Network/Route table** tab.
3. Click **Create Route table**.
4. For **Name**, enter a descriptive name for the Route table. The Route table name can include letters (a-z, A-Z, 0-9, '\_', '-'). The input length should be between 5 and 50 characters. It must not include leading or trailing spaces.
5. Select a **VPC** for your Route table; if there is no VPC, create a new one according to the instructions on the [VPC page](virtual-private-cloud-vpc.md).
6. Click **Create** to create the new Route table.

#### Adding, Deleting, and Editing Routes <a href="#routetable-them-xoa-suaroute" id="routetable-them-xoa-suaroute"></a>

You can add, delete, and modify Routes in your Route table. You can only modify Routes that you have added:&#x20;

To update Routes for a Route table using the control panel:

1. Open the vServer homepage at: [https://hcm-3.console.greennode.ai/vserver/overview](https://hcm-3.console.greennode.ai/vserver/overview).
2. In the navigation menu, select the **Network/Route table tab**.
3. Select a Route table, then click **Edit Routes**.
4. In the Add new **Route** section, enter the following information:

| Destination      | `Target`      |
| ---------------- | ------------- |
| ex: 10.21.0.0/24 | ex: 10.21.0.0 |

For Destination, enter the **Destination CIDR**.

For Target, enter the **Target CIDR**.

5. To modify a Route, replace the destination CIDR block or an IP address in the Destination field. For Target, enter a Target CIDR.
6. To delete a Route, select **Delete**.
7. Click **Save** changes.

#### Deleting a Route table&#x20;

You can delete a Route table if you no longer need it. To delete a Route table using the routing table:

1. Open the vServer homepage at: [https://hcm-3.console.greennode.ai/vserver/overview](https://hcm-3.console.greennode.ai/vserver/overview).
2. In the navigation menu, select the **Network/Route table** tab.
3. Select the Route table to delete, then select the **Delete** action.
4. Click **Confirm**.
