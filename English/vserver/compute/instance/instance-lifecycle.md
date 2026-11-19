# Instance Lifecycle

An instance transitions through different states from the moment it is created to the moment it is terminated.

<figure><img src="https://docs.vngcloud.vn/download/attachments/49648009/image2022-11-14_13-22-56.png?version=1&#x26;modificationDate=1669016497000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

### **Provisioning** <a href="#instancelifecycle-provisioning" id="instancelifecycle-provisioning"></a>

In this stage, the instances are prepared to enter the running state. The computing resources are allocated & configured at this stage.

In GreenNode, the instances have a pending state. Such instance states are launched for the first time or started after the stopping stage.

### **Running** <a href="#instancelifecycle-running" id="instancelifecycle-running"></a>

In this stage, the instances are running and ready for use. You can start hosting the workloads on the instances.

You are billed for the instances in the running stage.

### **Shutting Down** <a href="#instancelifecycle-shuttingdown" id="instancelifecycle-shuttingdown"></a>

In some cases, the instance may fail a status check or not run as expected. In this stage, the instance is prepared to shut down.

You can initiate the shutting down to fix the instance problem & restart the service.

When it enters the shutting down state, you can modify specific attributes of the instance.

### **Terminated** <a href="#instancelifecycle-terminated" id="instancelifecycle-terminated"></a>

You can delete an instance when you no longer require it. It is called the termination state of the instance.

You change the status of the instance to shutting down or terminated. As soon as the instance is terminated, you stop incurring charges.

When an instance terminates, the data on any instance store volumes are deleted.

You can use termination protection for your instances. It prevents the instances from being terminated accidentally.
