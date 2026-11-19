# Volume

Volume is an object in a virtualized environment responsible for providing block storage to servers with high availability and performance. You can use Volumes to store data and applications, or you can attach one or more Volumes to a Server while creating the Server or later while the Server is running. You can detach a volume from a Server and attach to another Server.

## Volume basics <a href="#volume-volumebasics" id="volume-volumebasics"></a>

When you use volumes, note that:

* Maximum size for single volume depend on the volume type.
* A root volume is always attached to its owner VM instance and cannot be detached.
* A data volume can be attached to or detached from different VM instances.
* You can set QoS for volumes by choosing Volume Type to limit the disk bandwidth and IOPS
* You can enable data encryption at provisioning volume to protect data. GreenNode supports aes-xts-plain64 algorithm.

## Work with volume <a href="#volume-workwithvolume" id="volume-workwithvolume"></a>

#### Create volume <a href="#volume-createvolume" id="volume-createvolume"></a>

There are two type of volume usage, boot volume and data volume. For boot volume, you can provide information of volume when create VM instance. Data volume can be created independently from Volume management view.

1. Go to GreenNode Portal console, navigate to Volume page
2. Create a data volume and provide information such as name, data size, IOPS quota and encryption option.
3. You can check the price of volume on the right panel, then click **Create**.

#### Attach volume to VM Instance <a href="#volume-attachvolumetovminstance" id="volume-attachvolumetovminstance"></a>

1. Go to GreenNode Portal console, navigate to Volume page
2. Select Data volume to attach, expand menu action on the right side, select **Attach.**
3. Select VM instance to attach, then go to VM instance to operate your volume like create partition, format and mount.

#### Detach volume from VM Instance <a href="#volume-detachvolumefromvminstance" id="volume-detachvolumefromvminstance"></a>

1. Go to GreenNode Portal console, navigate to Volume page
2. Select Data volume to detach, expand menu action on the right side, select **Detach.**
3. Select VM instance to detach.

#### Change volume QoS (Volume Type) - TBA <a href="#volume-changevolumeqos-volumetype-tba" id="volume-changevolumeqos-volumetype-tba"></a>

#### Delete volume <a href="#volume-deletevolume" id="volume-deletevolume"></a>

Only volume with status Available can be deleted.

1. Go to GreenNode Portal console, navigate to Volume page
2. Select Data volume to delete, expand menu action on the right side, select **Delete.**

<br>
