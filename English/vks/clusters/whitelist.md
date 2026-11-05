# Whitelist

#### O**verview** <a href="#tong-quan" id="tong-quan"></a>

The IP Whitelist feature on VKS's Private Node Group mode allows you to only allow specific IP addresses to connect to your Cluster. This helps increase security for applications and sensitive data by restricting access from unknown sources.

**Benefit**

* **Enhanced security:** IP Whitelist helps protect your data and applications from potential threats on public networks, such as cyberattacks and data breaches.
* **Minimize risk:** By restricting access to sensitive nodes, Whitelist IP helps minimize the risk of spreading a data breach to other parts of your network.
* **Greater control:** Whitelist IP allows you to tightly control access to your nodes, ensuring only authorized users and applications can access.

{% hint style="info" %}
**Recommendations for Using Whitelists in Different Cluster Models**

**1. Public Cluster Containing Only Public Node Groups**

**Recommendation:** Whitelisting is **not recommended**.

For users in the **HCM Region**, if you need to enable IP Whitelisting for security reasons, please allow the following **vServer public IP ranges**:

```
49.213.64.0/23
49.213.71.0/24
49.213.83.0/24
49.213.86.0/23
49.213.89.0/24
61.28.224.0/20
61.28.250.0/24
103.245.248.0/22
58.84.0.0/22
116.118.88.0/21
180.93.180.0/22
120.138.75.0/24
120.138.79.0/24
122.201.13.0/24
122.201.15.0/24
103.196.238.0/23
103.245.254.0/23
210.245.38.93/32
```

For users in the **HAN Region**, if you need to enable IP Whitelisting for security reasons, please allow the following **vServer public IP ranges**:

```
42.1.126.0/23
157.20.201.0/24
157.20.200.96/27  
157.20.200.128/25
```

***

**2. Public Cluster with Private Node Group Using a NAT Gateway (e.g., pfSense, Palo Alto)**

**Recommendation:** Whitelisting **can be used**.\
Make sure to whitelist the **IP address of the NAT Gateway**.

***

**3. Private Cluster with Public or Private Node Group**

**Recommendation:** Whitelisting **can be used**.
{% endhint %}

***

## Edit Whitelist <a href="#chinh-sua-whitelist" id="chinh-sua-whitelist"></a>

To use the IP Whitelist feature on Private Node Group mode, you need to perform the following steps:

**Step 1:** Visit [https://vks.console.greennode.ai/overview](https://vks.console-dev.vngcloud.tech/overview)

**Step 2: At the Overview** screen , select the **Kubernetes Cluster menu.**

**Step 3:** Select the icon ![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2Fdocs-admin.vngcloud.vn%2Fdownload%2Fthumbnails%2F73762015%2Fimage2024-4-16_15-51-55.png%3Fversion%3D1%26modificationDate%3D1713262579000%26api%3Dv2\&width=40\&dpr=4\&quality=100\&sign=10c09f1b\&sv=1)and select **Edit Whitelist or select the Edit** icon when viewing details of a Cluster to add a Whitelist to your Cluster.

**Step 4:** Now, the **Edit Whitelist** screen displays, you can enter the IP address you want to allow access to the Cluster then select **Add** .

**Step 5:** Repeat step 4 if you want to add more **Whitelist IPs** to your Cluster. You can also select **Delete** to delete the Whitelist IP you added previously.

**Step 6:** Select **Save** to save the information or **Cancel** to cancel saving these parameters.
