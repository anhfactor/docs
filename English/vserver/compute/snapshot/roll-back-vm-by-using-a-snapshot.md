# Roll back VM by using a snapshot

You can restore virtual disks or virtual servers using previously created snapshots. The following describes how to restore a virtual server using snapshots.

Using snapshots allows you to quickly restore data and systems after incidents, reducing system downtime. It's a safe way to back up your important data, ensuring that you can recover data and disks as needed, such as in the case of hardware failures, software errors, or accidental data deletion. Compared to reconfiguring and restoring systems from scratch, using snapshots saves significant time and effort.

***

### **Cases for VM Recovery** <a href="#khoiphucmaychuaobangbansnapshot-cactruonghopcankhoiphucmaychuao" id="khoiphucmaychuaobangbansnapshot-cactruonghopcankhoiphucmaychuao"></a>

* **Serious System Failures**: When a virtual server encounters a severe, unrecoverable failure that significantly impacts services and data, you may consider restoring the virtual server from a recent backup to restore services and data.
* **Specific Software Errors:** If the virtual server experiences specific software errors or malfunctions after installation or software updates, you can restore the virtual server to a state before the error occurred.
* **Security Risks:** If your virtual server is compromised by a network attack or there are suspicions of intrusion, you should consider restoring the virtual server from a point before the risk occurred to eliminate security vulnerabilities.
* **Testing and Development**: During application development or testing of new configurations, you can restore the virtual server to its initial state after testing to clean up the environment and prepare for further testing steps.
* **Creating Test Environments**: If you need to create a completely new test environment, you can restore the virtual server from a backup or snapshot to have a separate working environment. End-User Errors: If end users or virtual server administrators cause serious errors in the system, you may consider restoring the virtual server to remove unintended changes.
* **End-User Errors:** If end users or virtual server administrators cause serious errors in the system, you may consider restoring the virtual server to remove unintended changes.
* **Data Recovery Mistakes:** If you accidentally delete important data or make incorrect changes to data on the virtual server, you can restore the virtual server from a recent backup to recover lost data.

***

### **Risks** <a href="#khoiphucmaychuaobangbansnapshot-ruiro" id="khoiphucmaychuaobangbansnapshot-ruiro"></a>

* **Corrupted Data:** If you use a corrupted or damaged snapshot, restoration may result in incorrect or corrupted data. This is particularly important if you don't check the snapshot before using it.
* **Snapshot Creation Time**: If you create snapshots irregularly or infrequently, you may lose important data if an incident occurs between snapshot creations. The time gap between snapshots also affects data recovery capabilities.
* **Storage Costs:** Maintaining multiple snapshots can incur significant storage costs. You need to consider the balance between the benefits of storing multiple snapshots and the corresponding costs.
* **Careful Snapshot Management:** Managing snapshots requires careful attention to ensure you don't accidentally delete important backups or maintain too many unnecessary backups.

Using snapshots to restore VM has many important benefits but also comes with risks that need careful consideration and management. It's important to implement security measures and verify snapshot integrity before performing data recovery."

<br>

***

Notes

You can only restore a virtual server with a Snapshot of the Boot Volume.

### **Restoring a VM with a Snapshot on the Dashboard** <a href="#khoiphucmaychuaobangbansnapshot-khoiphucmaychuaobangsnapshottrenbangdieukhien" id="khoiphucmaychuaobangbansnapshot-khoiphucmaychuaobangsnapshottrenbangdieukhien"></a>

1. Open the vServer Dashboard at [https://hcm-3.console.greennode.ai/vserver/](https://hcm-3.console.greennode.ai/vserver/).
2. In the navigation sidebar, select **Snapshot.**
3. Choose the Snapshot of the Boot Volume on the list page, then select **Actions**, press Rollback Server.

### **Create Server with a Snapshot on the Create Server Screen** <a href="#khoiphucmaychuaobangbansnapshot-taomaychu-server-bangsnapshottrenmanhinhtaoserversnapshotcreateserve" id="khoiphucmaychuaobangbansnapshot-taomaychu-server-bangsnapshottrenmanhinhtaoserversnapshotcreateserve"></a>

1. Log in and open the vServer dashboard at [https://hcm-3.console.greennode.ai/vserver](https://hcm-3.console.greennode.ai/vserver/);
2. In the navigation sidebar, select **Server**;
3. Choose the "**Create a Server**" button to navigate to the Create Server screen;
4. To configure Creating a Server with the snapshot. In the "**Basic Configuration/Image**" section, select the "**My snapshot**" tab;
5. Users can select the appropriate snapshot to recreate the Server at the corresponding time.

<figure><img src="https://docs.vngcloud.vn/download/attachments/64554116/image2024-3-25_9-46-42.png?version=1&#x26;modificationDate=1711334805000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Note

When configuring a new Server creation with Snapshot, users still perform configuration operations in other sections (Configuration type, volume, Network settings, Other settings) as usual, see instructions at the link..

### **Create a Server with a Snapshot on the Snapshot Screen** <a href="#khoiphucmaychuaobangbansnapshot-taomaychu-server-bangsnapshottrenmanhinhsnapshot" id="khoiphucmaychuaobangbansnapshot-taomaychu-server-bangsnapshottrenmanhinhsnapshot"></a>

1. Log in and open the vServer dashboard at [https://hcm-3.console.greennode.ai/vserver](https://hcm-3.console.greennode.ai/vserver/);
2. In the navigation sidebar, select **Snapshot**;
3. On the Snapshot list screen, User **clicks on a Snapshot Server** to navigate to the detailed information screen.
4. On the detailed screen of the Snapshot Server, User selects the "**Restore Point**" tab.
5. Then select the corresponding Snapshot version to create the Server, by clicking on the action button, choose "**Create server**".
6. Navigate to the Create Server screen with the selected Snapshot file option, and continue the operation similar to "Creating a Server with Snapshot on the Create Server Screen" as above../.

<figure><img src="https://docs.vngcloud.vn/download/attachments/64554116/image2024-3-25_10-11-32.png?version=1&#x26;modificationDate=1711336295000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
