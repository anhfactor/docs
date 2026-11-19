# Package Bandwidth VNG Dedicated

The VNG Dedicated bandwidth package is the default free package with standard speed for all customers. In this package, we provide up to 300Mbps domestic bandwidth and up to 5Mbps international bandwidth. **By default, all your IP addresses will adhere to this package's bandwidth standards.**

### **View Detailed Package Information**

**Step 1**: Log in to your GreenNode account and go to[ https://hcm-3.console.greennode.ai/vserver/](https://hcm-3.console.greennode.ai/vserver/).

**Step 2**: In the left-hand menu, under the **Network** section, select **Bandwidth**.

**Step 3**: From the list of available bandwidth packages, select the **VNG Dedicated** package.

**Step 4**: You can now view the details of this bandwidth package. On this screen, you can:

* **Add IP to the package**: By selecting the **Add IP** icon, you can choose the IP addresses you want to add to this bandwidth package. Details can be found in the section below.
* **Add a tag to the package**: By entering a **Key and Value** and selecting the **Add** icon, you can add a tag to this bandwidth package.

{% hint style="info" %}
**Note:**

* This is the default bandwidth package that is automatically created and added to your service package. You cannot delete or change the configuration of this package.
* From the moment you create a new resource, within approximately one minute, these IP addresses will be automatically assigned to the **VNG Dedicated** bandwidth package.
{% endhint %}

***

### **Add IP Addresses to the Package** **Note**

{% hint style="info" %}
**Note:**

* You can only add IPs to this bandwidth package, but you cannot remove IPs with default bandwidth.
* IP addresses with the ATTACHED status mean that they have already been assigned to a bandwidth package. When you add these ATTACHED IP addresses to your bandwidth package, they will be removed from the old package and reassigned to the new one. **This ensures that an IP address can only be assigned to one bandwidth package at a time.**
{% endhint %}

**To add IP addresses to the package, follow these steps:**

**Step 1**: Log in to your GreenNode account and go to[ https://hcm-3.console.greennode.ai/vserver/](https://hcm-3.console.greennode.ai/vserver/).

**Step 2**: In the left-hand menu, under the **Network** section, select **Bandwidth**.

**Step 3**: From the list of available bandwidth packages, select the **VNG Dedicated** package.

**Step 4**: Select the icon <img src="../../../../.gitbook/assets/image (62).png" alt="" data-size="line"> and then choose **Add IP**, or on the package detail screen, under the **IP List** section, select the **Add IP icon**.

**Step 5**: The **Add IP** screen will be displayed. You can filter the list of IP addresses by type by selecting an option in the **Resource Type** field. Currently, we provide the following resource types: **K8S, Floating IP, External Interface, vLB.**

**Step 6**: Select one or more IP addresses by selecting the icon <img src="../../../../.gitbook/assets/image (63) (2).png" alt="" data-size="line">and then choosing **Add**.
