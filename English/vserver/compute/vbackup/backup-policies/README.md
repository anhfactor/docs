# Backup Policies

vBackup allows you to create backup plans that define how to back up your disk and virtual machine resources. The rules in the plan include a variety of settings, such as backup frequency, time frame where the backup takes place, number of backups. You can then apply these policies to the resource groups you want to protect.

Backup policies in the vBackup service will include those created by default by the system and policies created later by the user. After creating the policy, you can attach the backup policy to your Backup. You can apply inheritance rules to combine policies, appropriate nesting timeframe, reasonable number of saves. This results in an effective backup policy for each different backup job. Have an effective policy that guides vBackup on how to automatically back up your resources in the best way for your organization.

Backup policies give you granular control over backing up your resources to whatever level you require. For example, you can specify in an attachment policy with critical resources to ensure all are backed up concurrently and consistently. That policy may be included under the default backup configuration. Then, you can edit the backup policy to suit your needs. For example, HR organization can specify backup frequency as once per week, while Production Organization unit specify once per day, now you need to choose a schedule that integrates 2 backup time frames as above, refer to {[Schedule Structure of the Policy](schedule-structure-of-the-policy.md)}.

{% hint style="info" %}
**Important**

Remember that while a partial policy strategy as described earlier may work, if an effective policy for an account is incomplete it will result in errors or resources not being successfully backed up. Therefore, consider requiring all backup policies to be complete and valid.
{% endhint %}

***

### Getting started with backup policies <a href="#backuppolicies-gettingstartedwithbackuppolicies" id="backuppolicies-gettingstartedwithbackuppolicies"></a>

**Follow these steps to start using backup policies:**

1. Learn about what you must have to perform backup policy tasks.
2. Learn about some of our recommended best practices for using backup policies.
3. Enable backup policies for your backups.
4. Create a backup policy.
5. Attach the backup policy to the backup.
6. View effective backup policies and make adjustments accordingly.

<br>
