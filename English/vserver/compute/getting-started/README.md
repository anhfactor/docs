# Getting started

Use this guide to get started with GreenNode Server (vServer). You will learn how to launch, connect and use. A typical example for creating a virtual server in the GreenNode. With vServer, you can set up and configure the operating system and expected accompanying applications.

When you first sign up for the vServer service, you can start with free usage for a great experience before deciding to pay. If you've created your account in 3 days and haven't exceeded the benefits of the free tier for vServer, it won't cost you anything to complete this guide as we help you choose options that fall within benefits of the free tier. At the end of the free tier, you will be charged for using the standard vServer from the time you launch the instance until you end the instance, even if it is idle.

## Overview: <a href="#gettingstarted-overview" id="gettingstarted-overview"></a>

You need to complete the following steps to be able to use our vServer service:

***

## **Step 1: Activate vServer:** <a href="#gettingstarted-step1-activatevserver" id="gettingstarted-step1-activatevserver"></a>

1. Open vServer homepage at: [https://hcm-3.console.greennode.ai/vserver/overview](https://hcm-3.console.greennode.ai/vserver/overview)
2. For a new customer's account, to be able to use the service you need to first activate vServer by creating a Project. In the **"Overview"** tab, click **Activate**

***

## **Step 2: Initialize VPC:** <a href="#gettingstarted-step2-initializevpc" id="gettingstarted-step2-initializevpc"></a>

Next to initialize vServer, you need a VPC:

1. Open vServer homepage at: [https://hcm-3.console.greennode.ai/vserver/overview](https://hcm-3.console.greennode.ai/vserver/overview)
2. At the navigation menu bar, select Tab **VPC**
3. Select **Create VPC**
4. For **Name**, enter a descriptive name for the VPC. VPC names can include letters (a-z, A-Z, 0-9, '\_', '-'). The input data length is between 5 and 50. It must not include leading or trailing spaces.
5. Enter IP information in the **CIDR** field. The IP address should be Private and can be selected for the following values:
   * 10.0.0.0 - 10.255.0.0
   * 172.16.0.0 - 172.24.0.0
   * 192.168.0.0

***

## **Step 3: Declare the Subnet:** <a href="#gettingstarted-step3-declarethesubnet" id="gettingstarted-step3-declarethesubnet"></a>

After the initialization of the initial VPC is complete, an additional step of Subnet initialization is required. We can create multiple Subnets for our VPC:

1. Open the VPC tab at: [https://hcm-3.console.greennode.ai/vserver/network/vpc](https://hcm-3.console.greennode.ai/vserver/network/vpc)
2. Click on your **VPC**, select the **Subnet** tab at the bottom of the page and select **Add Subnet**
3. For **Name**, enter a descriptive name for the Subnet. Subnet names can include letters (a-z, A-Z, 0-9, '\_', '-'). The input data length is between 5 and 50. It must not include leading or trailing spaces.
4. Enter **IP** information in the **CIDR** field. The CIDR value of the Subnet must be in the network class of the previously created VPC. For example, the previous VPC we created with a CIDR of 192.168.0.0/16, the Subnet will have the form: 192.168.xxx.0/24

***

## **Step 4: Initialize Server:** <a href="#gettingstarted-step4-initializeserver" id="gettingstarted-step4-initializeserver"></a>

This guide helps you quickly launch your first **Server,** so it won't cover all the must-have options, but you'll get the Server up and running in just a few simple steps:

1. Open the Server tab at: [https://hcm-3.console.greennode.ai/vserver/v-server/cloud-server](https://hcm-3.console.greennode.ai/vserver/v-server/cloud-server)
2. Select **Create a Server**
3. In the **Basic Configuration** section, enter the **Server name** to describe the name for your Server. Server name can include letters (a-z, A-Z, 0-9, '\_', '-'). The input data length is between 5 and 50. It must not include leading or trailing spaces and the Server name must be different from the Username.
4. Choose from the following options in the **Image** section:

**Option 1**: Initialize vServer from a brand new **blank OS**

* At the **OS IMAGES** tab, select the OS Type (Ubuntu, Debian, CentOS, Windows, ...) and the corresponding OS version, select **Next**

**Option 2**: Initialize vServer with **GPU IMAGES** advanced support for graphics processing

* At **GPU IMAGES** tab, select OS Type (Ubuntu, Windows, ...) and corresponding OS version, select **Next**

**Option 3**: Initialize vServer with previously created MY IMAGES, to serve Clone Server running on Cloud into new Servers or Backup / Restore Server

* At the **My Images** tab, select the corresponding images needed to create the vServer, select Next.&#x20;

5\. Under section **Instance type**, is a list of Flavor configurations, you can choose the desired Flavor configuration for your Server by. **iot.v1.small1x1** is recommended by us as the default basic configuration for server initialization

6\. In the section **Volume Settings**, enter the configuration for Boot OS Volume (Root) including **Size GB**, **Volume Type SSD** and **IOPS**, then select **Next**

In addition, you can add **Data Volume** to the Server during the initialization process by selecting **Add Data volume**, then enter the configuration for the Data Volume including **Volume name**, **Size GB,** **Volume Type SSD** and **IOPS**, then select **Next**

7\. Next is the **Network settings:**

\+  Here you can choose **VPC** to grant Private IP to Server and **Subnet** from the list you created earlier, or you can choose [**Click here**](https://hcm-3.console.greennode.ai/vserver/network/vpc) to manage your VPCs to create new VPC and Subnet, it should be noted that after creating VPC and Subnet Subnet, it will be displayed at the list page allowing you to choose during Server initialization

\+  Check the box **Floating IP** to assign Public IP to the Server&#x20;

\+  **Security group** to manage the ACL - Access Control List for the Server. ([**Click here**](../server-group.md) for instructions on creating and managing a Security group)

\+  **SSH Key** to import to the Server during initialization. ([**Click here**](../security/ssh-key-key-pairs.md) for instructions)

\+  **Authentication** Information: Empty: the system will automatically generate and assign a password or the user can manually tweak and enable or disable the bypass of the first password change.

8\. In the **Other Settings** section, you can choose **Server Group** or not according to your needs. You can assign the Server to previously created Groups (With attributes such as the same Compute Host or different Compute Host)

***

## **Step 5: Pay and complete the Server initialization process:** <a href="#gettingstarted-step5-payandcompletetheserverinitializationprocess" id="gettingstarted-step5-payandcompletetheserverinitializationprocess"></a>

After filling in the necessary information to initialize the Server, it is necessary to review the summary of information in the **Summary** tab on the left side of the screen and detailed payment information for the items in the **Item list** tab. If you are ready, select **Launch Server** to confirm initialization of your Server.

On the Server list screen, you can see the launch status. It takes a short time for a Server to launch. Its initial state is pending. After the Server starts, its status changes to running. Note that it may take a few minutes for the Server to be ready for you to connect to it. Check if your Server has passed the status check; you can see this information in the Check Status column.

***

### Searching for Created Servers

In cases where users create many virtual machines (VMs), GreenNode provides a tool to quickly search for the virtual machines that users have previously created.

**Step 1:** Open the vServer homepage at: [https://hcm-3.console.greennode.ai/vserver/overview](https://hcm-3.console.greennode.ai/vserver/overview)

**Step 2:** Select the **Servers** section to go to the screen listing the created virtual machines.

**Step 3:** Select the **"Search with Suggestion"** box to choose the criteria to search for the specific virtual machine you need:

* **Search by Name**: Search by the name of the Server.
* **Search by Private IP**: Search by the private IP of the Server.
* **Search by Public IP**: Search by the public IP of the Server.
* **Search by Subnet ID**: Search by the Subnet ID where the Server was created.
* **Search by VPC ID**: Search by the VPC ID where the Server was created.
* **Search by Tag**: Search by the Tag assigned to the Server at creation.

**Step 4:** Enter the required search information and confirm the search to allow the system to automatically find the servers matching the keywords.

