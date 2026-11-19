# Resize Instance

If the configurations of an instance do not meet your business needs, you can change the configurations, including the vCPUs and memory by changing the flavor of instance.

## Change flavor or instance types <a href="#resizeinstance-changeflavororinstancetypes" id="resizeinstance-changeflavororinstancetypes"></a>

A flavor is a predefined combination of vCPUs and memory. When you change the flavor of an instance, you must select flavor from the predefined list. The number of vCPUs or memory size cannot be customed individually.

The instance must be stopped before resizing. This process only change the resource allocate for the instance including vCPU and memory, if you want to change for volume you must go to proccess extending volume.

The price and its calculation method of new flavor are displayed on the right panel in the GreenNode console when you select the new flavor for an instance.

## Procedure <a href="#resizeinstance-procedure" id="resizeinstance-procedure"></a>

Before you can change the flavor of an instance, you must identify the flavor and learn about the flavor such as Instance Family, CPU Platform… See more at {flavor page}

1. Log on to the GreenNode Portal and navigate to vServer service
2. In the **Instances** page, find the instance to be resized, ensure its status is **Stopped**. Expand the **Menu** list on right-side, select **Resize**.
3. Select new flavor that meet your requirement.
4. You can check the new price or the refund in case of down-resize, then click **Resize Server** to submit.
5. Waiting for status of instance become Stop again.

<br>
