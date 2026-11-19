# Manage vLB with Terraform

#### **To manage vServer with Terraform, you need to do the following steps:** <a href="#managevlbwithterraform-tomanagevserverwithterraform-youneedtodothefollowingsteps" id="managevlbwithterraform-tomanagevserverwithterraform-youneedtodothefollowingsteps"></a>

**Step 1**: Install Terraform CLI as instructed [here](install-terraform.md)

**Step 2**: To be able to manage vServer with Terraform, you need to create a Service account from the Root account on the IAM homepage (see instructions on how to create a Service account and use [IAM here](../../../identity-and-access-management-iam/)), in this case you want to create a Load Balancer with Terraform requires the following (Policy) permissions:

* CreateLoadBalancer
* GetLoadBalancer

or you can grant **vvLBFullAccess** permission (should have **vLBReadOnlyAccess** permission to get resource information after creation). For more information on how to assign permissions to each Resource, the corresponding Action at [{IAM Authorization Page}](../identity-and-access-management-iam-for-vserver/actions-resources-and-required-conditions-for-vserver-access-decentralization.md).

> **Note:** Each different resource management action will require different permissions, so it's essential to set up a reasonable set of permissions that fit your business needs.

**Step 3**: Create a folder containing the terraform file and download the example from the GreenNode repo at [here](https://github.com/vngcloud/terraform-provider-vngcloud/tree/main/examples).

After downloading the Example folder to the computer, the user opens the file [variable.tf](https://github.com/vngcloud/terraform-provider-vngcloud/blob/main/examples/variable.tf) (under the path **terraform-provider-vngcloud/examples/**[**variable.tf**](http://variable.tf/)), then changes the necessary information as follows:

* **Client\_id:** Get at IAM homepage/ Service account - Service account Detail - **Tab Security credentials**
* **Client\_secret:** Obtained when initializing Service account at IAM homepage or can be reset at IAM homepage/ Service account - Service account Detail - **Tab Security credentials**

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

```
variable "client_id" {  
type = string  
default = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
}
variable "client_secret" {  
type = string  
default = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
}
```

**Step 4:** Check the file [**main.tf**](https://github.com/vngcloud/terraform-provider-vngcloud/blob/main/examples/main.tf) information again (follow the path examples/ [main.tf](http://main.tf/)), in this case you need to delete the lines below:

* _module "vserver" {source = "./modules/vng-cloud-vserver"}_
* module "k8s" {source = "./modules/vng-cloud-k8s" }
* _just keep:_
* _module "vlb" { source = "./modules/vng-cloud-vlb" }_

```
terraform {  
required_providers {    
vngcloud = {      
source  = "vngcloud/vngcloud"      
version = "1.1.0"    
}
} 
provider "vngcloud" {  
token_url        = "https://iamapis.vngcloud.vn/accounts-api/v2/auth/token"  
client_id        = var.client_id  
client_secret    = var.client_secret  
vserver_base_url = "https://hcm-3.api.vngcloud.vn/vserver/vserver-gateway"  
vlb_base_url = "https://hcm-3.api.vngcloud.vn/vserver/vlb-gateway"}
module "vlb" {  
source = "./modules/vng-cloud-vlb" }
}
```

\
**Step 5:** Then go to the directory **vng-cloud-vserver/ examples/ modules/ vng-cloud-k8s/**, and open the [**variable/tf**](https://github.com/vngcloud/terraform-provider-vngcloud/tree/main/examples/modules/vng-cloud-vlb) **file**:

* **project\_id**: your project information, you can get it at [{Limit Tab}](https://hcm-3.console.greennode.ai/vserver/limit) on vServer Portal, For example: **pro-462803f3-6858-466f-bf05-df2b33faa360**:

<figure><img src="../../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **subnet\_id**: specify the subnet id that vServer will be created on, you can get it from [{VPC Tab}](https://hcm-3.console.greennode.ai/vserver/network/vpc), if you haven't initialized any subnet you can see the instructions at [{Subnet creation page}](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648039):

<figure><img src="../../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

```
variable "project_id" {  
type    = string  
default = "pro-462803f3-6858-466f-bf05-df2b33faa360"
}
variable "subnet_id" {  
type    = string  
default = "sub-5f101cba-7ce0-4084-8576-06b8dbfb298a"}
```

**Step 6**: Check the file [**main.tf**](https://github.com/vngcloud/terraform-provider-vngcloud/blob/main/examples/modules/vng-cloud-vlb/main.tf) information (follow the path _**erraform-provider-vngcloud/examples/modules/vng-cloud-k8s/**_[_**main.tf**_](http://main.tf/)), in the file we have some commands available: **Create Load Balancer**, **Listener, Policy, Pool,** in this case to Create K8S you just need to leave the **Create Load Balancer** resource follow the instructions below:

```
data "vngcloud_vlb_lb_packages" "lb_packages" {  
project_id = var.project_id
} 
resource "vngcloud_vlb_load_balancer" "example"{  
project_id = var.project_id  
name       = "example_vlb"  
package_id =  data.vngcloud_vlb_lb_packages.lb_packages.packages[0].uuid  
scheme     = "Internet"  
subnet_id  = var.subnet_id  
type       = "Layer 7"
}
```

**Step 7**: Launch the terraform command

* After completing the above information, in order for terraform to initialize and download the GreenNode provider and set up the necessary information, run the command below, note that when running, you need to stand in the directory terraform-provider-vngcloud/ [examples/](https://github.com/vngcloud/terraform-provider-vngcloud/tree/main/examples) :

| `terraform init` |
| ---------------- |

The system will return the following results:

```
vnglab:vngcloud cbr09$ terraform init 

Initializing the backend... 

Initializing provider plugins...
- Finding vngcloud/vngcloud versions matching "0.0.5"...
- Installing vngcloud/vngcloud v0.0.5...
- Installed vngcloud/vngcloud v0.0.5 (self-signed, key ID A6A27B3126EF15EB) 

Partner and community providers are signed by their developers.
If you'd like to know more about provider signing, you can read about it here:
https://www.terraform.io/docs/cli/plugins/signing.html 

Terraform has created a lock file .terraform.lock.hcl to record the providerselections it made above. Include this file in your version control repositoryso that Terraform can guarantee to make the same selections by default whenyou run "terraform init" in the future. 

Terraform has been successfully initialized! 

You may now begin working with Terraform. Try running "terraform plan" to seeany changes that are required for your infrastructure. All Terraform commandsshould now work. 

If you ever set or change modules or backend configuration for Terraform,rerun this command to reinitialize your working directory. If you forget, othercommands will detect it and remind you to do so if necessary.
```

Then, to see what changes will be applied to the resources that terraform is managing, you can run:

| `terraform plan` |
| ---------------- |

Finally you choose to run the command line:

| `terraform apply` |
| ----------------- |

and select **YES** to perform vServer initialization via Terraform

<br>

**Step 8**: You can go to the Portal to see the Load Balancer being initialized from Terraform:
