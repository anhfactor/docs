# Delete Backup

After creating backups, you can delete them. We recommend using the vBackup Policy to automatically delete backups that you no longer need by configuring the lifecycle of your backups when creating the backup policy. For example, if you create a backup with a policy scheduled for **daily** backups at **12:00 PM** and retain **four copies** starting from March 16, 2023, the system will create a backup on March 17, 2023, at 12:00 PM and store it. The system will continue to create backups on March 18, 19, and 20. However, on March 21, 2023, when the system creates a backup, the backup from March 17, 2023, will be automatically deleted. To learn more about configuring the lifecycle policy for backups, see "[Schedule Structure of the Policy](backup-policies/schedule-structure-of-the-policy.md)"

However, you may want to manually delete one or more restore points. For example:

You create a "Backup Now." These are restore points that vBackup cannot automatically delete. When vBackup attempts to delete them, it does not have the permission to do so; vBackup only has the authority to delete backups under the policy's control, while those created by "Backup Now" are not affected.

{% hint style="info" %}
**Quan trọng**

If you continue to store unnecessary restore points in your account, this can increase your storage costs.
{% endhint %}

You no longer want a backup plan to operate as you originally configured it. Updating the backup plan will affect future restore points that it will create, but it will not affect restore points that it has already created. To learn more, see "[Backup Policies](backup-policies/)."

***

### Manually Deleting Backups in the vBackup Console <a href="#xoabansaoluu-xoabansaoluubangcachthucongtrentrinhdieukhienvbackup" id="xoabansaoluu-xoabansaoluubangcachthucongtrentrinhdieukhienvbackup"></a>

1. Access the vBackup console at: [vBackup Console](https://hcm-3.console.greennode.ai/vserver/block-store/backup/backup-server).
2. Select and view the details of the Backup Server by clicking on its name.
3. On the detail page, select the "**Restore Point" tab**. Here, you will see backups at different restore points created according to the policy schedule.
4. Select the Backup Server or Backup Volume you need to delete, then click the **delete** icon.
