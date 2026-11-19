# Convert Volume Type

This feature allows users to switch the volume type from SSD (Solid State Drive) to NVMe (Non-Volatile Memory Express) and vice versa to optimize data storage performance on the system.

## Purpose

Convert between SSD and NVMe with following purpose:

### **Convert from SSD to NVMe**

1. **Increase Data Access Speed:** When applications or tasks require high data access speeds, switching from SSD to NVMe can improve performance and reduce response times.
2. **Handle Large Data Sets:** When working with large data files or needing to process data quickly, NVMe can provide faster read/write speeds, enhancing work efficiency.
3. **High Latency Requirements:** Applications such as databases, virtual servers, or those requiring lower response times can benefit from using NVMe.

### **Convert from NVMe to SSD**

1. **Cost Reduction:** In some cases, using SSD instead of NVMe can help reduce system operating costs while still providing reliable storage performance.
2. **Non-High-Speed Application Requirements:** When applications or tasks do not require extremely high data access speeds, switching from NVMe to SSD may not affect performance while reducing costs.
3. **Data Backup:** Using SSD instead of NVMe in scenarios not requiring high speeds can help back up data at a lower cost.

## Use Cases

Before starting, users should note a few important considerations:

* The conversion process may take some time depending on the size and status of the volume.
* The conversion process involves four steps, requiring user interaction between steps. Please ensure all necessary actions are taken between steps to continue the volume conversion.

### **Convert from SSD to NVMe**

Refer to the detailed guide below to convert the disk from SSD to NVMe.

**Step 0: Configure the Conversion Information:**

* 0.1: Access the volume list from the portal [here](https://hcm-3.console.greennode.ai/vserver/block-store/volumes).
* 0.2: Navigate to the volume to be converted, click the **three-dot icon** in the **Action** column.
* 0.3: Click "**Migrate Volume**."
* 0.4: In the window, select the following information for migration:
  * Type: Default to NVMe.
  * Size: Current capacity, cannot be changed.
  * IOPS: Adjustable, select IOPS as needed.
  * 0.5: Confirm the deletion of volume snapshots after a successful conversion. Then click "**Migrate**".

**Step 1: Initiate Migration (No Downtime)**

* The system creates a new volume with the configuration selected in step 0.4, then backs up data from the current volume to the new volume.
*   Processing time depends on the size and configuration of each volume. During this step, users can still write data to the volume without any downtime.

    <figure><img src="../../../.gitbook/assets/image (1) (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

**Step 2: Initiate Differential Migration (With Downtime)**

The purpose of this step is to back up new/changed data during step 1.

2.1: After completing step 1, the interface proceeds to step 2/4, requiring user interaction. Refer to the illustration below:

<figure><img src="../../../.gitbook/assets/image (2) (2) (1).png" alt=""><figcaption></figcaption></figure>

2.2: Click "Action Required" to continue the migration process. A "Migrate Volume" window will appear; click "Continue" to confirm. This process will interrupt services on the current volume. The downtime depends on the amount of data changed during step 1. The migration status will appear as follows:

<figure><img src="../../../.gitbook/assets/image (3) (2).png" alt=""><figcaption></figcaption></figure>

_<mark style="color:orange;">**If the volume is in use on a virtual server, users must shut down the server to continue the migration.**</mark>_

<figure><img src="../../../.gitbook/assets/image (4) (2).png" alt=""><figcaption></figcaption></figure>

**Step 3: Confirm Use of the Fully Converted Volume**

3.1: After completing step 1, the interface proceeds to step 3/4, requiring user interaction. Refer to the illustration below:

<figure><img src="../../../.gitbook/assets/image (5) (2).png" alt=""><figcaption></figcaption></figure>

3.2: Click "Action Required." A "Migrate Volume" window will appear, allowing users to confirm two actions:

3.2.1: **Delete Old Volume:** The system will complete the update of the new volume, and services on the volume will resume as usual. Note that snapshots related to the volume before the update will be permanently deleted.

3.2.2: **Restore:** Restore the volume to its pre-migration state. Data on the volume will be updated to the point before initiating the differential migration (step 2).

### **Convert from NVMe to SSD**

Refer to the detailed guide below to convert the disk from NVMe to SSD.

**Step 0: Configure the Conversion Information:**

* 0.1: Access the volume list from the portal [here](https://hcm-3.console.greennode.ai/vserver/block-store/volumes).
* 0.2: Navigate to the volume to be converted, click the **three-dot** icon in the **Action** column.
* 0.3: Click "**Migrate Volume**"
* 0.4: In the window, select the following information for migration:
  * Type: Default to SSD.
  * Size: Current capacity, cannot be changed.
  * IOPS: Adjustable, select IOPS as needed.
* 0.5: Confirm the deletion of volume snapshots after a successful conversion. Then click "**Migrate**"

**Step 1: Initiate Migration (No Downtime)**

* The system creates a new volume with the configuration selected in step 0.4, then backs up data from the current volume to the new volume.
*   Processing time depends on the size and configuration of each volume. During this step, users can still write data to the volume without any downtime.

    <figure><img src="../../../.gitbook/assets/image (6) (2).png" alt=""><figcaption></figcaption></figure>

**Step 2: Initiate Differential Migration (With Downtime)**

The purpose of this step is to back up new/changed data during step 1.

*   2.1: After completing step 1, the interface proceeds to step 2/4, requiring user interaction. Refer to the illustration below:

    <figure><img src="../../../.gitbook/assets/image (7) (2).png" alt=""><figcaption></figcaption></figure>
*   2.2: Click "Action Required" to continue the migration process. A "Migrate Volume" window will appear; click "Continue" to confirm. This process will interrupt services on the current volume. The downtime depends on the amount of data changed during step 1. The migration status will appear as follows:

    <figure><img src="../../../.gitbook/assets/image (8) (2).png" alt=""><figcaption></figcaption></figure>

_<mark style="color:orange;">**If the volume is in use on a virtual server, users must shut down the server to continue the migration.**</mark>_

<figure><img src="../../../.gitbook/assets/image (10) (2).png" alt=""><figcaption></figcaption></figure>

**Step 3: Confirm Use of the Fully Converted Volume**

*   3.1: After completing step 1, the interface proceeds to step 3/4, requiring user interaction. Refer to the illustration below:

    <figure><img src="../../../.gitbook/assets/image (11) (2).png" alt=""><figcaption></figcaption></figure>
* 3.2: Click "Action Required." A "Migrate Volume" window will appear, allowing users to confirm two actions:
  * 3.2.1: **Delete Old Volume:** The system will complete the update of the new volume, and services on the volume will resume as usual. Note that snapshots related to the volume before the update will be permanently deleted.
  * 3.2.2: **Restore:** Restore the volume to its pre-migration state. Data on the volume will be updated to the point before initiating the differential migration (step 2).
