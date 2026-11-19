# Snapshot

Snapshot feature is an essential component of GreenNode's cloud storage system. It provides the ability to create and manage backups of your virtual disk data at specific points in time, offering significant benefits in data protection, resource optimization, and ensuring data recovery in case of need.

Each snapshot contains all the information necessary to restore your data to the state it was in at the time the snapshot was created. When you create a new disk from a snapshot, this new disk starts as an exact copy of the original disk used to create the snapshot. The data copying process is done in the background so you can start using it immediately. If you access data that has not been loaded, the disk will automatically load the requested data from the system, and then continue to load the rest of the disk data in the background.

Snapshot also supports comprehensive data encryption, ensuring the security of stored data and helping to comply with security and privacy requirements. You can create snapshots for encrypted disks and can create new disks from encrypted snapshots.

At GreenNode, we support creating Snapshots for both Servers and Volumes, simplifying the Snapshot creation process and meeting all your usage needs. Once you have created Snapshots for your virtual machines and virtual disks, you can use our Roll Back feature to restore the state of the virtual machine and virtual disk to the time the Snapshot was created.

<figure><img src="../../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (2).png" alt=""><figcaption></figcaption></figure>

***

## How Snapshot work

The creation of snapshots in our cloud storage system is an incredibly complex and optimized process. When you create the first snapshot from a disk, it is always considered a full snapshot, containing all the data blocks that have been written to the original disk at the time that snapshot was created.

Subsequent snapshots, in an impressive way, are incremental versions of the original snapshot. They do not require re-storing all the data on the source disk, but instead focus on backing up new and changed data blocks since the previous snapshot was created. It is important to note that the size of a full snapshot does not depend on the size of the source disk, but rather on the size of the data you are backing up. For example, if you create the first snapshot from a 200 GB disk but only contains 50 GB of data, the full snapshot will be 50 GB in size and you will only be charged for the storage of that 50 GB snapshot.

Similarly, the size and storage cost of subsequent incremental snapshots will be based on the size of the new data that has been written to the disk since the previous snapshot was created. Continuing the example above, if you create a second snapshot for the 200 GB disk after changing 20 GB of data and adding 10 GB of data, the incremental snapshot will be 30 GB in size. You will then be charged for the storage of that additional 30 GB snapshot.

**Let's consider a disk with a capacity of 25 GB:**

* **State 1**: The disk contains 20 GB of data. Snap 1 is the first snapshot of the disk. Snap 1 is a full snapshot, and all 20 GB of data are backed up.
* **State 2**: The disk still contains 20 GB of data, but only 5 GB has changed since Snap 1 was taken. Snap 2 is an incremental snapshot. It only needs to back up the 5 GB that has changed. The other 15 GB of unchanged data, which was already backed up in Snap 1, is referenced by Snap 2 instead of being backed up again.
* **State 3**: 2 GB of data has been added to the disk, for a total of 22 GB, after Snap 2 was taken. Snap 3 is an incremental snapshot. It only needs to back up the 2 GB that was added after Snap 2 was taken. Snap 3 also references the 5 GB of data stored in Snap 2 and the 15 GB of data stored in Snap 1.

The total storage required for the three snapshots at stage 3 (the final stage) is a total of 27 GB. This is comprised of 20 GB for Snap 1, 5 GB for Snap 2, and 2 GB for Snap 3.

In this way, you have created a chain of incremental snapshots, each snapshot containing only the changes since the previous snapshot, saving storage space and making data backup and recovery more efficient.

<figure><img src="/broken/files/EIG6BLHhOZhUEUbyKXDk" alt=""><figcaption></figcaption></figure>

***

## UseCase

**Data Storage & Recovery**

Snapshots are commonly used to protect critical data from loss. By creating periodic snapshots, you can restore data to a state before a system crash or data deletion.

**Development and Testing**

When working in a development or testing environment, snapshots can be used to create backups of the current environment. You can then use this snapshot to deploy a similar environment or to test changes without affecting the main environment.

**Switching Environments**

Snapshots can help you easily switch data in case you want to migrate data or applications between different environments. For example, you can migrate data from a development environment to a production environment.

***

## Start with Snapshot

To use Snapshot, you need to activate the Snapshot on our dashboard. Please refer to the [Activate Snapshot](activate-snapshot.md) guide.
