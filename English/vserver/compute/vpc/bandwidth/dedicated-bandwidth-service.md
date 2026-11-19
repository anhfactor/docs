# Package Bandwidth Pay As You Go

The Pay As You Go bandwidth package requires you to pay for the amount of bandwidth used beyond the free bandwidth package (VNG Dedicated). This Pay As You Go package includes three specific packages:

* **PAYG-ALL**: This package allows you to use unlimited bandwidth for both domestic and international traffic. You will pay for the total bandwidth used beyond the free limit, regardless of whether the traffic is domestic or international.
* **PAYG-DOMESTIC**: This package applies to domestic bandwidth usage. You will pay for the amount of bandwidth used beyond the free limit dedicated to **domestic** traffic. In this package, international traffic will follow the default package configuration.
* **PAYG-INTERNATIONAL**: This package applies to international bandwidth usage. You will pay for the amount of bandwidth used beyond the free limit dedicated to **international** traffic. In this package, domestic traffic will follow the default package configuration.

***

### **View Detailed Package Information**

**Step 1**: Log in to your GreenNode account and go to [https://hcm-3.console.greennode.ai/vserver/](https://hcm-3.console.greennode.ai/vserver/).

**Step 2**: In the left-hand menu, under the **Network** section, select **Bandwidth**.

**Step 3**: From the list of available bandwidth packages, select the **Pay As You Go** package.

**Step 4**: You can now view the details of this bandwidth package. On this screen, you can:

* **Add IP to the package**: By selecting the **Add IP** icon, you can choose the IP addresses you want to add to this bandwidth package. Details can be found in the section below.
* **Add a tag to the package**: By entering a **Key and Value** and selecting the **Add** icon, you can add a tag to this bandwidth package.

{% hint style="info" %}
**Note:**

* This is a default bandwidth package automatically created and added to your service package. You cannot delete or change the configuration of this package.
{% endhint %}

***

### **Add IP Addresses to the Package**

{% hint style="info" %}
**Note:**

* IP addresses with the ATTACHED status mean that they have already been assigned to a bandwidth package. When you add these ATTACHED IP addresses to your bandwidth package, they will be removed from the old package and reassigned to the new one. **This ensures that an IP address can only be assigned to one bandwidth package at a time.**
{% endhint %}

**To add IP addresses to the package, follow these steps:**

**Step 1**: Log in to your GreenNode account and go to [https://hcm-3.console.greennode.ai/vserver/](https://hcm-3.console.greennode.ai/vserver/).

**Step 2**: In the left-hand menu, under the **Network** section, select **Bandwidth**.

**Step 3**: From the list of available bandwidth packages, select the **PAYG-ALL, PAYG-DOMESTIC, or PAYG-INTERNATIONAL** package according to your needs.

**Step 4**: Select the icon and then choose **Add IP**, or on the package detail screen, under the **IP List** section, select the **Add IP** icon.

**Step 5**: The **Add IP** screen will be displayed. You can filter the list of IP addresses by type by selecting an option in the **Resource Type** field. Currently, we provide the following resource types: **K8S, Floating IP, External Interface, vLB.**

**Step 6**: Select one or more IP addresses by selecting the icon <img src="../../../../.gitbook/assets/image (64) (1).png" alt="" data-size="line">and then choosing **Add**.

***

### **Remove IP Addresses from the Package**

To remove IP addresses from the package, follow these steps:

**Step 1**: Log in to your GreenNode account and go to [https://hcm-3.console.greennode.ai/vserver/](https://hcm-3.console.greennode.ai/vserver/).

**Step 2**: In the left-hand menu, under the **Network** section, select **Bandwidth**.

**Step 3**: From the list of available bandwidth packages, select the **PAYG-ALL, PAYG-DOMESTIC, or PAYG-INTERNATIONAL** package according to your needs.

**Step 4**: Under the **IP List** section, select the icon <img src="../../../../.gitbook/assets/image (65) (1).png" alt="" data-size="line">next to the IP address you want to remove from the package and choose the icon <img src="../../../../.gitbook/assets/image (66) (2).png" alt="" data-size="line">.

**Step 5**: On the IP removal confirmation screen, select **Delete**.

{% hint style="info" %}
**Note:**

* When you remove an IP address from the Pay As You Go package, this IP address will be reassigned to the default free bandwidth package, VNG Dedicated.
{% endhint %}
