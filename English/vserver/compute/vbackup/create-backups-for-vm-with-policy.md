# Create backups for VM with policy

On the vBackup console, the Protected Resources page will list all resources that have been backed up at least once. If you are using vBackup for the first time, note that no resources (such as protected virtual machines or disks) will be listed on this page. At GreenNode, we support centralized data protection for virtual machines (Servers) in a cloud computing environment. You can back up virtual machines and the data will be transferred to vStorage.

However, what you need to do now is create a Backup job for your resource following the instructions below:

***

{% hint style="info" %}
Important

When you use the vBackup service for the first time, we will automatically create a default storage location on vStorage with 50 GB of free storage and a usage period of 1 month. However, to store more data, you will need to purchase additional storage capacity. The usage and payment for backup storage will be in the Gold class tier of vStorage. For more information on storage policies and terms, see [here](/broken/pages/RwVKLViyzVmAsRYZjnVj).
{% endhint %}

### Creating a Backup Based on Policy Schedule in the vBackup Interface <a href="#taobansaoluuchomaychuaotheobolichpolicy-taobansaoluutheobolichpolicytaigiaodienvbackup" id="taobansaoluuchomaychuaotheobolichpolicy-taobansaoluutheobolichpolicytaigiaodienvbackup"></a>

1. Open the vBackup console at: [vBackup Console](https://hcm-3.console.greennode.ai/vserver/block-store/backup/backup-server).
2. Select "**Create Backup Server**."
3. Choose the type of resource you want to back up, such as the list of Servers and their attached Volumes.
4. Select the **Policy** you want to apply to the backup. Note that you need to create a Policy to add to your Backup Server. See the guide for creating a Policy at "[Create, Edit, Delete Backup Policies](backup-policies/create-edit-delete-backup-policies.md)."
5. The default storage location will be on **vStorage**. When selecting resources to back up, the system will calculate and provide an estimated backup size. Ensure that your storage capacity on vStorage is sufficient to avoid interruptions and issues during the backup creation process.
6. Enter **notes** for your backups to serve as reminders.
7. Click "**Create Backup Server.**"
8. You can then view the backup job information on the list screen. Select the Backup Server to see information about the protected virtual machines, attached disks, policy, storage location, backup size, and the most recent backup time.

### Creating a Backup Based on Policy Schedule When Creating a Server <a href="#taobansaoluuchomaychuaotheobolichpolicy-taobansaoluutheobolichpolicykhikhoitaoserver" id="taobansaoluuchomaychuaotheobolichpolicy-taobansaoluutheobolichpolicykhikhoitaoserver"></a>

In addition to creating a backup in the vBackup interface, you can also opt to create a backup when creating a new Server. Follow these steps:

1. Open the Server console at: [Server Console](https://hcm-3.console.greennode.ai/vserver/v-server/cloud-server).
2. Select "**Create New Server**."
3. On the Create New Server page, you can check the box to create a Backup Server in the "**Other Settings**" section.
4. When the Server is created, a Backup Server will be created along with the default Policy schedule and displayed on the Backup Server list page.

### Creating a Backup Based on Policy Schedule from the Server List Page <a href="#taobansaoluuchomaychuaotheobolichpolicy-taobansaoluutheobolichpolicytaitrangdanhsachserver" id="taobansaoluuchomaychuaotheobolichpolicy-taobansaoluutheobolichpolicytaitrangdanhsachserver"></a>

You can quickly create a backup for one or more Servers from the Server list management page:

1. Open the Server console at: [Server Console](https://hcm-3.console.greennode.ai/vserver/v-server/cloud-server).
2. Select one or more Servers that need a backup, then click on the toolbar and select "Create Backup."
3. One or more Backup Servers will be created with the default Policy schedule depending on the number of Servers selected for backup.
4. After creating a Backup Server, you can wait for the time specified in the Policy schedule for the system to create the Backup file, or you can choose "[Backup Now](create-backups-immediately-back-now.md)" to create a backup immediately.&#x20;

<br>
