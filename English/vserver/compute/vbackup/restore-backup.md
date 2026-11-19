# Restore Backup

Once a resource has been backed up at least once, it is considered protected and available for restoration using vBackup Follow these steps to restore the resource using the GreenNode console.

If you are restoring a GreenNode virtual machine, you can perform a Full Restore to restore the virtual machine's entire system to a new virtual machine. Or, you can restore specific drives belonging to a virtual machine. Follow the steps below to finish restoring a virtual machine or your drive:

### **Virtual Server Recovery Process** <a href="#restorebackup-virtualserverrecoveryprocess" id="restorebackup-virtualserverrecoveryprocess"></a>

1. Open the vBackup console at [https://hcm-3.console.greennode.ai/vserver/block-store/backup](https://hcm-3.console.greennode.ai/vserver/block-store/backup)
2. At the navigation page, select the virtual server to be backed up and click **Restore**
3. The page to create a new virtual server will display with the configuration of the backup, you need to select the remaining parameters to finish restoring the backup to a virtual machine
4. Click **Create Server**
5. A Server will be created in the **Shutdown** status with the configuration of the backup you selected earlier

### **Volume Recovery Process** <a href="#restorebackup-volumerecoveryprocess" id="restorebackup-volumerecoveryprocess"></a>

1. Open the vBackup console at  [https://hcm-3.console.greennode.ai/vserver/block-store/backup](https://hcm-3.console.greennode.ai/vserver/block-store/backup)
2. At the navigation page, view the backed up virtual server details
3. At the list of volumes attached to the virtual machine, select the volume you backed up and click **Restore**
4. The create new drive page will display with the configuration of the backup, you need to select the remaining parameters to complete the backup restore to a drive
5. Click **Create Volume**
6. A new volume is created with the configuration of the backup you selected earlier

{% hint style="info" %}
Ghi chú

Regardless of whether you restore a Server or Volume, each restore will create a new one. If you try to restore multiple times for the same resource, there may be multiple duplicate entries for that resource.
{% endhint %}
