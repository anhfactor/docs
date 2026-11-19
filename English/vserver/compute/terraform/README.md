# Terraform

### **What is Terraform?** <a href="#terraform-whatisterraform" id="terraform-whatisterraform"></a>

Terraform is an open source infrastructure as a code engine that allows users to easily and efficiently manage their infrastructure across different cloud platforms, such as GreenNode, AWS, Google Cloud and Azure. Terraform server refers to the instance of the Terraform engine running on a particular server or machine. This is where the infrastructure code is written and executed, allowing users to create, modify, and destroy resources in the cloud.

Terraform itself does not have a graphical user interface, instead the user interacts with it using a command line interface. Terraform requires a configured cloud provider account and key along with a Terraform configuration file to execute the infrastructure as code. Additionally, Terraform can operate in a team environment where multiple users can collaborate on the same infrastructure codebase, making it a powerful and flexible tool for infrastructure management. cloud.

<figure><img src="/broken/files/OhmM04HV6D0x2xJaXGRb" alt=""><figcaption></figcaption></figure>

<br>

### **What benefits does Terraform bring?** <a href="#terraform-whatbenefitsdoesterraformbring" id="terraform-whatbenefitsdoesterraformbring"></a>

* Improve accuracy, save implementation time: With one-time and reusable infrastructure descriptor file definitions, Terraform helps us automate infrastructure construction. They ensure the infrastructure is built correctly eliminating the mistakes that can be made by doing it manually. Infrastructure built by Terraform also ensures consistency between environments because it is built from the same file. This will eliminate discrepancies between development, test, and production environments. Ensure accurate and consistent test results across environments. Infrastructure construction time will be shortened because manual steps have now been replaced by automated commands. When we need to build the infrastructure for a new environment or change the infrastructure for all existing environments, we just need to run the description file with Terraform. All changes will go as you want, no need to recreate from scratch or modify the infrastructure in all environments to be consistent.
* Change version management: You can track the development and change of the infrastructure by using version tracking tools for the infrastructure descriptor file. From there we can easily and quickly modify the infrastructure to an old version if the change process has problems.
* Documenting infrastructure information: According to the traditional process with manual infrastructure management, to support the development and operation of the system, we need to develop a document describing the information. and implementation steps, but when using Terraform, we do not need to build those documents because the necessary information is already shown in the HCL source code file used to build the infrastructure.\
  Support collaboration, reuse: Because the infrastructure is managed using the HCL programming language to describe, programmers can easily collaborate and work together to build together. Programmers can also create common modules to reuse for future projects, making the process of building infrastructure for a new system faster and simpler instead of having to do it all over again. everything from scratch.\
  Working with multiple Cloud Providers simultaneously: We can use Terraform to work with many different compute service providers such as: GreenNode, Amazon Web Service, Microsoft Azure, Google Cloud Platform, Kubernetes, VMWare. ..Using Terraform to work with many different services makes managing resources on many other platforms at the same time easier and more convenient.

***
