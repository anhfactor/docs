# Automatic Backup

The automatic backup feature is a crucial part of the backup service, making it easy for users to protect their data without needing to perform complex manual steps. With this feature, after you have created a backup on the server, the system will automatically activate the automatic backup mode. It will then continue to create backups according to the scheduled plan until the user decides to turn off this feature.

***

### Enabling the Automatic Backup Feature <a href="#tudongsaoluu-battinhnangtudongsaoluu" id="tudongsaoluu-battinhnangtudongsaoluu"></a>

After creating a backup on the server, the automatic backup feature will be activated automatically. You can do this through the user interface or by using specific system commands.

#### **Through the User Interface:** <a href="#tudongsaoluu-thuchienthongquagiaodiennguoidung" id="tudongsaoluu-thuchienthongquagiaodiennguoidung"></a>

1. Access the vServer homepage at: [vServer Overview](https://hcm-3.console.greennode.ai/vserver/overview).
2. In the navigation menu, select the "Backup/Backup server" tab.
3. Choose the Backup server you want to enable the automatic backup feature for from the list.
4. Find and select "**Enable Automatic Backup**."

#### **Through System Commands:** <a href="#tudongsaoluu-thuchienthongqualenhhethong" id="tudongsaoluu-thuchienthongqualenhhethong"></a>

* Use command-line tools or APIs to enable the automatic backup feature for a specific backup.

***

### Disabling the Automatic Backup Feature <a href="#tudongsaoluu-tattinhnangtudongsaoluu" id="tudongsaoluu-tattinhnangtudongsaoluu"></a>

Users can disable the automatic backup feature at any time if they do not want the system to continue creating automatic backups. This decision can be made through the user interface or by using specific system commands.

**Through the User Interface:**

1. Access the vServer homepage at: [vServer Overview](https://hcm-3.console.greennode.ai/vserver/overview).
2. In the navigation menu, select the "Backup/Backup server" tab.
3. Choose the Backup server you want to disable the automatic backup feature for from the list.
4. Find and select "**Disable Automatic Backup**."

**Through System Commands:**

* Use command-line tools or APIs to disable the automatic backup feature for a specific backup.

{% hint style="info" %}
**Important**

Backups created while the automatic backup feature was active will not be affected by the decision to disable the feature. However, new backups will not be created automatically according to the schedule if this feature is disabled.
{% endhint %}
