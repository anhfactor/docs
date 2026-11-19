# Working VKS with Terraform

## What is Terraform? <a href="#terraform-la-gi" id="terraform-la-gi"></a>

Terraform is an open source infrastructure as code tool that allows users to manage their infrastructure easily and efficiently across different cloud platforms, such as GreenNode, AWS, Google Cloud and Azure. Terraform Server refers to the instance of the Terraform engine running on a specific server or machine. This is where infrastructure code is written and executed, allowing users to create, modify, and destroy resources on the cloud platform.

Terraform itself does not have a graphical user interface, instead users interact with it using a command line interface. Terraform requires a cloud provider account and key to be configured along with a Terraform configuration file to execute the infrastructure as code. Additionally, Terraform can operate in clustered environments where multiple users can collaborate on the same infrastructure codebase, making it a powerful and flexible tool for infrastructure management. cloud.

***

## Implementation steps <a href="#quanlyvcontainervoiterraform-dequanlyvcontainervoiterraform-bancanlamcacbuocsauday" id="quanlyvcontainervoiterraform-dequanlyvcontainervoiterraform-bancanlamcacbuocsauday"></a>

To initialize a Kubernetes Cluster using Terraform, you need to perform the following steps:

1. **Access the IAM Portal** here , create a Service Account with [VKS ](https://iam.console.greennode.ai/)**Full Access** authority . Specifically, at the IAM site, you can:
   * Select " **Create a Service Account** ", enter a name for the Service Account and click **Next Step** to assign permissions to the Service Account.
   * Find and select **Policy: VKSFullAccess** then click " **Create a Service Account** " to create a Service Account, **Policy: VKSFullAccess** is created by GreenNode, you cannot delete these policies.
   * After successful creation, you need to save **the Client\_ID** and **Secret\_Key** of the Service Account to perform the next step.
2. **Access the VKS Portal** here **, Activate** [the](https://vks.console.greennode.ai/overview) VKS service on the **Overview tab.** Please wait until we successfully create your VKS account.
3. **Install Terraform:**
   * Download and install Terraform for your operating system from [https://developer.hashicorp.com/terraform/install](https://developer.hashicorp.com/terraform/install) .
4. **Initialize Terraform configuration:**
   * Create a file `variable.tf`and declare Service Account information in this file.
   * Create a file `main.tf`and define the Kubernetes Cluster resources you want to create.

For example:

* The file `variable.tf:`you need to replace the Client ID and Client Secret created in step 1 in this file.

```
variable "client_id" {
  type = string
  default = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
}
variable "client_secret" {
  type = string
  default = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
}
```

***

* On the **main.tf** file , you need to be able to add resources to create a Cluster/ Node Group:
  * Create independent Cluster my-vks-cluster and Node Group my-nodegroup:

```
resource "vngcloud_vks_cluster" "primary" {
  name      = "my-cluster"
  cidr      = "172.16.0.0/16"
  vpc_id    = "net-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  subnet_id = "sub-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
}

resource "vngcloud_vks_cluster_node_group" "primary" {
  name= "my-nodegroup"
  ssh_key_id= "ssh-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  cluster_id= vngcloud_vks_cluster.primary.id
}
```

* Create Cluster with Default Node Group

```
resource "vngcloud_vks_cluster" "primary" {
  name      = "my-cluster"
  cidr      = "172.16.0.0/16"
  vpc_id    = "net-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  subnet_id = "sub-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  node_group {
    name= "my-nodegroup"
    ssh_key_id= "ssh-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  }
}
```

{% hint style="info" %}
**Attention:**

* We recommend that you create and manage Clusters and Node Groups as separate resources, as in the example below. This allows you to add or remove Node Groups without recreating the entire Cluster. If you declare Node Group Default directly in the vngcloud\_vks\_cluster resource, you cannot delete them without recreating the Cluster itself.
*   In the main.tf file, to successfully create a cluster with a node group, you must enter information in the following 4 fields:

    ```
      vpc_id    = "net-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
      subnet_id = "sub-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
      ssh_key_id= "ssh-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
    ```
{% endhint %}

**Example 1:**

Below is the main.tf file I used to initialize the Cluster with the following parameters:

* Cluster name: cluster-demo
* K8S Version: v1.29.1
* Mode: Public Cluster and Public Node Group
* Node Group name: nodegroup1
* Initial Node: 3
* Turn on AutoScaling: scale from 0 to 5 nodes

```
terraform {
  required_providers {
    vngcloud = {
      source  = "vngcloud/vngcloud"
      version = "1.2.2"
    }
  }
}

provider "vngcloud" {
  token_url        = "https://iamapis.vngcloud.vn/accounts-api/v2/auth/token"
  client_id        = var.client_id
  client_secret    = var.client_secret
  vserver_base_url = "https://hcm-3.api.vngcloud.vn/vserver/vserver-gateway"
  vlb_base_url     = "https://hcm-3.api.vngcloud.vn/vserver/vlb-gateway"
}

resource "vngcloud_vks_cluster" "primary" {
  name      = "cluster-demo"
  description = "Cluster create via terraform"
  version = "v1.29.1"
  cidr      = "172.16.0.0/16"
  enable_private_cluster = false
  network_type = "CALICO"
  vpc_id    = "net-70ef12d4-d619-43fc-88f0-1c1511683123"
  subnet_id = "sub-0725ef54-a32e-404c-96f2-34745239c123"
  enabled_load_balancer_plugin = true
  enabled_block_store_csi_plugin = true
}

resource "vngcloud_vks_cluster_node_group" "primary" {
  cluster_id = vngcloud_vks_cluster.primary.id
  name = "nodegroup1"
  num_nodes = 3
  auto_scale_config {
    min_size = 0
    max_size = 5
  }
  upgrade_config {
    strategy = "SURGE"
    max_surge = 1
    max_unavailable = 0
  }
  image_id = "img-108b3a77-ab58-4000-9b3e-190d0b4b07fc"
  flavor_id = "flav-9e88cfb4-ec31-4ad4-8ba5-243459f6d123"
  disk_size = 50
  disk_type = "vtype-61c3fc5b-f4e9-45b4-8957-8aa7b6029018"
  enable_private_nodes = false
  ssh_key_id= "ssh-f923c53c-cba7-4131-9f86-175d04ae2123"
  security_groups = ["secg-faf05344-fbd6-4f10-80a2-cda08d15ba5e"]
  labels = {
    "test" = "terraform"
  }
  taint {
    key    = "key1"
    value  = "value1"
    effect = "PreferNoSchedule"
  }
}
```

**Example 2**

Below is the main.tf file I used to initialize the Cluster with the following parameters:

* Cluster name: my-cluster
* K8S Version: v1.29.1
* Mode: Public Cluster and Private Node Group
* Node Group name: my-nodegroup
* Initial Node: 3 nodes
* Turn on AutoScaling: scale from 0 to 5 nodes

First, apply the main file according to the following structure:

```
terraform {
  required_providers {
    vngcloud = {
      source  = "vngcloud/vngcloud"
      version = "1.2.2"
    }
  }
}

provider "vngcloud" {
  token_url        = "https://iamapis.vngcloud.vn/accounts-api/v2/auth/token"
  client_id        = var.client_id
  client_secret    = var.client_secret
  vserver_base_url = "https://hcm-3.api.vngcloud.vn/vserver/vserver-gateway"
  vlb_base_url     = "https://hcm-3.api.vngcloud.vn/vserver/vlb-gateway"
}

resource "vngcloud_vks_cluster" "primary" {
  name      = "my-cluster"
  description = "VNGCLOUD uses terraform"
  version = "v1.29.1"
  cidr      = "172.16.0.0/16"
  enable_private_cluster = false
  network_type = "CALICO"
  vpc_id    = "net-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  subnet_id = "sub-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  enabled_load_balancer_plugin = true
  enabled_block_store_csi_plugin = true
}

resource "vngcloud_vks_cluster_node_group" "primary" {
  cluster_id= vngcloud_vks_cluster.primary.id
  name= "my-nodegroup"
  num_nodes = 3
  auto_scale_config {
    min_size = 0
    max_size = 5
  }
  upgrade_config {
    strategy = "SURGE"
    max_surge = 1
	max_unavailable = 0
  }
  image_id = "img-108b3a77-ab58-4000-9b3e-190d0b4b07fc"
  flavor_id = "flav-9e88cfb4-ec31-4ad4-8ba5-243459f6dc4b"
  disk_size = 20
  disk_type = "vtype-61c3fc5b-f4e9-45b4-8957-8aa7b6029018"
  enable_private_nodes = true
  ssh_key_id= "ssh-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  labels = {
    "mylabel" = "vngcloud"
  }
  taint {
    key    = "mykey"
    value  = "myvalue"
    effect = "PreferNoSchedule"
  }
}
```

Then, if you need to add Whitelist IP for Control Plane, add this field to the main.tf file and reapply this file:

```
terraform {
  required_providers {
    vngcloud = {
      source  = "vngcloud/vngcloud"
      version = "1.2.2"
    }
  }
}

provider "vngcloud" {
  token_url        = "https://iamapis.vngcloud.vn/accounts-api/v2/auth/token"
  client_id        = var.client_id
  client_secret    = var.client_secret
  vserver_base_url = "https://hcm-3.api.vngcloud.vn/vserver/vserver-gateway"
  vlb_base_url     = "https://hcm-3.api.vngcloud.vn/vserver/vlb-gateway"
}

resource "vngcloud_vks_cluster" "primary" {
  name      = "my-cluster"
  description = "VNGCLOUD uses terraform"
  version = "v1.29.1"
  cidr      = "172.16.0.0/16"
  white_list_node_cidr = "172.25.32.1/16"
  enable_private_cluster = false
  network_type = "CALICO"
  vpc_id    = "net-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  subnet_id = "sub-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  enabled_load_balancer_plugin = true
  enabled_block_store_csi_plugin = true
}

resource "vngcloud_vks_cluster_node_group" "primary" {
  cluster_id= vngcloud_vks_cluster.primary.id
  name= "my-nodegroup"
  num_nodes = 3
  auto_scale_config {
    min_size = 0
    max_size = 5
  }
  upgrade_config {
    strategy = "SURGE"
    max_surge = 1
	max_unavailable = 0
  }
  image_id = "img-108b3a77-ab58-4000-9b3e-190d0b4b07fc"
  flavor_id = "flav-9e88cfb4-ec31-4ad4-8ba5-243459f6dc4b"
  disk_size = 20
  disk_type = "vtype-61c3fc5b-f4e9-45b4-8957-8aa7b6029018"
  enable_private_nodes = true
  ssh_key_id= "ssh-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  labels = {
    "mylabel" = "vngcloud"
  }
  taint {
    key    = "mykey"
    value  = "myvalue"
    effect = "PreferNoSchedule"
  }
}
```

{% hint style="info" %}
**Attention:**

* To get the image\_id you want to use, you can access VKS Portal, select System Image menu and get the ID you want or get this information [here](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vks/reference/danh-sach-system-image-dang-ho-tro) .
* To get the flavor\_id you want to use for your Node group, please get the ID [here](https://docs.vngcloud.vn/vng-cloud-document/vn/vks/reference/node-flavors/danh-sach-flavor-tai-zone-hcm03-c) .
{% endhint %}

#### **Launch Terraform command** <a href="#quanlyvcontainervoiterraform-khoichayterraformcommand" id="quanlyvcontainervoiterraform-khoichayterraformcommand"></a>

* After completing the above information, run the command below:

```
terraform init
```

* Then, to see the changes that will be applied to the resources that terraform is managing, you can run:

```
terraform plan
```

* Finally, you choose to run the command line:

```
terraform apply
```

* Select **YES** to initiate Cluster and Node Group via Terraform

***

## **Check the newly created Cluster on the GreenNode Portal interface** <a href="#quanlyvcontainervoiterraform-kiemtracontainervuataotrengiaodienvngcloudportal" id="quanlyvcontainervoiterraform-kiemtracontainervuataotrengiaodienvngcloudportal"></a>

After successfully initializing Terraform, you can go to VKS Portal to view the newly created Cluster information.

See more about how to use Terraform to work with VKS [here](https://registry.terraform.io/providers/vngcloud/vngcloud/latest/docs/resources/vks\_cluster) .
