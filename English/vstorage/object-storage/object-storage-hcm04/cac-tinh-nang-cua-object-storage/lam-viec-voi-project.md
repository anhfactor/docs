# Working with project

After you successfully complete the above steps, the automatic renewal feature for the project has been turned off.

1. Log in to [https://vstorage.console.greennode.ai](https://vstorage.console.greennode.ai/storage/list) .
2. Select the icon ![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FEedDoSjQC1v0i4G6OKT6%252Fimage.png%3Falt%3Dmedia%26token%3D5270bd91-5976-4b49-9747-6c848e043f7e\&width=32\&dpr=4\&quality=100\&sign=e2bdf3ba\&sv=2)in **the project** you want to disable auto-renew. Select **Disable Auto-renew.**
3. **The Disable Auto-renew** screen is displayed **.**
4. Select **OK.**

## Overview <a href="#tong-quan" id="tong-quan"></a>

A Project is a term on vStorage that represents a storage package with a specific capacity that you purchase on GreenNode. <mark style="color:red;">**With Region HCM04, at a time you can own up to 10 Projects and use them to organize your data storage.**</mark>

***

## **Project scope** <a href="#pham-vi-gioi-han-project" id="pham-vi-gioi-han-project"></a>

### **Project naming rules**

The following rules apply to project naming in vStorage:

* Project name must be between 1 (minimum) and 40 (maximum) characters long.
* Project names can only contain uppercase and lowercase letters (a-z, A-Z), numbers (0-9), periods (.), spaces ( ), underscores (\_), hyphens (-), and the @ character.
* Project names should not contain sensitive information (e.g. IP addresses, account names, login passwords, etc.).
* The project name must be unique across a GreenNode account within or across regions until the project is deleted. We recommend that your business project or product name be used as the name of the project stored in vStorage.

### **Example**

* The following example project names are valid and follow the recommended naming guidelines:
  * project du an 1
  * project-2022
  * ...
* The following example project names are valid but we do not recommend using them:
  * [docexamplewebsite.com](http://docexamplewebsite.com/)
  * [www.docexamplewebsite.com](http://www.docexamplewebsite.com/)
  * ...
* The following example project names are invalid:
  * Project efficiency 80% (contains %)
  * project\_1/2022 (contains / character)
  * ...

***

## Create a project <a href="#khoi-tao-project" id="khoi-tao-project"></a>

Create a project by following the steps below:

1. Log in to [https://vstorage.console.greennode.ai](https://vstorage.console.greennode.ai/storage/list) . If you don't have an account, register for free [here](https://register.vngcloud.vn/signup) .
2. Select **Region HCM04.**
3. Select **Create a Project.**
4. Enter **Project Name**
5. Select the appropriate **Billing method** according to your needs. We will provide you with 2 types **Pay monthly** and **Pay as you go**.
6. Select the appropriate **Project type** (package) according to your needs. Region HCM04 offers the **Gold** and **Instant Archive** packages. Free traffic equals 10 times (Gold) or 2 times (Instant Archive) the Quota you choose, and requests are completely free. For more information on pricing, please refer to [Pricing.](../../cach-tinh-phi.md)
7. Select **the Quota** (storage capacity) you want.
8. Select **Period** and check/uncheck **Auto-renew** according to your needs.
9. **Go through the Checkout** steps and your **Project** will be created.

<figure><img src="../../../../.gitbook/assets/image (105).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (133).png" alt=""><figcaption></figcaption></figure>

***

## View project information <a href="#xem-thong-tin-project" id="xem-thong-tin-project"></a>

You can view and use properties for the project including general project information, generated S3 key pairs, auto-scaling configuration if any, impact history as well as project connection information to S3,...

To view the properties for a project, you can:

1. Log in to [https://vstorage.console.greennode.ai/storage](https://vstorage.console.greennode.ai/storage/list) .
2. Select **Region: HCM04**
3. Select the icon ![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FUezdPyPY1knPTFpXbLOa%252Fimage.png%3Falt%3Dmedia%26token%3Df6613ac8-8cb7-4055-91fe-8676327c00ae\&width=40\&dpr=4\&quality=100\&sign=66c02356\&sv=2)in **the project** you want to see details.
4. **On the project** details page , you can view and use properties for the project.

* **Information** : Provides general project information such as Total quota, Total usage, Project type, Account URL, Project Owner.
* **S3 key** : Provides information about S3 key pairs that are initialized for the project from vStorage Portal. To initialize S3 key, please refer here.
* **History** : Provides historical information affecting the project including action type, action status, time the action occurred, and a detailed description of the action if available.
* **Connection Information** : Provides commands and configuration files to connect the project to S3.

<figure><img src="../../../../.gitbook/assets/image (25) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

***

## Resize a project <a href="#tang-giam-han-muc-project" id="tang-giam-han-muc-project"></a>

You have initialized the project with an initial quota that matches your storage needs. Now your business needs have changed and the old capacity cannot meet them. To solve this problem, you can change the storage quota through the Change Quota feature that we provide.

To change the quota for a project, you can:

1. Log in to [https://vstorage.console.greennode.ai](https://vstorage.console.greennode.ai/storage/list) .
2. Select the checkbox at the project you want to increase or decrease the limit and select the icon ![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FklArErUf8YJCZgjw6j8E%252Fimage.png%3Falt%3Dmedia%26token%3D8bf06cfe-52c0-4060-837b-caa420fea819\&width=41\&dpr=4\&quality=100\&sign=cc455acd\&sv=2)or you can also select the icon ![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FrxitUMM9JIncMgn4JDAK%252Fimage.png%3Falt%3Dmedia%26token%3D7baaf770-23ce-478c-816f-bd324ab4ddee\&width=27\&dpr=4\&quality=100\&sign=4695600d\&sv=2)then select Resize.
3. **The Resize project** screen is displayed **.** Select the storage **quota you want to increase, the storage quota** you can increase or decrease to the maximum or minimum **quota** provided by the hosting package. You cannot adjust the storage **quota** to be smaller or larger than this value.
4. Select **Resize project.**
5. Select **Checkout** after reviewing your shopping cart and payment method.
6. Select **Continue to checkout** and make payment after choosing the appropriate payment method.

After you successfully complete the above 6 steps, the new total **quota** value after change will be updated on the general information of the project you selected.

<figure><img src="../../../../.gitbook/assets/image (26) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

***

## Renew a project <a href="#gia-han-project" id="gia-han-project"></a>

You have started your project with a short retention period. Now your business needs have changed and you want to increase this retention period. To solve this problem, you can change the retention period through the renew feature we provide.

To renew a project, you can:

1. Log in to [https://vstorage.console.greennode.ai](https://vstorage.console.greennode.ai/storage/list) .
2. Select the checkbox at **the project** you want to increase or decrease the limit and select the icon ![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F1HTMWIvPjqwnOkYKUU7v%252Fimage.png%3Falt%3Dmedia%26token%3De30c9175-97b4-4ab3-8645-57e51c206768\&width=38\&dpr=4\&quality=100\&sign=92bed989\&sv=2)or you can also select the icon ![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FrxitUMM9JIncMgn4JDAK%252Fimage.png%3Falt%3Dmedia%26token%3D7baaf770-23ce-478c-816f-bd324ab4ddee\&width=27\&dpr=4\&quality=100\&sign=4695600d\&sv=2)then select **Renew** .
3. Select the desired storage period to renew. We offer storage periods of **1 month, 3 months, 6 months, 12 months, 24 months, 36 months . When you select a renewal period, the system will automatically calculate the effective time of the new storage period and the total amount you need to pay for project** renewal .
4. Select **Checkout** after reviewing your shopping cart and payment method.
5. Select **Continue to checkout** and make payment after choosing the appropriate payment method.

After you successfully complete the above 5 steps, the new retention period after project renewal will be updated on the general information of the project you selected.

***

## Auto-renew a project <a href="#gia-han-tu-dong-project" id="gia-han-tu-dong-project"></a>

In addition to manually renewing a project, we also support you to set up automatic renewal through the Auto-renew feature.

The automatic renewal feature is a system feature that supports automatic renewal of expired services more easily for prepaid customers. Customers do not need to worry about when the service expires to access the vStorage Portal to renew, pay,...

7 days before the service expires, the system will send an email notification about the automatic service renewal. During these 7 days, you will receive 1 notification email each day.

The system will automatically renew 3 days before the service expires:

* If you have enough credits, all services will be renewed. When the renewal is successful or failed, we will send you an email containing information about the successful/failed renewal. The service renewal payment history will also be stored on the vConsole system. For more information, visit [the vConsole Dashboard](https://dashboard.console.greennode.ai/payment-history) .
* If there are not enough credits, the system will try to renew the services until there are no more credits. When the renewal is successful or failed, we will send you an email containing the successful/failed renewal information. The service renewal payment history will also be stored on the vConsole system. For more information, visit the vConsole [Dashboard](https://dashboard.console.greennode.ai/payment-history) .

<details>

<summary>Set up auto-renewal when creating a project</summary>

1. Follow the steps to initialize the project as instructed in [Initializing the project](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vstorage/object-storage/vstorage-hcm03/cac-tinh-nang-cua-vstorage/lam-viec-voi-project/khoi-tao-project) .
2. At the time of setting up information about the project to be purchased, select **Auto Renew** .
3. Select **the automatic renewal cycle** . We offer renewal cycles including: 1 month, 3 months, 6 months, 12 months, 24 months, 36 months. When you select the renewal cycle, the system will automatically calculate the validity period of the new storage cycle and the total amount you need to pay for the **project** renewal .

For a list of vStorage payment types and how project renewals are charged, see [Charging Fee](../../cach-tinh-phi.md).

After you successfully complete the above steps, the new retention period after project renewal will be updated on the general information of the project you selected.

</details>

<details>

<summary>Set up auto-renewal on previously created projects</summary>

1. Log in to [https://vstorage.console.greennode.ai](https://vstorage.console.greennode.ai/storage/list) .
2. Select the icon ![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FK4egjGi7BcVc4LoWfjmV%252Fimage.png%3Falt%3Dmedia%26token%3D5b4d93e0-8bd9-4970-a85e-e3564c780054\&width=40\&dpr=4\&quality=100\&sign=4fa90d8e\&sv=2)at **the project** you want to perform auto-renew setup. Select Enable Auto-renew.
3. **The Enable Auto-renew** screen is displayed **.** Select the renewal **Period** you want.
4. Select **OK.**

After you successfully complete the above steps, the new retention period after project renewal will be updated on the general information of the project you selected.

</details>

<details>

<summary>Remove auto-renewal on a project that was previously set to auto-renewal</summary>

1. Log in to [https://vstorage.console.greennode.ai](https://vstorage.console.greennode.ai/storage/list) .
2. Select the icon ![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FEedDoSjQC1v0i4G6OKT6%252Fimage.png%3Falt%3Dmedia%26token%3D5270bd91-5976-4b49-9747-6c848e043f7e\&width=32\&dpr=4\&quality=100\&sign=e2bdf3ba\&sv=2)in **the project** you want to disable auto-renew. Select **Disable Auto-renew.**
3. **The Disable Auto-renew** screen is displayed **.**
4. Select **OK.**

After you successfully complete the above steps, the automatic renewal feature for the project has been turned off.

</details>

***

## Delete project <a href="#xoa-project" id="xoa-project"></a>

You have created a project with the appropriate hosting package. Now your business needs have changed and you no longer need the project. We recommend that you delete the project to optimize costs.

To delete a project, you can:

1. Log in to [https://vstorage.console.greennode.ai](https://vstorage.console.greennode.ai/storage/list) .
2. Select the icon ![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FkcyUBgpsSXeMN2pcVWWi%252Fimage.png%3Falt%3Dmedia%26token%3D94a5949b-5b8c-4780-9b32-9fa7175fab46\&width=21\&dpr=4\&quality=100\&sign=f4d132ff\&sv=2)in the project you want to delete. Select **Delete** .
3. Enter the string **delete me** and select **Delete.**

After you delete the project, the deleted project will disappear from your project list. At this time, the deleted project will be in **the Trash** , your deleted project will be stored in **the Trash** for 7 days without any charge. During these 7 days, you can restore the deleted project. To restore, see the instructions in the Restore project section. If after 7 days you do not restore the project, the project and all data inside will be completely deleted from the system and cannot be restored.

If you delete a project before the initial retention period, we will refund you, and if you restore a project, we will also charge you a restore fee. For details on how vStorage charges for project refunds and restores, see How it's Charged.

Because deleting a project is risky, we recommend that you consider carefully and create a backup version of the project before deleting it.

***

## Auto-scale Quota <a href="#tang-dung-luong-tu-dong-auto-scale-quota" id="tang-dung-luong-tu-dong-auto-scale-quota"></a>

The Auto-scale Quota feature in vStorage allows you to set up automatic storage expansion based on your usage and needs. This guide will provide details on how to configure and manage this feature through the vStorage Portal.

To set up automatic growth for a project, you can:

1. Log in to [https://vstorage.console.greennode.ai](https://vstorage.console.greennode.ai/storage/list) .
2. In the project that needs to set Auto-scale Quota, select the icon ![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2Fdocs.vngcloud.vn%2F%7Egitbook%2Fimage%3Furl%3Dhttps%253A%252F%252F3672463924-files.gitbook.io%252F%257E%252Ffiles%252Fv0%252Fb%252Fgitbook-x-prod.appspot.com%252Fo%252Fspaces%25252FB0NrrrdJdpYOYzRkbWp5%25252Fuploads%25252Fxle5SMO5J6MplFpJZC74%25252Fimage.png%253Falt%253Dmedia%2526token%253De9cdb754-9a75-4868-90bf-67e670048eb5%26width%3D27%26dpr%3D4%26quality%3D100%26sign%3D1f9a3808%26sv%3D1\&width=27\&dpr=4\&quality=100\&sign=66330d1\&sv=2)then select **Auto-scale** and continue to select **Configure Auto-scale** or select the icon ![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2Fdocs.vngcloud.vn%2F%7Egitbook%2Fimage%3Furl%3Dhttps%253A%252F%252F3672463924-files.gitbook.io%252F%257E%252Ffiles%252Fv0%252Fb%252Fgitbook-x-prod.appspot.com%252Fo%252Fspaces%25252FB0NrrrdJdpYOYzRkbWp5%25252Fuploads%25252Fs6DACNvZx3OSJhJDO654%25252Fimage.png%253Falt%253Dmedia%2526token%253D3164ca6e-fc29-4fd0-b88a-34a960d4cde0%26width%3D29%26dpr%3D4%26quality%3D100%26sign%3Daa473973%26sv%3D1\&width=29\&dpr=4\&quality=100\&sign=6440465f\&sv=2)then select **Set Auto-scale**.
3. **At the Auto-scale** configuration screen , set up the necessary parameters for **Auto Scale**. Specifically:

* **Set Quota Unit:** you can choose 1 of 2 types of units including **GB** or **Percent**.
* **Set Quota Threshold or Quota Remain:** If you choose **Quota Unit** as **Percent** , here you will enter the percentage of usage threshold that when reached will trigger the quota increase. If you choose **Quota Unit** as **GB** , here you will enter the remaining quota that when reached will trigger the quota increase.
* **Set Quota Increment Level** : enter desired increment level in **GB** or **Percent**.

1. **Choose to receive email** notification when quota increase is successful if desired.
2. Enable **Auto-scale** at the icon ![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2Fdocs.vngcloud.vn%2F%7Egitbook%2Fimage%3Furl%3Dhttps%253A%252F%252F3672463924-files.gitbook.io%252F%257E%252Ffiles%252Fv0%252Fb%252Fgitbook-x-prod.appspot.com%252Fo%252Fspaces%25252FB0NrrrdJdpYOYzRkbWp5%25252Fuploads%25252FjlLW0mG9Z7he3tym9yeH%25252Fimage.png%253Falt%253Dmedia%2526token%253D247a3e39-731f-4fdb-a2f4-08b6bf8bbf2d%26width%3D64%26dpr%3D4%26quality%3D100%26sign%3D44906aa4%26sv%3D1\&width=64\&dpr=4\&quality=100\&sign=f80a3317\&sv=2). When this icon becomes , ![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2Fdocs.vngcloud.vn%2F%7Egitbook%2Fimage%3Furl%3Dhttps%253A%252F%252F3672463924-files.gitbook.io%252F%257E%252Ffiles%252Fv0%252Fb%252Fgitbook-x-prod.appspot.com%252Fo%252Fspaces%25252FB0NrrrdJdpYOYzRkbWp5%25252Fuploads%25252FVGMWqFlP5OOPvrycdMrg%25252Fimage.png%253Falt%253Dmedia%2526token%253D94d216a5-2e33-489e-884d-f837683920c6%26width%3D59%26dpr%3D4%26quality%3D100%26sign%3D38683327%26sv%3D1\&width=59\&dpr=4\&quality=100\&sign=a00223b5\&sv=2)it means you have successfully enabled **Auto-scale.**

{% hint style="info" %}
**Attention:**

* **The vStorage system will perform a 5-minute** auto-scaling check to automatically increase capacity based on the set threshold.
* The price is applied according to the **standard vStorage** price list , the feature only increases capacity without changing the Storage Class.
* Users need to ensure that they have **sufficient credit balance** for their account (prepaid) before performing Auto-scaling.
* If the capacity increase **fails** , the user will receive an email notification. After two consecutive auto-scaling failures, our system will stop sending email notifications to you. You need to proactively access vStorage to manually resize the project according to the instructions above.
{% endhint %}

<figure><img src="../../../../.gitbook/assets/Screenshot from 2026-05-04 13-45-11.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/Screenshot from 2026-05-04 13-45-24.png" alt=""><figcaption></figcaption></figure>

***

## Usage alert <a href="#canh-bao-dung-luong-usage-alert" id="canh-bao-dung-luong-usage-alert"></a>

The **Usage alert** feature in vStorage allows you to set up automatic alert based on your usage and needs. This guide will provide details on how to configure and manage this feature through the vStorage Portal.

To set up automatic alert for a project, you can:

1. Log in to [https://vstorage.console.greennode.ai](https://vstorage.console.greennode.ai/storage/list).
2. In the project that needs to set Usage alert, select the icon <img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fxle5SMO5J6MplFpJZC74%252Fimage.png%3Falt%3Dmedia%26token%3De9cdb754-9a75-4868-90bf-67e670048eb5&#x26;width=27&#x26;dpr=4&#x26;quality=100&#x26;sign=1f9a3808&#x26;sv=1" alt="" data-size="line"> then select **Usage alert** and continue to select **Configure Usage alert**.
3. At the **Usage alert** configuration screen , set up the necessary parameters for **Usage alert**. Specifically:

* Set **Quota Unit:** you can choose 1 of 2 types of units including **GB** or **Percent**.
* Set **Quota Threshold** or **Quota Remain:** If you choose **Quota Unit** as **Percent** , here you will enter the percentage of usage threshold that when reached will trigger the usage alert. If you choose **Quota Unit** as **GB** , here you will enter the remaining quota that when reached will trigger the usage alert.

4. Enable **Usage alert** at the icon <img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FjlLW0mG9Z7he3tym9yeH%252Fimage.png%3Falt%3Dmedia%26token%3D247a3e39-731f-4fdb-a2f4-08b6bf8bbf2d&#x26;width=64&#x26;dpr=4&#x26;quality=100&#x26;sign=44906aa4&#x26;sv=1" alt="" data-size="line">. When this icon becomes <img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FVGMWqFlP5OOPvrycdMrg%252Fimage.png%3Falt%3Dmedia%26token%3D94d216a5-2e33-489e-884d-f837683920c6&#x26;width=59&#x26;dpr=4&#x26;quality=100&#x26;sign=38683327&#x26;sv=1" alt="" data-size="line">it means you have successfully enabled **Usage alert.**
5. Click **Manage your notification recievers** if you want to set up additional email lists to receive alerts.

{% hint style="info" %}
**Attention:**

* **The vStorage system will perform a 2-times per day** usage alert check to automatically alert usage based on the set threshold.
{% endhint %}

<figure><img src="../../../../.gitbook/assets/Screenshot from 2026-05-04 13-45-47.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/Screenshot from 2026-05-04 13-45-57.png" alt=""><figcaption></figcaption></figure>

***

## Create a POC project <a href="#thuc-hien-poc-project" id="thuc-hien-poc-project"></a>

When you are a user on the vStorage system, by default you will not be able to perform POC projects. POC is a program that helps customers experience the service through the value (in credit in the POC wallet) provided by GreenNode to customers. Normally, POC wallets will be granted through promotional programs, promotional campaigns of GreenNode. Thereby, customers can experience creating certain services within a specified period of time. To perform POC projects, please contact the Sales staff or the staff who directly supports you or open a support ticket on our system. The POC wallet granted has a certain value and is used within a specified period of time depending on the company's policy. After the validity period expires, you can request to extend the POC wallet's usage period or pay an additional fee to maintain the service.

Once we confirm that we have provided a POC wallet to your account, to use the POC wallet please follow the instructions below:

<details>

<summary>Create a project using POC wallet balance</summary>

1. Log in to [https://vstorage.console.greennode.ai](https://vstorage.console.greennode.ai/storage/list) .
2. Select **region HCM04.**
3. Select **Create a project.**
4. **The Create New Project** screen is displayed. In **Project Name** , enter a name that complies with our regulations for your project.
5. Choose a hosting **Quota** according to your needs. Quota is the maximum hosting package size you can create. For each hosting package, we have provided a minimum and maximum size so you can choose to change based on your actual needs.
6. **Turn off the Enable auto-renewal** option. Now we show the **PoC** option.
7. Select **PoC** .
8. Select **Create a project.**
9. Select **Checkout PoC** after reviewing your cart information.

After you complete the 9 steps described above, your project has been created through the payment method of POC wallet. This **project** has the prefix **\[POC]. By default, this project will have a start date as the project creation time and an end date as the expiration date of the POC wallet you were provided.**

The default POC resource usage time coincides with the POC wallet expiration time. We only support you to use the POC wallet to pay for POC resources. For POC resources, the price of POC resource usage is calculated similarly to that of regular resources. For more details, please refer to How to calculate fees.

</details>

<details>

<summary>Renew a project using POC wallet</summary>

After you create a project using POC wallet, you can continue to extend the project using Poc wallet. For details, follow these steps:

1. Log in to [https://vstorage.console.greennode.ai](https://vstorage.console.greennode.ai/storage/list) .
2. Select the icon ![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FygA5fq4dzy9Rq5tPOgx2%252Fimage.png%3Falt%3Dmedia%26token%3D721a82c5-eb44-4657-9af9-82d2129a5c2d\&width=22\&dpr=4\&quality=100\&sign=856d143c\&sv=2)at **the project** you want to renew. Select **Renew.**
3. **You can extend the project using POC wallet if you have extended the POC wallet usage period. After you extend the POC wallet usage period, the time you can extend the project is the period from the current end date to the new expiration date of the POC wallet** . To extend the POC wallet usage period, please contact the Sales staff or the staff who directly supports you or open a support ticket on our system. Select **Extend**.
4. Select **Checkout PoC** .

Once you complete the 4 steps described above, your project has been renewed via the POC wallet payment method.

The process and pricing method are similar to regular project extensions. For more details, please refer to How to calculate fees.

</details>

<details>

<summary>Delete project using POC wallet</summary>

After you initialize a project using POC wallet, if you no longer need to use this project, you can delete it according to the instructions at Delete project.

Now the **project will be completely remove** from vStorage.

</details>

<details>

<summary>Stop POC a project</summary>

1. Log in to [https://vstorage.console.greennode.ai](https://vstorage.console.greennode.ai/storage/list) .
2. Select the icon ![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F7MKwglc67piWKdxGb7Jc%252Fimage.png%3Falt%3Dmedia%26token%3Dc06c8276-677f-4192-8a54-20bc35c657c7\&width=25\&dpr=4\&quality=100\&sign=c1b8c293\&sv=2)at **the project** you want to stop POC. Select **Stop POC**.
3. Select **Stop POC** .

Once you successfully stop the POC, your project will be converted to a prepaid resource type with expired status.

* If you really don't need to use this project anymore, you can completely delete the project from our system following the instructions at Delete project.
* **If you want to renew this expired project to continue using it, follow the instructions to Renew Project. When renew a project that has just been stopped from POC, you need to select a new renewal cycle and make a payment with your real money (credit wallet balance, Momo wallet, Zalopay wallet,...).**
* You also cannot enable POC usage after you have performed POC Stop. If you have any problems at this point, please contact your Sales or support staff directly or open a support ticket on our system.

</details>

<details>

<summary>POC implementation deadline expired</summary>

At the time of POC wallet expiry, we will:

* **Stop the POC** for all POC resources in use. The process is similar to when you actively stop the POC on a resource.
* **Disable POC wallet** : you will not be allowed to use resources in POC form until the POC wallet is enabled again.

</details>

***

## Create a trial project <a href="#thuc-hien-trial-project" id="thuc-hien-trial-project"></a>

Currently, with region HCM04 we do not support you to create trial project..
