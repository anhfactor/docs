# Create a VPC Connection

**Follow these steps to create a VPC connection between two regions:**

**Step 1**: Successfully log in to GreenNode, and on the Console screen, navigate to the vNetwork service;

**Step 2**: In the left-hand menu of the vNetwork interface, select the Cross Connect section;

**Step 3**: The screen will navigate to the Cross Connect List page;

**Step 4**: On the Cross Connect list screen, click on the previously created Cross Connect;

<figure><img src="../../.gitbook/assets/image (294).png" alt=""><figcaption></figcaption></figure>

**Step 5**: On the Cross Connect detail screen, in the Connections tab, click '**Add More Connections**' to create a VPC connection between the two regions;

<figure><img src="../../.gitbook/assets/image (295).png" alt=""><figcaption></figcaption></figure>

**Step 6**: On the **Add more VPC's Connections** screen:

* The user must first select the **Requester's VPC**;
* The system will check connection conditions based on the selected Requester's VPC and display the available **Accepter's VPCs** that can be connected;

<figure><img src="../../.gitbook/assets/image (296).png" alt=""><figcaption></figcaption></figure>

**Step 7**: After selecting the VPC pair to connect, click 'Add' to create a new VPC connection pair. The system will then establish the connection, and if successful, the status will be 'Active.' Additionally, the number of VPC connections will increase and be displayed on the Cross Connect list screen.

<figure><img src="../../.gitbook/assets/image (297).png" alt=""><figcaption><p>Describe the pairing process between two VPCs.</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (298).png" alt=""><figcaption><p>The result is the connection status of the newly connected VPC pair.</p></figcaption></figure>

{% hint style="info" %}
**Note:**

* The **Requester Region** and **Accepter Region** are understood to be two independent regions that form a Cross Connect connection (the Requester Region is automatically selected based on the region chosen when accessing vServer).
* The VPCs in each region must be pre-created in vServer (refer to [**Create VPC**](../../vserver/compute/vpc/virtual-private-cloud-vpc.md)).
{% endhint %}
