# Delete Snapshot

Snapshots store data copies at a specific point in time. When you remove unnecessary snapshots, you free up storage space, allowing you to utilize that space for other purposes or save storage costs. This also helps manage costs more effectively in cloud computing services, where you often pay based on storage capacity and usage time.

However, maintaining unnecessary or irrelevant snapshots unrelated to the recovery process can make data management complex. Deleting unnecessary snapshots helps maintain cleanliness and efficiency in your data management.

Moreover, note that snapshots can also impact system and server performance. When there are too many snapshots or they are created and maintained indiscriminately, the overall performance of the system and storage can be affected. Deleting unnecessary snapshots can improve this performance.

***

### Limitations <a href="#xoasnapshot-gioihan" id="xoasnapshot-gioihan"></a>

* When you delete a snapshot, the data contained within that snapshot will be deleted, but the disk where the snapshot was created remains unaffected.
* Deleting a snapshot means you won't be able to restore data from them in the future. Ensure you have a backup strategy in place if you need to retain data for compliance or disaster recovery purposes.

***

**You can delete snapshots for Servers and Volumes on our control panel, please refer to the following instructions:**

Note

You can only delete Volume snapshots on the Snapshot management page; to delete Server snapshots, you need to delete them on the Server detail page.

### **Delete Volume Snapshot on the Snapshot list page on the Dashboard** <a href="#xoasnapshot-xoasnapshotvolumetaitrangdanhsachsnapshottrenbangdieukhien" id="xoasnapshot-xoasnapshotvolumetaitrangdanhsachsnapshottrenbangdieukhien"></a>

1. Open the vServer dashboard at [https://hcm-3.console.greennode.ai/vserver/](https://hcm-3.console.greennode.ai/vserver/).
2. In the navigation sidebar, select **Snapshot**.
3. Choose the Snapshot you want to delete, then select **Action**, click **Delete Snapsho**t.

***

### **Delete Volume Snapshot on the Volume detail page on the Dashboard** <a href="#xoasnapshot-xoasnapshotvolumetaitrangchitietvolumetrenbangdieukhien" id="xoasnapshot-xoasnapshotvolumetaitrangchitietvolumetrenbangdieukhien"></a>

1. Open the vServer Dashboard at [https://hcm-3.console.greennode.ai/vserver/](https://hcm-3.console.greennode.ai/vserver/).
2. In the navigation sidebar, select **Volume**.
3. Click on the Volume name to go to the Volume detail page
4. Switch to the **Associated Snapshot** Tab
5. Select the Snapshot Volume to be deleted and choose **Delete**

***

### **Delete Server Snapshot on the Server detail page on the Dashboard** <a href="#xoasnapshot-xoasnapshotservertaitrangchitietservertrenbangdieukhien" id="xoasnapshot-xoasnapshotservertaitrangchitietservertrenbangdieukhien"></a>

1. Open the vServer Dashboard at [https://hcm-3.console.greennode.ai/vserver/](https://hcm-3.console.greennode.ai/vserver/).
2. In the navigation sidebar, select Server.
3. Click on the Server name to go to the Server detail page
4. Switch to the **Associated Snapshot** Tab
5.  Select the Snapshot Server to be deleted and choose **Delete.**

