# Package Bandwidth Share

The Share bandwidth package offers high-speed bandwidth shared among multiple customers. The speed of this package may vary at different times of the day. **This package is suitable for small businesses or projects that do not require large and consistently stable bandwidth.** If you only need bandwidth to maintain basic activities without high network performance requirements, this is the most reasonable choice for you.

### **View Detailed Package Information**

**Step 1**: Log in to your GreenNode account and go to [https://hcm-3.console.greennode.ai/vserver/](https://hcm-3.console.greennode.ai/vserver/).

**Step 2**: In the left-hand menu, under the **Network** section, select **Bandwidth**.

**Step 3**: From the list of available bandwidth packages, select the **Share** package.

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

* IP addresses with the ATTACHED status mean that they have already been assigned to a bandwidth package. When you add these ATTACHED IP addresses to your bandwidth package, they will be removed from the old package and reassigned to the new one. This ensures that an IP address can only be assigned to one bandwidth package at a time.
{% endhint %}

**To add IP addresses to the package, follow these steps:**

**Step 1**: Log in to your GreenNode account and go to [https://hcm-3.console.greennode.ai/vserver/](https://hcm-3.console.greennode.ai/vserver/).

**Step 2**: In the left-hand menu, under the **Network** section, select **Bandwidth**.

**Step 3**: From the list of available bandwidth packages, select the **Share** package according to your usage needs.

**Step 4**: Select the icon and then choose **Add IP**, or on the package detail screen, under the **IP List** section, select the **Add** IP icon.

**Step 5**: The **Add IP** screen will be displayed. You can filter the list of IP addresses by type by selecting an option in the **Resource Type** field. Currently, we provide the following resource types: **K8S, Floating IP, External Interface, vLB.**

**Step 6**: Select one or more IP addresses by selecting the icon ![](<../../../../.gitbook/assets/image (67) (2).png>)and then choosing **Add**.

***

### **Remove IP Addresses from the Package**

To remove IP addresses from the package, follow these steps:

**Step 1**: Log in to your GreenNode account and go to [https://hcm-3.console.greennode.ai/vserver/](https://hcm-3.console.greennode.ai/vserver/).

**Step 2**: In the left-hand menu, under the **Network** section, select **Bandwidth**.

**Step 3**: From the list of available bandwidth packages, select the **Share** package according to your usage needs.

**Step 4**: Under the **IP List** section, select the icon ![](<../../../../.gitbook/assets/image (68) (2).png>)next to the IP address you want to remove from the package and choose the icon ![](<../../../../.gitbook/assets/image (69) (2).png>)

**Step 5**: On the IP removal confirmation screen, select **Delete**.

{% hint style="info" %}
**Note:**

* When you remove an IP address from the Share package, this IP address will be reassigned to the default free bandwidth package, VNG Dedicated.
{% endhint %}
