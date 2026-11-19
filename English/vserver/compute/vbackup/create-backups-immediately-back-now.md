# Create backups immediately (Back now)

The "Backup Now" feature allows you to perform an immediate data backup by clicking the "Backup Now" button for the Backup Server or Server you select. Typically, users may need to perform regular backups, but sometimes an immediate backup is necessary to protect critical data at that moment.

Benefits of Immediate Data Backup:

1. **Flexibility and Urgency:** Immediate data backup allows you to perform backups whenever you feel necessary, instead of waiting for the scheduled backup time. This is very useful in emergency situations or when you want to protect data immediately before a potential incident.
2. **Protecting Important Data Quickly:** If you only need to back up a small portion or a specific project, immediate backup helps you protect important data that you have just worked on.
3. **Quick Recovery:** When you need to recover data, you will have the most recent backup available.

***

### Creating an Immediate Backup for a Backup Server on the vBackup Console <a href="#taobansaoluungaylaptuc-backupnow-taobansaoluungaylaptucchobanbackupservertrenbangdieukhienvbackup" id="taobansaoluungaylaptuc-backupnow-taobansaoluungaylaptucchobanbackupservertrenbangdieukhienvbackup"></a>

1. After creating the Backup Server based on the Policy schedule (see the guide for creating a Backup Server at "[Creating a Backup for Virtual Servers Based on Policy ](create-backups-for-vm-with-policy.md)").
2. Select the newly created Backup Server, then select "**Backup Now**."
3. Choose "**Backup Now**," and a backup will be created immediately at the time of action and will be displayed on the Backup Server list page.

{% hint style="info" %}
**Note**

When you create a "Backup Now" for a Backup Server, this backup will be listed under the Restore Point tab and will not be affected by the retention rules of the Policy schedule unless you manually delete it.
{% endhint %}

***

### Creating an Immediate Backup for a Server on the vBackup Console <a href="#taobansaoluungaylaptuc-backupnow-taobansaoluungaylaptucchoservertrenbangdieukhienvbackup" id="taobansaoluungaylaptuc-backupnow-taobansaoluungaylaptucchoservertrenbangdieukhienvbackup"></a>

1. You can perform a "Backup Now" on the Server list page. Access the vServer console at: [vServer Console](https://hcm-3.console.greennode.ai/vserver/v-server/cloud-server).
2. Select one or more Servers you want to create an immediate backup for.
3. Then select "**Actions**," and choose "**Backup Now**."
4. A backup will be created immediately at the time of action and will be displayed on the Backup Server list page.

{% hint style="info" %}
**Note:**

When you create a "Backup Now" for a Server, this backup will be listed under the Restore Point tab and will not be affected by the retention rules of the Policy schedule unless you manually delete it.
{% endhint %}
