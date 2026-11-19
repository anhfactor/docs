# Extend volume with Linux OS

The volume (removable) of vServer can be easily expanded, without interrupting vServer.

Note: Volume Status must be AVAILABLE to expand the size. Volume cannot be reduced in size, it can only increase in size.

***

### Expanding Volume with Linux Operating System <a href="#morongvolumevoihedieuhanhlinux-morongvolumevoihedieuhanhlinux" id="morongvolumevoihedieuhanhlinux-morongvolumevoihedieuhanhlinux"></a>

Use the following guide to resize the Volume on the dashboard:

**Step 1: Increase Disk Capacity on the vServer Console**

1. Open the vServer console at: [https://hcm-3.console.greennode.ai/vserver/block-store/volumes](https://hcm-3.console.greennode.ai/vserver/block-store/volumes)
2. On the "VPC/Volumes" tab, select a volume and click "**Actions**."
3. Choose "**Expand.**"
4. Select the new size and IOPS for the volume. Note that the volume size must be at least 20 GB and can be up to 10,000 GB. You can check the additional cost in the right column.
5. Click "**Expand**" to complete the process.

After the process of increasing the capacity on the console is complete, the capacity of the drive inside the server needs to be increased.

**Step 2: Increase Disk Capacity Inside the Server**

**a. Check if the Disk Has Been Expanded:**

1. [Connect to the server.](../instance/connect-to-virtual-server/)
2. Type the command **`lsblk`**

In the following example output, the root drive (disk0) has two partitions (disk01 and disk02), while the additional drive (disk00) has no partitions.

```
sudo lsblk
NAME          MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
disk00        259:0    0  30G  0 disk /data
disk0         259:1    0  16G  0 disk
└─disk0p1     259:2    0   8G  0 part /
└─disk0p2     259:3    0   1M  0 part
```

If the disk has one partition, proceed with the process from the next step (2b). If the disk has no partitions, skip steps 2b, 2c, and 2d, and continue with the process from step 3.

3. Check if the partition needs to be expanded. In the `lsblk` output, compare the partition size and the original disk size. If the partition size is smaller than the disk size, proceed to the next step. If the partition size equals the disk size, the partition cannot be expanded.

**b. Increase Disk Capacity Using the Command:**

1. Expand the partition. Use the **`growpart`** command and specify the partition to expand. Type the command: growpart \<disk> \<partition> .

Example: To expand the partition named disk0p1, use the following command:

Important: Note the space between the device name (disk0) and the partition number (1).

```
sudo growpart /dev/disk0 1
```

2. Verify that the partition has been expanded. Use the **`lsblk`** command. The partition size should now match the disk size.

```
sudo lsblk
NAME          MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
disk00        259:0    0  30G  0 disk /data
disk0         259:1    0  16G  0 disk
└─disk0p1     259:2    0  16G  0 part /
└─disk0p2     259:3    0   1M  0 part
```

**c. Expand the File System**

1. Get the name, size, type, and mount point for the file system you need to expand. Use the **`df -hT`** command.\
   The following example output shows that the file system /dev/disk0p1 is 8 GB in size, its type is xfs, and its mount point is /.

```
df -hT
Filesystem      Type  Size  Used Avail Use% Mounted on
/dev/disk0p1    xfs   8.0G  1.6G  6.5G  20% /
/dev/disk00     xfs   8.0G   33M  8.0G   1% /data
```

2.  The commands to expand the file system vary depending on the file system type. Choose the correct command below based on the file system type noted in the previous step.

    **\[XFS File System]** Use the **`xfs_growfs`** command and specify the mount point of the file system noted in the previous step.

```
sudo xfs_growfs -d /
```

Hint:

* `xfs_grofs: /data` is not a mounted XFS file system Indicates that you have specified the wrong mount point or the file system is not XFS. To verify the mount point and file system type, use the `df -hT` command.
* Data size unchanged, skipping: Indicates that the file system has fully expanded to the drive size. If the drive has no partitions, confirm that the drive modification was successful. If the drive has partitions, ensure that the partition has been expanded as described in step b.

**\[Ext4 File System]** Use the **`resize2fs`** command and specify the name of the file system noted in the previous step.

```
sudo resize2fs /dev/disk0p1
```

3. Verify that the file system has been expanded. Use the `df -hT` command and confirm that the file system size matches the disk size.
