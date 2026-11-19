# Extend Volume with Windows OS

A detachable volume of the vServer can be easily expanded without interrupting the vServer. Note: The volume cannot be reduced in size; it can only be increased.

## Extend Volume with Windows OS

**Use the following guide to resize the Volume on the console:**

**Step 1: Increase Disk Capacity on the vServer Console**

1. Open the vServer controller at: [vServer Console](https://hcm-3.console.greennode.ai/vserver/block-store/volumes)[https://hcm-3.console.greennode.ai/vserver/block-store/volumes](https://hcm-3.console.greennode.ai/vserver/block-store/volumes).
2. On the "VPC/Volumes" tab, select a volume and click "**Actions**."
3. Choose "**Expand**."
4. Select the new size and IOPS for the volume. Note that the volume size must be at least 20 GB and can be up to 10,000 GB. You can check the additional cost in the right column.
5. Click "**Expand**" to complete the process.

After the process of increasing the capacity on the console is complete, use the Windows Disk Management utility or PowerShell to extend the drive size to the new disk size. You can start resizing the file system immediately after expanding it on the vServer console.

**Step 2: Expand the Windows File System Using Disk Management Utility**

Use the following guide to Expand  the Windows File System.

1. To expand the file system using **Disk Management.** Before expanding a file system that contains valuable data, it is best to create a snapshot of the disk containing it in case you need to revert your changes.
2. Log in to your Windows instance using Remote Desktop.
3. In the **Run** dialog box, type **`diskmgmt.msc`** and press Enter. The **Disk Management** utility will open.

<figure><img src="https://docs.vngcloud.vn/download/attachments/59804681/image2023-6-27_16-12-43.png?version=1&#x26;modificationDate=1687857164000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

4. On the **Disk Management** menu, select "**Action**," then "**Rescan Disks**."
5. Open the context menu (right-click) for the expanded disk and select "**Extend Volume**."

**Note:**

* "Extend Volume" may be disabled (grayed out) if:
  * The unallocated space is not contiguous to the disk. The unallocated space must be contiguous to the right side of the disk you want to extend.
  * The disk uses the Master Boot Record (MBR) partition style and is already 2TB in size. Disks using MBR cannot exceed 2TB.

<figure><img src="https://docs.vngcloud.vn/download/attachments/59804681/image2023-6-27_16-16-1.png?version=1&#x26;modificationDate=1687857362000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

6. In the Extend Volume Wizard, select "Next." For "Select the amount of space in MB," enter the number of megabytes to extend the volume. Generally, you specify the maximum available space. The highlighted text under "Selected" is the added space, not the final size the disk will have. Complete the wizard.

<figure><img src="https://docs.vngcloud.vn/download/attachments/59804681/image2023-6-27_16-18-53.png?version=1&#x26;modificationDate=1687857534000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

**Step 2: Expand the Windows File System Using PowerShell**

**To expand the file system using PowerShell:**

1. Before expanding a file system that contains valuable data, it is best to create a snapshot of the disk containing it in case you need to revert your changes.
2. Log in to your Windows instance using Remote Desktop.
3. Run PowerShell as an administrator.
4. Run the `Get-Partition` command. PowerShell returns the partition number, drive letter, offset, size, and type for each partition. Note the drive letter of the partition to be extended.
5. Run the following command to rescan the disks:

| `"rescan"` `\| diskpart` |
| ------------------------ |

6. Run the following command, using the drive letter noted in step 4 instead of `<drive letter>`. PowerShell returns the minimum and maximum allowed partition sizes in bytes:

```
Get-PartitionSupportedSize -DriveLetter <drive-letter>
```

7. To extend the partition to a specific size, run the following command, entering the new disk size instead of `<size>`. You can enter the size in KB, MB, and GB; for example, 50GB:

```
Resize-Partition -DriveLetter <drive-letter> -Size <size>
```

8. To extend the partition to the maximum available size, run the following command:

```
Resize-Partition -DriveLetter <drive-letter> -Size $(Get-PartitionSupportedSize -DriveLetter <drive-letter>).SizeMax
```

\
**The following PowerShell commands show the complete command line and response to extend the file system to a specific size:**

<figure><img src="https://docs.vngcloud.vn/download/attachments/59804681/image2023-6-27_16-34-14.png?version=1&#x26;modificationDate=1687858455000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

**The following PowerShell commands show the complete command line and response to extend the file system to the maximum available size:**

<figure><img src="https://docs.vngcloud.vn/download/attachments/59804681/image2023-6-27_16-34-51.png?version=1&#x26;modificationDate=1687858492000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
