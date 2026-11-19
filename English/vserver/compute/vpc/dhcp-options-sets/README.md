# DHCP Options Sets

## Overview

The **DHCP** (Dynamic Host Configuration Protocol) feature allows you to configure the DNS server IP address for virtual machines (VM) in a vServer within a VPC. Before you can use a DHCP options set, you must first have the DNS server IP address, after which you can associate the DHCP options set with a VPC. Once a DHCP options set is associated with a VPC, if a VM is created within the VPC using that DHCP options set, the VM will also use that DHCP options set after synchronization.

**Some notes when configuring a DHCP options set:**

* A DHCP options set can only be associated with one VPC deployed in the region where the DHCP was created;
* **A DHCP options set** is allowed to be **associated with multiple VPCs**;
* **A VPC** can only be **associated with one DHCP options set**;
* There is a **limit of 10 DHCP options sets per user** that can be created (this limit cannot be increased).

{% hint style="info" %}
**Note:**

After configuring DNS for a VM, to refresh the DHCP usage on the VM, you can either restart the VM, or wait for the lease to expire, or manually run the following commands:

* **For Linux servers**: Run the command _<mark style="background-color:orange;">sudo dhclient -r && sudo dhclient</mark>_
* **For Windows Server**: Run the command _<mark style="background-color:orange;">ipconfig /renew</mark>_
{% endhint %}

***

## Creating a DHCP Options Set

This guide will help you create a DHCP options set by following these steps:

1. Log in to GreenNode and navigate to the vServer service;
2. On the vServer screen, choose the appropriate region;
3. In the left-hand menu, select **DHCPs**;

<figure><img src="../../../../.gitbook/assets/image (278).png" alt=""><figcaption></figcaption></figure>

4. On the DHCP options sets list screen, click the **Create a DHCP Options Set** button;

<figure><img src="../../../../.gitbook/assets/image (279).png" alt=""><figcaption></figcaption></figure>

5. On the DHCP options set creation page, enter the following information:

* **DHCP Option Set name**: Enter a name for the DHCP options set;
* **Description:** Enter a description for the DHCP options set;
* **DHCP Server IP:** By default, GreenNode's DNS Server is automatically provided for the VPC.
  * Click the "**Set to Optimize**" button to manually enter the DNS Server IP;
  * Note that if you do not use the default DNS, you may experience failures when accessing GreenNode services.

{% hint style="info" %}
**The default DNS server IP addresses provided by GreenNode:**

* 10.166.12.196
* 10.166.12.197

You can **enter up to 4 DNS server IP addresses** (you may add 2 more if you are still using the system's 2 default IPs).
{% endhint %}

<figure><img src="../../../../.gitbook/assets/image (280).png" alt=""><figcaption></figcaption></figure>

6. After completing the setup, click the **Create** button to finalize the configuration.

<figure><img src="../../../../.gitbook/assets/image (281).png" alt=""><figcaption></figcaption></figure>

***

## Associating with a VPC

After creating a DHCP options set, you need to associate it with a VPC. There are two ways to perform the association (Associate). Follow these steps:

1. Log in to GreenNode and navigate to the vServer service;
2. On the vServer screen, choose the appropriate region;
3. In the left-hand menu, select **DHCPs**;
4. Select an existing DHCP set to access the details screen;
5. On the details screen, in the **Associated VPCs** tab, all VPCs associated with this set are listed;

<figure><img src="../../../../.gitbook/assets/image (282).png" alt=""><figcaption></figcaption></figure>

6. Click the **Associate** button to list all available VPCs, select the desired VPC, and click **Associate**.

<figure><img src="../../../../.gitbook/assets/image (283).png" alt=""><figcaption></figcaption></figure>

After the successful association, the information of the associated VPC will be displayed on the list of VPCs associated with the detailed DHCP on the screen.

<figure><img src="../../../../.gitbook/assets/image (284).png" alt=""><figcaption></figcaption></figure>

***

## Deleting a DHCP options set

Trong quá trình sử dụng DHCP options set, người dùng có thể xóa DHCP options set. Tuy nhiên, khi xóa được một DHCP options set cần thực hiện:

### Step 1: Detach all VPCs from the DHCP options set

1. Log in to GreenNode and navigate to the vServer service;
2. On the vServer screen, choose the appropriate region;
3. In the left-hand menu, select **DHCP Options Sets**;
4. Select the DHCP options set you want to delete to access its details;
5. On the details screen, in the **Associated VPCs** tab, all associated VPCs are listed. Select all associated VPCs and click **Detach** to remove them;

<figure><img src="../../../../.gitbook/assets/image (285).png" alt=""><figcaption></figcaption></figure>

6. Confirm the detachment of all VPCs from the DHCP options set.

### Step 2: Delete the DHCP Options Set

1. After detaching all VPCs from the DHCP options set, return to the DHCP options set list;
2. Find the DHCP options set you wish to delete, and click the **Delete** action;
3. Confirm the deletion of the DHCP options set. Once deleted, the DHCP options set cannot be recovered.

<figure><img src="../../../../.gitbook/assets/image (287).png" alt=""><figcaption></figcaption></figure>
