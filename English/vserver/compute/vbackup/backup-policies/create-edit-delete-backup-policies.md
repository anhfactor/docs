# Create, edit, delete backup policies

To be able to create backups of your resources you need to create a new policy.

When backup requirements change, you can update existing policies.

When you no longer need the policy, you need to separate it from your backup resources, and you can delete it.

***

### **Create Backup Policy** <a href="#create-edit-deletebackuppolicies-createbackuppolicy" id="create-edit-deletebackuppolicies-createbackuppolicy"></a>



{% hint style="info" %}
**Important**

Make sure that the rules in the backup policy you create meet your needs, but are not too redundant, as that will lead to cost and system resources.
{% endhint %}

You can create policies in the vServer Management Console using a visual editor that allows you to choose options for creating policies for you. It's a great way to create your first policies and feel comfortable using them.

**The procedure for creating a backup policy:**

1. Open the vBackup control panel at [https://hcm-3.console.greennode.ai/vserver/block-store/backup](https://hcm-3.console.greennode.ai/vserver/block-store/backup)
2. In the navigation menu bar, select **Backup Policy Tab**
3. Select **Create Backup Policy**
4. On the Policy creation page, enter the **Policy Name** information in the Basic Information section
5. Then in the **Policy Settings section**, select the time and time zone in which the system will perform the backup
6. Choose the **backup frequency** that suits your usage needs by Day, Week, Month, note that you can combine all 3 together to create the perfect calendar
7. Enter the **number of copies** that will be kept by the system according to the most recent backups
8. In addition, you can choose to **automatically back up** for **drives** added to the virtual machine later.
9. Click "**Create Backup Policy**"
10. Then you can view the newly created backup policy information at the list screen.

{% hint style="info" %}
**How backup policies work**

A backup policy selects the backup frequency according to **Daily** at **12:00** and number of backups are 4. Every day at 12:00 PM, the system according to the above time frame will create a backup for the virtual server, with the first backup will be a full backup of the VM, the next day will backup the VM changes since yesterday's last backup, the number of retentions will be **4 copies** for the **last 4 days**.
{% endhint %}

### **Edit Backup Policy** <a href="#create-edit-deletebackuppolicies-editbackuppolicy" id="create-edit-deletebackuppolicies-editbackuppolicy"></a>

When a backup policy no longer matches business requirements or data scale or recovery times are required faster you need to revise the parameters of the backup policy

**Backup policy editing process:**

1. Open the vBackup control panel at [https://hcm-3.console.greennode.ai/vserver/block-store/backup](https://hcm-3.console.greennode.ai/vserver/block-store/backup)
2. In the navigation menu bar, select **Backup Policy Tab**
3. Click **Edit** Backup Policy
4. You can re-enter the policy name, as well as change all the parameters of the backup time, time zone, as well as the backup calendar set, the number of copies of the Backup Policy that you want to update
5. After updating the policy, select **Save** to change

### **Delete Backup Policy** <a href="#create-edit-deletebackuppolicies-deletebackuppolicy" id="create-edit-deletebackuppolicies-deletebackuppolicy"></a>

You can delete a backup policy if you no longer need to use it, but it should be noted that you cannot delete the default backup policy created by the system.

**Backup Policy deleting process:**

1. Open the vBackup control panel at [https://hcm-3.console.greennode.ai/vserver/block-store/backup](https://hcm-3.console.greennode.ai/vserver/block-store/backup)
2. In the navigation menu bar, select **Backup Policy Tab**
3. Select **Delete** Backup Policy
4. After deleting the backup policy will be lost from the list page
