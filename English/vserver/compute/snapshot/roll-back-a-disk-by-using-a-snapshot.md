# Roll back a disk by using a snapshot

You can restore virtual disks or virtual servers using previously created snapshots. The content below describes how to restore a virtual disk using snapshots.

Using snapshots allows you to quickly restore data and systems after incidents, reducing system downtime. It's a safe way to back up your important data, ensuring that you can recover data and disks as needed, such as in the case of hardware failures, software errors, or accidental data deletion. Compared to reconfiguring and restoring systems from scratch, using snapshots saves significant time and effort.

***

### **Risks:** <a href="#khoiphucodiaaobangbansnapshot-ruiro" id="khoiphucodiaaobangbansnapshot-ruiro"></a>

* Corrupted Data: If you use a corrupted or damaged snapshot, restoration may result in incorrect or corrupted data. This is particularly important if you don't check the snapshot before using it.
* Snapshot Creation Time: If you create snapshots irregularly or infrequently, you may lose important data if an incident occurs between snapshot creations. The time gap between snapshots also affects data recovery capabilities.
* Storage Costs: Maintaining multiple snapshots can incur significant storage costs. You need to consider the balance between the benefits of storing multiple snapshots and the corresponding costs.
* Careful Snapshot Management: Managing snapshots requires careful attention to ensure you don't accidentally delete important backups or maintain too many unnecessary backups.

Using snapshots to restore virtual disks has many important benefits, but it also comes with risks that need careful consideration and management. It's important to implement security measures and verify the integrity of the snapshot before performing data recovery.

***

Notes:

You can only restore a virtual disk with a Snapshot of the Data Volume.

### **Restoring a virtual disk with a Snapshot on the Dashboard** <a href="#khoiphucodiaaobangbansnapshot-khoiphucodiaaobangsnapshottrenbangdieukhien" id="khoiphucodiaaobangbansnapshot-khoiphucodiaaobangsnapshottrenbangdieukhien"></a>

1. Open the vServer dashboard ati [https://hcm-3.console.greennode.ai/vserver/](https://hcm-3.console.greennode.ai/vserver/).
2. In the navigation sidebar, select **Snapshot**.
3. Choose the Snapshot of the Data Volume on the list page, then select **Action**, press Rollback Volume.
