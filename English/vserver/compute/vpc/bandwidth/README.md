# Bandwidth

### **Overview**

**Bandwidth** is the amount of data transmitted to and from your virtual server over a certain period, typically a month. Bandwidth is usually measured in units such as kilobits per second (kbps), megabits per second (Mbps), gigabits per second (Gbps), etc. Additionally, bandwidth plays a crucial role in speeding up data access and improving application performance.

With GreenNode, we currently offer four bandwidth packages for customers to choose from:

* **VNG Dedicated**: This is the default free bandwidth package with standard speed for all customers. In this package, we provide up to 300Mbps domestic bandwidth and up to 5Mbps international bandwidth. **This package is suitable for customers with stable and unchanging bandwidth needs over time. It is a good choice for businesses looking to avoid unforeseen costs and need a fixed rate.**
* **Pay As You Go**: This is the bandwidth package where you pay for the amount of bandwidth used beyond the free bandwidth package (VNG Dedicated). **This can be more reasonable for businesses with fluctuating bandwidth needs, requiring flexibility and quick scalability without being limited by fixed bandwidth levels**. The Pay As You Go package includes three specific packages:
  * **PAYG-ALL**: This package allows you to use unlimited bandwidth for both domestic and international traffic. You will pay for the total bandwidth used beyond the free limit, regardless of whether the traffic is domestic or international. **This package is suitable for businesses or individuals with large and diverse bandwidth needs, both domestic and international.**
  * **PAYG-DOMESTIC**: This package applies to domestic bandwidth usage. You will pay for the amount of bandwidth used beyond the free limit dedicated to domestic traffic. In this package, international traffic will follow the default package configuration. **This package is suitable for businesses or individuals primarily operating domestically with large domestic bandwidth needs.**
  * **PAYG-INTERNATIONAL**: This package applies to international bandwidth usage. You will pay for the amount of bandwidth used beyond the free limit dedicated to international traffic. In this package, domestic traffic will follow the default package configuration. **This package is suitable for businesses or individuals with high international bandwidth needs but low domestic bandwidth.**
* **Share**: This is a high-speed shared bandwidth package for multiple customers to use. The speed of this package may vary at different times of the day. **This package is suitable for small businesses or projects that do not require large and consistently stable bandwidth**. If you only need bandwidth to maintain basic operations without high network performance requirements, this is the most reasonable choice for you.

<figure><img src="../../../../.gitbook/assets/image (60) (1).png" alt=""><figcaption></figcaption></figure>

* **Dedicated**: This is a bandwidth package with a customizable speed of your own. With this package, we commit to ensuring the service quality for customers with the required capacity. **This package is suitable for businesses or projects that need large and stable bandwidth, such as websites with high traffic, applications requiring fast and continuous network connections, or online services needing to ensure user experience quality.**

<figure><img src="../../../../.gitbook/assets/image (61) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Note:**

* The **VNG Dedicated, Pay As You Go, and Share** bandwidth packages are automatically created and added to your service package. These packages are marked with the "**System**" label on the interface.
* The **VNG Dedicated** bandwidth package is chosen as the default package for all IP addresses (IP on all your resources on the **vServer**). This package is marked with the "**Default**" label on the interface.
* From the moment you create a new resource, within approximately one minute, these IP addresses will be automatically assigned to the **VNG Dedicated** bandwidth package. You can add these IPs to other bandwidth packages according to your needs, or you can customize and create bandwidth packages as desired within the **Dedicated** package.
{% endhint %}
