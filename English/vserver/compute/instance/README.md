# Instance

An instance is a virtual server in the cloud that includes basic components such as vCPUs, memory, an operating system (OS), network configurations, and volumes. You can use management tools provided by GreenNode such as the Portal and API to create and manage vServer instances. You can also resize the capabilities (such as compute and storage capabilities) of your instances as your requirements change.

<figure><img src="https://docs.vngcloud.vn/download/attachments/49648003/image2022-11-14_13-49-32.png?version=1&#x26;modificationDate=1669016135000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

### **Basic configurations for instance** <a href="#instance-basicconfigurationsforinstance" id="instance-basicconfigurationsforinstance"></a>

You can launch different types of instances from a single Image. An _instance type_ essentially determines the hardware of the host computer used for your instance. Each instance type offers different compute and memory capabilities. Select an instance type based on the amount of memory and computing power that you need for the application or software that you plan to run on the instance.&#x20;

Images contain the required information necessary to run ECS instances, such as OSs and initialization data of applications. GreenNode provides ready-to-use OS images for Windows Server and several Linux OSs. You can also create or import your own custom images to save time in making repeated configurations. In addition, image providers provide images pre-installed with a variety of runtime environments and software applications in Marketplace. GreenNode Marketplace images are suitable for specific scenarios such as website building, application development, and visualized management. You can conveniently select Marketplace images based on their purpose.

Instances use their attached boot volume and data volumes for storage. Each instance must have a boot volume attached. The first time the instance starts, the OS is installed and instance configurations are initialized based on the image on the boot volume. If you want your instances to have more storage space, you can resize their attached volumes or attach more volumes after the instances are created.

Business data is an important asset. To ensure that your data remains available, we recommend that you back up your data on a regular basis. You can create snapshots of volumes to back up data.

In addition to these basic configurations, you can customize VPC network configurations, security groups, OS configurations, and custom configurations for instances.&#x20;

