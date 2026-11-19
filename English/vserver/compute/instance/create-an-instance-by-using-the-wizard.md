# Create an instance by using the wizard

Create a virtual server using the initialization process on GreenNode

Procedure: [Getting started](../getting-started/)

The GreenNode portal provides a wizard for creating instances. This wizard lists all configuration information used to create an instance and guides you through creating an instance.

### **Preparations** <a href="#createaninstancebyusingthewizard-preparations" id="createaninstancebyusingthewizard-preparations"></a>

Create an GreenNode account and complete the verification of account information.

You will need some credits to purchase later.

### **Complete the setting in Basic configuration** <a href="#createaninstancebyusingthewizard-completethesettinginbasicconfiguration" id="createaninstancebyusingthewizard-completethesettinginbasicconfiguration"></a>

In the Basic Configurations step, you can configure the basic parameters and resources including the instance name and system image. The instance name must be between 5 and 50 characters in length and contains only these letters: a-z, A-Z, 0-9, '-', '\_'

You must select an Images that contain the information required to run instances. The following table describes the image types:

| **Image type**          | **Description**                                                                                                                                                                                                     | **Notes or References**                                           |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| OS Image / Public Image | Public images are base images provided by GreenNode that are fully tested. These images include Windows Server OS images and mainstream Linux OS images.                                                            | [{Image Page}](../image.md)                                       |
| My Image / Custom Image | Customer can create or import custom images. Custom images contain initial system environments, application environments, and software configurations. This eliminates the need for repeated manual configurations. | {Custom image Page}                                               |
| GPU Image               | Image contains NVIDIA driver or NVIDIA Software that are tested by GreenNode. These images include Windows OS and Ubuntu OS images                                                                                  | Customer can select public image then install GPU driver if need. |

Select an Instance Type or Flavor that describes the resource CPU, Memory matching your requirement. You can follow the summary billing on the right panel.

### **Complete the setting in Volume configurations** <a href="#createaninstancebyusingthewizard-completethesettinginvolumeconfigurations" id="createaninstancebyusingthewizard-completethesettinginvolumeconfigurations"></a>

Instances provide storage capabilities based on the system volumes, data volumes that are attached to the instances.

Block Storage volumes are fully backed by SSD disk.

The IOPS configuration is the performance quota of volume. Base on your application, you must select the right quota to archive the best experience.

You can encrypt the volumes to meet the requirements of scenarios such as data security and regulatory compliance. Encryption Key is securely managed by the GreenNode KMS system and independent this instance OS workload.

You can add more data volumes to instance to increase the capability at this step or later.

### **Complete the setting in Network configurations** <a href="#createaninstancebyusingthewizard-completethesettinginnetworkconfigurations" id="createaninstancebyusingthewizard-completethesettinginnetworkconfigurations"></a>

You can make network and security group configurations to allow the instance to communicate with the Internet and other GreenNode resources in the VPC network.

A VPC is an isolated network dedicated for your use. You have full control over your VPC. For example, you can specify a private subnet and configure route tables and network policy for the VPC. See more at [{VPC Page}](../vpc/virtual-private-cloud-vpc.md).

If you have not created a VPC in the availability zone, the system creates a default VPC and subnet to minimize the process.

#### Floating Setting: Assign a public IP address to the instance <a href="#createaninstancebyusingthewizard-floatingsetting-assignapublicipaddresstotheinstance" id="createaninstancebyusingthewizard-floatingsetting-assignapublicipaddresstotheinstance"></a>

To enable the instance to access the Internet, you must assign a public IP address to the instance. FIP will be NAT 1:1 with your instance’s private IP (in subnet belong to VPC network) and it’s invisible to your instance’s OS view.

You can select check box Floating IP when you create an instance to have a public IP address automatically assigned to the instance. Alternatively, you can assign FIP after an instance is created to provide Internet access for the instance. You can purchase FIP to reserved an unchanged FIP when stop instance.

#### Select security group <a href="#createaninstancebyusingthewizard-selectsecuritygroup" id="createaninstancebyusingthewizard-selectsecuritygroup"></a>

A security group is a virtual firewall that is used to control the inbound and outbound traffic of instances in the security group.

If you do not want to configure security group-related parameters when you create an instance, you can skip the step. The system creates a default security group. The default security group allows inbound traffic over SSH port 234, Remote Desktop Protocol (RDP) port 3490, and Internet Control Message Protocol (ICMP). You can modify the security group configurations after the security group is created.

#### Authentication <a href="#createaninstancebyusingthewizard-authentication" id="createaninstancebyusingthewizard-authentication"></a>

It’s recommended to use SSH Key to access your Linux Instance. You can create new SSH Key pair or import your public key to GreenNode. See more at [{SSH key page}](../security/ssh-key-key-pairs.md).

Additionally, you can provide your manual username and password that will be injected to you instances in order to access.

### **Other settings** <a href="#createaninstancebyusingthewizard-othersettings" id="createaninstancebyusingthewizard-othersettings"></a>

You can select the server group info for request an affinity or anti-affinity policy for your instance’s location when provisioning.

### **Result** <a href="#createaninstancebyusingthewizard-result" id="createaninstancebyusingthewizard-result"></a>

After the instance is created, go to the Instance page to check the state of the instance. When the state of the instance changes to **Running**, the instance can be accessed. You will receive an email with credential.

<br>
