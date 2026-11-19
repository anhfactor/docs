# Create Snapshots

The GreenNode Snapshot service is a robust data backup solution that empowers you to create consistent snapshots of your system or data disks instantly, without the need for any additional agents. These snapshots serve as valuable tools for data backup, disaster recovery, and system rollback. Before restoring a disk, modifying critical system files, or changing the operating system of a server, you can create a disk snapshot to enhance fault tolerance.

You have the ability to create point-in-time snapshots of your volume, which serve as a baseline for creating new volumes or securing your data through backups. In case you set up periodic snapshots for a specific volume, these snapshots will work incrementally, meaning that each new snapshot records only the blocks of data that have changed since the previous snapshot was taken.

The snapshot process operates asynchronously. Even though the point-in-time snapshot is started immediately, its status remains pending until the entire snapshot process is completed. Completing this process requires transferring all modified data blocks to the original volume. For important initial snapshots or subsequent snapshots with significant changes, this operation can take several hours. It is important that during this period of activity, the snapshot in progress remains unaffected by the read and write operations occurring on the volume.



***

### Prerequisites <a href="#taosnapshot-dieukientienquyet" id="taosnapshot-dieukientienquyet"></a>

* Snapshot must be activated. For more information, please refer to [Activate Snapshot](activate-snapshot.md).
* The disk you want to take a snapshot of is in either the In Use or Not Attached state. Please note the following:
  * If the disk is in the In Use state, ensure that the version the disk is attached to is either Running or Stopped.
  * If the disk is in the Not Attached state, make sure the disk has been attached to a Server at some point. Snapshots cannot be created for cloud disks that have never been attached to a Server."

***

### **Create a Snapshot for a Volume on the Dashboard** <a href="#taosnapshot-taosnapshotchovolumetrenbangdieukhien" id="taosnapshot-taosnapshotchovolumetrenbangdieukhien"></a>

1. Open the vServer control panel at [https://hcm-3.console.greennode.ai/vserver/block-store/snapshot](https://hcm-3.console.greennode.ai/vserver/block-store/snapshot).
2. Select **Create Snapshot**
3. On the Create Snapshot information entry page, you need to complete the following items:
   * **Snapshot Type** – Choose the object you want to create a Snapshot for, according to Volume.&#x20;
   * **Snapshot Name** – Name for your Snapshot. The name can only contain letters and numbers (a-z, A-Z, 0-9, '\_', '-'). Your input data length must be from 5 to 50 characters. The name must be unique within the Region and GreenNode account you are creating the Snapshot for.
   * **Snapshot Settings**:<br>
     * **Volume ID:** Select the Volume you want to create a Snapshot for by ID
     * **Description** – Enter a note for the Snapshot
     * **Retention Time:** Choose the retention time for the Snapshot, you can choose to retain the Snapshot permanently or for the number of days you enter
4. After filling in the necessary information, select **Create Snapshot** to confirm initialization. The Status field will display **Creating** when the Snapshot is being created. This action will prompt the cloud infrastructure to begin collecting data from the selected disk.

***

### **Create a Snapshot for a Server on the Dashboard** <a href="#taosnapshot-taosnapshotchoservertrenbangdieukhien" id="taosnapshot-taosnapshotchoservertrenbangdieukhien"></a>

1. Open the vServer control panel at [https://hcm-3.console.greennode.ai/vserver/block-store/snapshot](https://hcm-3.console.greennode.ai/vserver/block-store/snapshot).
2. Select Create **Snapshot**
3. On the Create Snapshot information entry page, you need to complete the following items:
   * **Snapshot Type** – Choose the object you want to create a Snapshot for, according to the Server. Selecting by Server implies that you will create a Snapshot attached to the chosen Server.
   * **Snapshot Name** – Name for your Snapshot. The name can only contain letters and numbers (a-z, A-Z, 0-9, '\_', '-'). Your input data length must be from 5 to 50 characters. The name must be unique within the Region and GreenNode account you are creating the Snapshot for.
   * **Snapshot Settings:**<br>
     * **Volume ID**: Select the Volume you want to create a Snapshot for by ID
     * **Description** – Enter a note for the Snapshot
     * **Retention Time**: Choose the retention time for the Snapshot, you can choose to retain the Snapshot permanently or for the number of days you enter
4. After filling in the necessary information, select **Create Snapshot** to confirm initialization. The Status field will display **Creating** when the Snapshot is being created. This action will prompt the cloud infrastructure to begin collecting data from the selected disk.

***

### **Snapshot Encryption** <a href="#taosnapshot-mahoasnapshot" id="taosnapshot-mahoasnapshot"></a>

Snapshot encryption ensures the security of your data in cloud environments. When snapshots are created from encrypted disks, they are automatically encrypted, safeguarding the data during storage and transmission. This encryption mechanism provides comprehensive protection for both the disk and any related snapshots. For further details, please refer to the documentation on [Volume encryption.](../instance/compute-encryption-volume/)&#x20;

<br>
