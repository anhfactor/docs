# Create and Manage PostgreSQL Cluster

PostgreSQL Cluster enables deploying a database with a **1 Writer + N Readers** architecture, ensuring **High Availability** and the ability to **scale read** operations for your application. When the Writer encounters an issue, the system automatically fails over to a Reader without manual intervention.

For more information about concepts, architecture, and the comparison between Single Node and Cluster, please refer to [PostgreSQL Cluster](README.md).

***

## Create a PostgreSQL Cluster

### Access the vDB Portal

You can access the vDB service interface in 2 ways:

* **Option 1**: Go to the GreenNode homepage at [https://dashboard.console.greennode.ai/](https://dashboard.console.greennode.ai/). On the main interface, navigate to **vServer** and select **vDB Relational** from the list of vServer products/services.
* **Option 2**: Go directly to the vDB Relational homepage at [https://vdb.console.greennode.ai/relational/database](https://vdb.console.greennode.ai/relational/database)

### Create a PostgreSQL Cluster

On the Database management interface, click **Create Database**. The creation process goes through the following steps:

#### Step 1: Basic Configuration

* **Cluster Name**: Enter a name for the cluster (6-20 characters, must start with a letter).
* **Database Engine**: Select **PostgreSQL**.
* **Deployment Type**: Select **Cluster** (this option only appears when the Engine is PostgreSQL).
* **Availability & Durability**: Select **Single-AZ** or **Multi-AZ**. For Multi-AZ, see the dedicated guide at [Create a Multi-AZ PostgreSQL Cluster](create-multi-az-postgresql-cluster.md).

{% hint style="info" %}
When selecting **Cluster** as the Deployment Type, the label changes from "Database Instance Name" to "Cluster Name".
{% endhint %}

**Restore from Backup (optional):**

When selecting **Cluster** as the Deployment Type, the system also displays a **Backup Image** section that allows you to restore the cluster from an existing backup:

* Expand a backup item to view **restore points**.
* Select a restore point if you want to create a cluster with data from that backup.
* If no restore point is selected, the cluster will be created with an empty database.

{% hint style="warning" %}
**Note:** When restoring from a backup, the **Storage Size** of the new cluster must be greater than or equal to the **Backup Size** of the selected backup.
{% endhint %}

#### Step 2: Specifications

* **Engine Version**: Select the PostgreSQL version (e.g., 15, 14, 13...).
* **Flavor**: Select the instance configuration (vCPU, RAM). This configuration applies to **all nodes** in the cluster.
* **Storage Type**: Select the storage disk type.
* **Storage Size**: Select the storage capacity (includes data and logs).
* **Number of Nodes**: Select the number of nodes for the cluster (from 2 to 10). The system will display the corresponding **Role Distribution**:

| Number of Nodes | Role Distribution |
| --- | --- |
| 2 | 1 Writer + 1 Reader |
| 3 | 1 Writer + 2 Readers |
| 5 | 1 Writer + 4 Readers |
| 10 | 1 Writer + 9 Readers |

#### Step 3: DB Settings

* **Master Username**: Username for managing the database cluster.

{% hint style="warning" %}
**Reserved Usernames:** You must not use the following usernames: `postgres`, `admin`, `cron_admin`, `robot_zmon`, `vngpooler`, `vngpam`, `vngrep`, `vngsuperrole`.
{% endhint %}

* **Master Password**: Password for the master user. The password must meet the following requirements:
  * Length of 8-32 characters.
  * Allowed characters: A-Z, a-z, 0-9, and special characters ($, ^, \_, <, >).
  * Must start with a letter (A-Z or a-z).
  * Must not start or end with a special character.

#### Step 4: Network & Security

* **Cloud Network (VPC & Subnet)**: Select the VPC and Subnet for the cluster. If you don't have one yet, you can create a new one following the guide [here](../../../../vserver/compute-hcm03-1a/vpc/virtual-private-cloud-vpc.md).
* **Public Accessibility**: Enable if you want the cluster to have a Public IP and be accessible from the Internet; disable if you only want access via Private IP.
* **Multi-AZ**: if you selected **Multi-AZ** in Step 1, this step requires a VPC with DNS enabled and shows a **Subnets** table for zone selection instead of a single Subnet — see [Create a Multi-AZ PostgreSQL Cluster](create-multi-az-postgresql-cluster.md).

{% hint style="warning" %}
**Note:** The Public Accessibility setting can only be selected **once** at the time of creation and cannot be changed afterwards.
{% endhint %}

#### Step 5: DB Options

* **Database Name**: Name of the database that will be automatically initialized.
* **DB Configuration Group** (optional): Select a Configuration Group to apply to the cluster.

#### Step 6: Backup Settings

{% hint style="info" %}
Backup Settings are **mandatory** when creating a PostgreSQL Cluster. You must select both a Backup Policy and a Backup Location.
{% endhint %}

* **Backup Policy**: Select the policy that defines the backup schedule and retention period from Backup Center.
* **Backup Location**: Select the backup storage location from Backup Center. The dropdown only shows locations with **status = Available** and **Product = vDB**, sorted in **newest first** order.

{% hint style="warning" %}
**If no Backup Location is available:**

If your account has no Backup Location in Available status, the Backup Location dropdown will appear with a red border and an error message. You need to click the link in the message to open Backup Center and create a new location before continuing to create the cluster.
{% endhint %}

If you don't have a Backup Policy yet, you can click the link to open Backup Center and create a new one.

{% hint style="info" %}
**Note:** The Backup Location **cannot be changed** after the cluster has been created. Each cluster is permanently bound to a single Backup Location, so choose the appropriate location from the start.
{% endhint %}

#### Completion

In the **Summary** section on the right, review all configuration information. When everything is correct, click **Create Database** to complete. During initialization, the cluster will have **Building** status. When initialization is successful, the cluster will transition to **Active** status.

***

## Manage PostgreSQL Cluster

### View Database List

On the Database List page, you can quickly filter databases by deployment type:

| Tab | Description |
| --- | --- |
| **All Databases** | Shows all databases |
| **Single Node** | Shows only Single Node databases |
| **Clusters** | Shows only Cluster databases |

### View Cluster Details

When clicking on a cluster in the list, the detail page shows the following information:

**General Information:**

| Information | Description | Example |
| --- | --- | --- |
| ID | Cluster identifier | pg-1dfa6aaf-20c9-44a1-... |
| Zone | Availability Zone | HCM03-1A |
| Role | Instance role | Primary Writer / Replica Reader |
| Replica Source | Replica source (if any) | N/A |
| Instance Type | Instance configuration | db-postgre.s-general-2x4-n10 (2 Core, 4 GB) |
| Engine | Engine and deployment type | PostgreSQL 15 (Cluster, 3 Node) |
| Storage | Storage capacity and type | 20 GB (GEN2-NVME-IOPS5000) |
| Free GB | Free backup capacity included with the package | 20 GB |
| Configuration Group | Applied configuration group | default-group |
| Network | VPC network | vpc-10-10-0-0 |

**Detail tabs:**

| Tab | Content |
| --- | --- |
| **Configuration** | Flavor information (vCPU, RAM) and storage (type, size, disk usage) |
| **Connectivity & Security** | Connection endpoints and security settings |
| **Backup** | Backup history, create manual backup, view backup information |
| **History** | Activity logs |
| **Monitor** | Metrics and monitoring charts, see the **Monitor a PostgreSQL Cluster (Monitoring)** section below |

***

### Back Up Now

The **Back up now** button is displayed directly on the action bar of the cluster detail page (alongside Reboot, Edit Number of Nodes, Resize IOPS, Resize Storage Size), not inside the More Actions (⋮) menu.

1. On the cluster detail page, click **Back up now** on the action bar.
2. The system displays a confirmation dialog.
3. Click **Confirm** to start creating the backup.

After confirmation, the system triggers the creation of a Full Snapshot and displays a toast notification. The new backup appears in the **Backup** tab with **In Progress** status, transitioning to **Completed** when done.

{% hint style="warning" %}
**Note:**

* The **Back up now** button will be **disabled** when a backup job (Auto or Manual) is currently running. Hovering over the button will show a tooltip.
* If the account runs out of quota or is locked, the system returns an error and does not automatically retry.
{% endhint %}

### Edit Number of Nodes

You can change the number of nodes in the cluster (from 2 to 10):

1. On the cluster detail page, click **Edit Number of Nodes** on the action bar.
2. Enter the desired number of nodes.
3. Confirm the change.

The system will automatically add or remove Reader nodes. The Writer node is not affected.

### Resize IOPS

1. On the cluster detail page, click **Resize IOPS** on the action bar.
2. Select the new IOPS value.
3. Confirm the change.

### Resize Storage Size

1. On the cluster detail page, click **Resize Storage Size** on the action bar.
2. Enter the new storage capacity (only increasing is supported, decreasing is not).
3. Confirm the change.

### Edit Configuration Group

1. On the cluster detail page, click **More Actions (⋮)** > **Edit Configuration Group**.
2. Select the new Configuration Group.
3. Confirm the change.

### Reboot Cluster

1. On the cluster detail page, click **Reboot** on the action bar.
2. Confirm the restart.

### Monitor a PostgreSQL Cluster (Monitoring)

When you create a PostgreSQL Cluster, the system automatically collects the cluster's metrics through vMonitor Platform and displays them in the **Monitor** tab of the cluster detail page. Some metrics are enabled by default, with no extra configuration needed.

To view metrics:

1. Go to the PostgreSQL Cluster detail page.
2. Select the **Monitor** tab.
3. Select **Cluster metric** to view metrics for the whole cluster, or **Node metric** to view metrics for each node.
4. Select the time range in the top-right corner, from 15 minutes to 1 day.

Main charts available in the Monitor tab:

| View | Group | Charts |
| --- | --- | --- |
| Cluster metric | Connections | Max Connections, Connection Usage Per Node |
| Cluster metric | Memory and cache | Shared Buffers, Cache Hit Rate |
| Cluster metric | Replication | Replication Lag |
| Node metric | Node status | Online Nodes |
| Node metric | Resources | CPU Usage, Mem Usage (Percent), Volume Usage (Percent) |

To view more metrics beyond the default set, build your own dashboards, or create alarms, select **Monitored by vMonitor Platform** to go to vMonitor Platform and enable Detailed Monitoring. See also:

* [Monitoring vDB with vMonitor Platform](../../working-with-rds/giam-sat-hoat-dong-vdb-bang-vmonitor-platform.md)
* [List vDB's metrics](../../../../vmonitor-platform/cach-tinh-nang-cua-vmonitor-platform/metrics/danh-sach-metrics-ho-tro/danh-sach-metrics-cua-vdb.md)

***

## Manage Backup

### View Backup Information

On the cluster detail page, select the **Backup** tab to view:

* **Backup Information**: Overview including Description, Created Date, Latest Record, Backup Size, Backup Policy, Backup Location.
* **Backup List**: List of backups with Backup DB Point ID, Min.Restore Size (GB), Backup Type, Schedule Type, Backup Location, Backup Point, Status, Action (Restore / Delete).

At the top of the Backup tab there is a **"View full backup details →"** link that goes directly to the detailed backup page for the current cluster in Backup Center (opens in a new tab).

### Create Manual Backup

There are 2 ways to create a Manual Backup:

* **Option 1 (recommended):** Click the **Back up now** button directly on the action bar of the cluster detail page (see guide at [Back Up Now](#back-up-now)).
* **Option 2:** In the **Backup** tab, click **Create Manual Backup**, then confirm.

The system will create a **Full Snapshot** of the database. The new backup appears in the list with **In Progress** status, transitioning to **Completed** when done.

{% hint style="warning" %}
**Note:**

* Manual Backup only supports creating a **Full Snapshot**.
* Only **1 job** backup/restore is allowed to run at a time. If Auto Backup is running, Manual Backup will be rejected.
* If the account runs out of quota or is locked, the system will return an error and will not automatically retry.
{% endhint %}

### Restore from Backup

Restoring from a backup will **create a new cluster** (it does not restore over the existing cluster):

1. In the **Backup** tab, click **Restore** on the backup you want to restore.
2. Or when creating a new cluster, select the restore point in the **Backup Image** section in Step 1.
3. Configure the parameters for the new cluster (Storage Size must be >= Backup Size).
4. Complete the cluster creation.

### vDB Backup Page

Go to **Menu: Relational > Backup** to view an overview of backups:

* When no backups exist: Displays a message and a **Create a Backup** button to go to Backup Center.
* When backups exist: Displays a list of backups and a **Go to Backup Center** button for full management (Download, Restore, Delete, Policy).

{% hint style="info" %}
The vDB Backup page only allows **viewing** the backup list. To perform full management operations (Download, Restore, Delete), please go to **Backup Center**.
{% endhint %}

***

## Delete PostgreSQL Cluster

1. On the cluster detail page, click **More Actions (⋮)** > **Delete**.
2. The system displays a confirmation dialog with the following components:
   * **"Create final backup?" checkbox** (optional): Check this if you want to create a final backup before deletion.
   * **Confirmation field:** Enter **`delete`** to activate the Delete button.
3. Click **Delete** (red) to complete.

{% hint style="info" %}
**If the cluster no longer has a Backup Database in Backup Center:**

* The "Create final backup?" checkbox will be **disabled** and cannot be selected.
* The system displays a notification.
* You still need to enter **`delete`** to confirm.
{% endhint %}

{% hint style="warning" %}
**Note when deleting a Cluster:**

* **Auto Backup** will be automatically deleted along with the cluster.
* **Manual Backup** will be retained. You need to manually delete it in Backup Center if no longer needed.
* The deletion action **cannot be undone**. Make sure you have backed up any necessary data before deleting.
{% endhint %}
