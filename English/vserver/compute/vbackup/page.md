# Changing the backup policy

You can change the backup policy for a Backup Server. Keep the following points in mind:

* When you attach a backup policy to a Backup Server, this policy will apply to all Volumes attached to that Server.
* You can only attach one backup policy to a Backup Server at a time. If you want to change to a different policy, you must detach the old backup policy and attach the new one.
* In addition to the backup policies you create yourself, we have pre-created default backup policies that are optimized for efficiency, so consider using them.

***

### Changing the Backup Policy <a href="#thaydoichinhsachsaoluu-thaydoichinhsachsaoluu" id="thaydoichinhsachsaoluu-thaydoichinhsachsaoluu"></a>

When logged into your account on the vServer console, you can attach a backup policy when creating a Backup Server, and later, you can change the backup policy as needed.

**Minimum Permission Required:**

To change backup policies, you must have permission to perform the following action:\
IAM: UpdateBackupPolicy

**To change the backup policy for a Backup Server:**

1. Log in to the vBackup console at: [vBackup Console](https://hcm-3.console.greennode.ai/vserver/block-store/backup/backup-server). You must log in as an IAM user, assume the IAM account role, or log in as the Root user account (not recommended) within the organization's management account.
2. In the Backup Server tab, specify the Backup Server, then select "**Change Policy**."
3. Find the policy you want to change to, then select "**Apply**." Note that you can change the policy simultaneously for one or more Backup Servers.
