# Package Bandwidth Dedicated

**Dedicated Bandwidth Package**

The Dedicated bandwidth package offers customizable speeds tailored to your needs. With this package, we commit to and guarantee service quality for customers with the required capacity. **This package is suitable for businesses or projects that need large and stable bandwidth, such as high-traffic websites, applications requiring fast and continuous network connections, or online services that need to ensure user experience quality.**

### **Creating a Package**

{% hint style="info" %}
**Note:**

* You can create up to 10 Dedicated bandwidth packages per account.
* When creating a bandwidth package, you can choose to purchase either Domestic bandwidth or International bandwidth, or both at the same time.
{% endhint %}

**Step 1:** Log in to your GreenNode account and go to [https://hcm-3.console.greennode.ai/vserver/](https://hcm-3.console.greennode.ai/vserver/)

**Step 2:** In the left-hand menu, under the **Network** section, select **Bandwidth**.

**Step 3:** Select the **Create Bandwidth** icon.

**Step 4:** Enter the **Bandwidth Name**. The name can include letters (a-z, A-Z, 0-9, '\_', '-'). The length of the name must be between 5 and 50 characters.

**Step 5:** Enter the **Description** or **Tag** for the bandwidth as desired.

**Step 6:** Choose the **Bandwidth Configuration**. Here, you can select:

* **Domestic bandwidth package:**

| **Package Name**   | **Bandwidth** | **Description**    |
| ------------------ | ------------- | ------------------ |
| Domestic 500 Mbps  | 500 Mbps      | 500 Mbps Domestic  |
| Domestic 1000 Mbps | 1000 Mbps     | 1000 Mbps Domestic |
| Domestic 2000 Mbps | 2000 Mbps     | 2000 Mbps Domestic |

* **International bandwidth package:**

| **Package Name**      | **Bandwidth** | Description           |
| --------------------- | ------------- | --------------------- |
| International 10 Mbps | 10 Mbps       | 10 Mbps International |
| International 20 Mbps | 20 Mbps       | 20 Mbps International |
| International 50 Mbps | 50 Mbps       | 50 Mbps International |

**Step 7:** Select **Allocate** and complete the payment steps as with normal resources.

***

### **Viewing Package Details**

**Step 1:** Log in to your GreenNode account and go to [https://hcm-3.console.greennode.ai/vserver/](https://hcm-3.console.greennode.ai/vserver/)

**Step 2:** In the left-hand menu, under the **Network** section, select **Bandwidth**.

**Step 3:** From the list of available bandwidth packages, select the **Dedicated** package.

**Step 4:** You can now view the details of this bandwidth package. On this screen, you can:

* **Add IP to the package:** By selecting the **Add IP** icon, you can choose the IP addresses you want to add to this bandwidth package. Details can be found in the section below.
* **Add a tag to the package:** By entering a **Key and Value** and selecting the **Add** icon, you can add a tag to this bandwidth package.

***

### **Adding IP Addresses to the Package**

{% hint style="info" %}
**Note:**

* IP addresses with the ATTACHED status mean that they have already been assigned to a bandwidth package. When you add these ATTACHED IP addresses to your bandwidth package, they will be removed from the old package and reassigned to the new one. **This ensures that an IP address can only be assigned to one bandwidth package at a time.**
{% endhint %}

**Step 1:** Log in to your GreenNode account and go to [https://hcm-3.console.greennode.ai/vserver/](https://hcm-3.console.greennode.ai/vserver/)

**Step 2:** In the left-hand menu, under the **Network** section, select **Bandwidth**.

**Step 3:** From the list of available bandwidth packages, select the **Dedicated** package according to your usage needs.

**Step 4:** Select the icon and then choose **Add IP**, or on the package detail screen, under the **IP List** section, select the **Add IP** icon.

**Step 5:** The **Add IP** screen will be displayed. You can filter the list of IP addresses by type by selecting an option in the **Resource Type** field. Currently, we provide the following resource types: **K8S, Floating IP, External Interface, vLB.**

**Step 6:** Select one or more IP addresses by selecting the icon ![](<../../../../.gitbook/assets/image (70) (2).png>) and then choosing **Add**.

***

### **Removing IP Addresses from the Package**

**Step 1:** Log in to your GreenNode account and go to [https://hcm-3.console.greennode.ai/vserver/](https://hcm-3.console.greennode.ai/vserver/)

**Step 2:** In the left-hand menu, under the **Network** section, select **Bandwidth**.

**Step 3:** From the list of available bandwidth packages, select the **Dedicated** package according to your usage needs.

**Step 4:** Under the **IP List** section, select the icon ![](<../../../../.gitbook/assets/image (71) (1).png>) next to the **IP address** you want to remove from the package and choose the icon ![](<../../../../.gitbook/assets/image (72) (2).png>)

**Step 5:** On the IP removal confirmation screen, select **Delete**.

{% hint style="info" %}
**Note:**

* When you remove an IP address from the Share package, this IP address will be reassigned to the default free bandwidth package **VNG Dedicated.**
{% endhint %}

***

### **Resize Package**

**Step 1:** Log in to your GreenNode account and go to [https://hcm-3.console.greennode.ai/vserver/](https://hcm-3.console.greennode.ai/vserver/)

**Step 2:** In the left-hand menu, under the **Network** section, select **Bandwidth**.

**Step 3:** From the list of available bandwidth packages, select the **Dedicated** package according to your change needs.

**Step 4:** Select the icon next to the **Dedicated bandwidth** you want to change and choose **Resize**.

**Step 5:** On the **Resize bandwidth** screen, select the **Domestic bandwidth** or **International bandwidth** package you want to change.

**Step 6:** Select **Resize bandwidth**. If you resize up, you will need to complete the payment as with normal resources. If you resize down, the system will refund the unused amount.
