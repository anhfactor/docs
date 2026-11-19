# Schedule Structure of the Policy

## Daily/Weekly/Monthly combination scheduling structure <a href="#schedulestructureofthepolicy-daily-weekly-monthlycombinationschedulingstructure" id="schedulestructureofthepolicy-daily-weekly-monthlycombinationschedulingstructure"></a>

When the backup object is a virtual machine and a disk, the implementation of the scheduler considers the Policy that coordinates all 3 Daily+Weekly+Monthly to ensure the use-case management of the backup lifecycle of the virtual machine object from short to long term. long-term.

This is realized based on the fact that a virtual machine will have a 1:1 map calendar with the actual calendar realized, where each day under the policy merge convention will mark the base property of the backup date. that day needs to be done

For example, the table below is a description of a calendar with the following rule use-case:

**Daily backup:** the days of the week (daily is the basic backup every day with no special options to add with the backup diff option)

**Weekly backup:** executed on every Sunday due to slow customer service on weekends with the option of full backup

**Monthly backup:** executed on the last Saturday of the last week of any month with the option of full backup

<figure><img src="https://docs.vngcloud.vn/download/attachments/49649830/image2023-3-15_17-59-20.png?version=1&#x26;modificationDate=1678878245000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

**Objectives of implementation:**

Make sure to simplify backup rules by virtual machine object in the same interactive backup rule interface

Reduces risk associated with duplicating backup jobs of the same Volume along with minimizing duplication of same-day backup data
