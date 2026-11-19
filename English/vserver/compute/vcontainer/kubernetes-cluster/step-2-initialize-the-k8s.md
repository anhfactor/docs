# Step 2: Initialize the K8S

This topic provides an overview of available options and describes what to consider when you create a Kubernetes Cluster (K8S). If this is your first time creating a K8S, we recommend that you follow our instructions below. This tutorial helps you create a simple, default Kubernetes Cluster without expanding to all the available options.

### **Prerequisites**  <a href="#step2-initializethek8s-prerequisites" id="step2-initializethek8s-prerequisites"></a>

* An existing VPC and subnets meet K8S requirements. Before you deploy a Cluster for production use, we recommend that you have a good understanding of VPC and Subnet requirements. If you don't have a VPC and a Subnet, you can create them on the vServer's interface.
* The kubectl command line tool is installed on your device. Instances can be the same or at most a minor instance earlier or later than your Cluster's Kubernetes instance. For example, if your Cluster instance is 1.23.16, then you can use kubectl version 1.22, 1.23 or 1.24 with it.
* If you are using Kubernetes Cluster in the pfsense or Fortigate network layer, you need to Config MTU for FW types to 1450 according to the [MTU và “DF flag” best practice on GreenNode](https://docs.vngcloud.vn/vserver/vmarketplace/vmarketplace-giao-dien-cu/network-software-installation/pfsense-tren-hcm03/mtu-va-df-flag-best-practice-on-vng-cloud).
* The main IAM account have the create and describe K8S permissions. For more information, see [IAM for vServer](../../identity-and-access-management-iam-for-vserver/actions-resources-and-required-conditions-for-vserver-access-decentralization.md).

***

### **Create Kubernetes Cluster** <a href="#step2-initializethek8s-createkubernetescluster" id="step2-initializethek8s-createkubernetescluster"></a>

1. Open the vServer console at: [https://hcm-3.console.greennode.ai/vserver/container/cluster](https://hcm-3.console.greennode.ai/vserver/container/cluster).
2. Choose **Create a Kubernetes Cluster**
3. On the Cluster **basic configuration settings** pag&#x65;**,** enter the following fields:<br>
   * **Name** – Name for your Cluster. It must be unique in your GreenNode account. Names can only contain alphanumeric characters (a-z, A-Z, 0-9, '\_', '-'). Your input data length should be between 5 and 50. The name must be unique in the Region and GreenNode account you are creating the Cluster for.
   * **Kubernetes version** – The Kubernetes instance to use for your Cluster. We recommend choosing the latest version, unless you need an older version.
   * **Description** – Enter the information you want to note for the Cluster to create your own signature for easier management of them in the future.
   * **Number of Master nodes** – Enter the number of Master nodes for your Cluster, note that for non-HA (Highly available) you need to enter the number of 1 node and HA the number is 3 or 5 nodes.
   * **Number of Minion nodes** – Enter the number of Minion nodes for your Cluster, note that the number of nodes needs to be greater than or equal to 1 and less than or equal to 10.
4. Scroll down, you will see the **ETCD Storage** Configuration section:<br>
   * **ETCD Storage Information –** Choose an ETCD storage configuration for your Cluster under the **Small** or **Medium** plan.
5. In the **Instance type** section, select the appropriate configuration instance type for the Master node and Minion node according to your needs.
6. Set up the drives for the Kubernetes cluster at **Volume Settings:**
   * **Configure Boot Volume** – Parameters set by default by the system to optimize your Cluster
   * **Configure Docker Volume** – Choose the size and type of drive that suits your needs, the size of the Data Disk must be greater than or equal to 20 GB and not exceed 4000 GB.
7. In the **Network Settings** section, select values for the following fields:
   * **VPC** – Select an existing VPC that meets the requirements of K8S to create your Cluster. Before choosing a VPC, we recommend that you familiarize yourself with all the requirements and considerations in the VPC as well as the Subnet requirements and considerations. You cannot change which VPC you want to use after creating the Cluster. If no VPC is listed, you need to create one first. For more information, see [**Create a VPC**](https://hcm-3.console.greennode.ai/vserver/network/vpc).
   * **Network Type, Encapsulatio**n **Mode** are self-selected by default by the system and you cannot change them, however you can re-enter Calico CIDR parameters (note IP must be private and can be selected from the following options: (10.0.0.0 - 10.255.0.0 / 172.16.0.0 - 172.24.0.0 / 192.168.0.0)
   * **Subnets** – By default, all available subnets in the VPC specified in the previous field will be randomly selected in the first order, you can choose another Subnet, but only 1 can be selected.
   * **SSH keys** - to Import into Kubernetes during initialization (Click [**here** ](../../security/ssh-key-key-pairs.md)for instructions on creating SSH Key)
8. After filling in the necessary information to initialize K8S, it is necessary to review the summary of payment information at the **Summary** tab on the left side of the screen and detailed payment information for items in the Item list tab, if necessary or perform change. When you are satisfied select Create Kubernetes Cluster to confirm initialization of your Cluster. The Status displays **Creating** field when the Cluster is provisioned.
