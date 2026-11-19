---
hidden: true
---

# Migrate Instance

## What is a server migration? <a href="#vngcloudsvirtualservermigrationservice-whatisaservermigration" id="vngcloudsvirtualservermigrationservice-whatisaservermigration"></a>

GreenNode provides automation of data migration of VMs and Volume virtual disks. The system will gradually clone your host virtual machine as an image, which will then migrate the host location from **QTSC** to **HCM-03-1A**, which usually involves one or more hosts, depending on the configuration of the host. Performing monitoring on the interface, you can easily check and update the health of your servers before deciding to deploy to migrate them.

### Server migration process <a href="#vngcloudsvirtualservermigrationservice-servermigrationprocess" id="vngcloudsvirtualservermigrationservice-servermigrationprocess"></a>

By using the vServer Portal visual manager to manage server migrations, you can:

* **Simplify the migration process by copying original data**. You can start migrating a server fleet by visiting our vServer Portal at [{link}](https://hcm-3.console.greennode.ai/vserver/v-server/cloud-server). For the first time, the interface will display a list of servers with **Ready to migrate** status, you need to select servers you want to migrate then click **Migrate to HCM-03-1A**, the execution will begin. After the migration begins, GreenNode manages all the complex elements of the migration process, including automatically copying the original data of the servers and creating new images periodically. What you need to do now is monitor the progress of the migration and wait until this stage is completed.
* **Launch the server on HCM-03-1A in the control panel:** After completing the original data replication phase, the status of the server will change to **Ready to switch**, with the support of incremental replication, GreenNode allows you to quickly launch virtual servers without having to wait to minimize downtime, Limit business impact related to application downtime during the final transition. Now what you need to do is select the server and click **Shutdown**, then when the server is turned off, select **Switch to HCM-03-1A** to start the server on the new location.
* **Check server health and confirm migration:** Once you've actually migrated data from one server to another, it's time to experiment. A fully functional test and complete data transmission can be time-consuming and cumbersome, but it's a reasonable amount of time to avoid detecting a problem at a later date. Select the server and check its status after data migration, if everything is still working normally and efficiently, click **Confirm final migration** to complete your data migration, at which point the system will erase all virtual server data in QTSC, otherwise select **Back to QTSC** to cancel the data migration process, everything will return to its original state.

Data migration may experience some limitations as follows:

* You may have to spend some time waiting for the migration to complete.
* Data after migration may be lost or out of sync, but this is a rare occurrence.

### How long does the server migration take? <a href="#vngcloudsvirtualservermigrationservice-howlongdoestheservermigrationtake" id="vngcloudsvirtualservermigrationservice-howlongdoestheservermigrationtake"></a>

A typical server migration can take anywhere from 2 minutes to 3 hours, with speeds averaging at 200 Mb/s. This is because the time spent on the server migration will depend a lot on the amount of data transferred, the magnitude of the data. The server only has a certain amount of bandwidth to meet tasks like this. As you increase the number of files and applications moved, the process takes up more server bandwidth – ultimately taking longer to complete.

### Cost <a href="#vngcloudsvirtualservermigrationservice-cost" id="vngcloudsvirtualservermigrationservice-cost"></a>

There is no fee to use Server Migration Service, we always want to bring the best experience to GreenNode customers.

### Why consider migrating hosts? <a href="#vngcloudsvirtualservermigrationservice-whyconsidermigratinghosts" id="vngcloudsvirtualservermigrationservice-whyconsidermigratinghosts"></a>

Several possible scenarios may make a server migration necessary:

* Take advantage of new technology or better services, or ensure that operating systems (OS) and hardware based on new technology are always up to date.
* Move to new locations for increased flexibility or scalability.
* To save and consolidate hosting services.
* Replace aging infrastructure at the end of its life cycle.
* Hosting expansion and distribution reduces load at a single point and achieves high availability.

<br>
