# Working with S3 Keys

## **Overview** <a href="#tong-quan" id="tong-quan"></a>

On the vStorage system, S3 key is a key pair including access key and secret key integrated by vStorage and compatible with S3 client tools such as s3cmd, s3 SDK,...

***

## Root User Account creates a S3 keys <a href="#root-user-account-khoi-tao-s3-keys" id="root-user-account-khoi-tao-s3-keys"></a>

To initialize an S3 key, follow the instructions below:

1. Log in to [https://vstorage.console.greennode.ai with ](https://vstorage.console.greennode.ai/storage/list)<mark style="background-color:orange;">Root User Account</mark> .
2. Select **Region HCM04.**
3. Select the icon ![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FzBejUW7ARqXZMMLNJPI2%252Fimage.png%3Falt%3Dmedia%26token%3D67d600f9-d645-434f-b403-be01af3603e0\&width=37\&dpr=4\&quality=100\&sign=46e8d333\&sv=2)in the project you just created and then select **Identity and Access Management.**
4. Under **List of S3 keys of this project** , select **Generate S3 key** .
5. Select **Copy** or **Download** to download the Access Key/Secret Key information you just generated.

<figure><img src="../../../../.gitbook/assets/image (23) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (24) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Attention:**

* After clicking to create S3 key, you need to **save the Access Key/Secret Key pair** for use. If you do not save it now, you will not be able to get the Secret Key of this Access Key later.
* <mark style="background-color:orange;">The S3 key initialized by</mark> <mark style="background-color:orange;">**the Root User Account**</mark> <mark style="background-color:orange;">will have full access/operation rights on the buckets of this project.</mark>
{% endhint %}

***

## IAM User Account creates a S3 keys <a href="#iam-user-account-khoi-tao-s3-keys" id="iam-user-account-khoi-tao-s3-keys"></a>

To initialize an S3 key, follow the instructions below:

1. Log in to [https://vstorage.console.greennode.ai](https://vstorage.console.greennode.ai/storage/list) with your <mark style="background-color:orange;">IAM User Account</mark> .
2. Select **Region HCM04.**
3. Select the icon ![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FzBejUW7ARqXZMMLNJPI2%252Fimage.png%3Falt%3Dmedia%26token%3D67d600f9-d645-434f-b403-be01af3603e0\&width=37\&dpr=4\&quality=100\&sign=46e8d333\&sv=2)in the project you just created and then select **Identity and Access Management.**
4. Under **List of S3 keys of this project** , select **Generate S3 key** .
5. Select **Copy** or **Download** to download the Access Key/Secret Key information you just generated.

<figure><img src="../../../../.gitbook/assets/image (25) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (26) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Attention:**

* After clicking to create S3 key, you need to **save the Access Key/Secret Key pair** for use. If you do not save it now, you will not be able to get the Secret Key of this Access Key later.
* <mark style="background-color:orange;">S3 keys created by</mark> <mark style="background-color:orange;">**IAM User Account**</mark> <mark style="background-color:orange;">will have full access/operation rights on buckets/objects according to the permissions of that IAM User Account. For example, if your IAM User Account only has Read Object permission, then S3 keys created by this IAM User Account will also only have Read Object permission.</mark>
{% endhint %}

***

## Work with the S3 API (or 3rd party software) via S3 keys <a href="#thuc-hien-lam-viec-voi-s3-api-hoac-3rd-party-software-thong-qua-s3-keys" id="thuc-hien-lam-viec-voi-s3-api-hoac-3rd-party-software-thong-qua-s3-keys"></a>

### Connect 3rd party softwares to vStorage <a href="#ket-noi-3rd-party-softwares-voi-vstorage" id="ket-noi-3rd-party-softwares-voi-vstorage"></a>

After you have successfully initialized the project and initialized the S3 key, you can now use 3rd party softwares to connect and work with your project. The 3rd party softwares you can choose to use can be S3cmd, Cyberduck, Rclone, S3 Browser, MinIO Client,... In this document, we will guide you to connect S3 Browser with vStorage. S3 Browser is an optimized tool that allows you to share and upload your files. This tool has a relatively simple interface, is easy to use and is compatible with the API of the vStorage storage service.

To integrate the S3 Browser tool with vStorage, you can follow the instructions below:

1. Download the S3 Browser user tool here [https://s3browser.com/download.aspx](https://s3browser.com/download.aspx) .
2.  Open the S3 Browser app **.** Select the Account folder, **then select Add new account**

    <figure><img src="../../../../.gitbook/assets/image (439).png" alt="" width="295"><figcaption></figcaption></figure>
3. The Add New Account screen appears, now you enter the following information:

* **Display name:** Display name of the account. Example: Demo\_HCM04
* **Account type** : Select **S3 Compatible Storage.**
* **REST Endpoint** : Path to vstorage, for Region HCM04 the path is [hcm04.vstorage.vngcloud.vn](http://hcm04.vstorage.vngcloud.vn/)
* **Access Key ID & Secret Access Key:** This is the S3 key pair you generated in step 2 earlier.

4. Select the **Use Secure transfer (SSL/TLS)** option because vStorage only supports encrypted transmission channels (HTTPS, port 443) to ensure data security, vStorage currently does not support unencrypted transmission channels (HTTP, port 80).
5. Select **Add new account.**

<figure><img src="../../../../.gitbook/assets/image (440).png" alt=""><figcaption></figcaption></figure>

6. When the connection is successful, the S3 Browser screen will display as follows:

<figure><img src="../../../../.gitbook/assets/image (442).png" alt=""><figcaption></figcaption></figure>

### Use 3rd party softwares to implement features on vStorage <a href="#su-dung-3rd-party-softwares-de-thuc-hien-cac-tinh-nang-tren-vstorage" id="su-dung-3rd-party-softwares-de-thuc-hien-cac-tinh-nang-tren-vstorage"></a>

#### **Basic use cases**

Below are instructions for some common use cases you can perform on S3 Browser:

**Create / Delete bucket**

* Create and delete a bucket by selecting the **New bucket** button . Now enter **the Bucket name** and select **Create new bucket.**

**Upload / Download file**

* After creating a bucket, select the bucket you want to upload/download files to. Next, select **Upload/Download** depending on your upload/download needs.

**Create / Delete Folder**

* You can also create/delete folders by selecting **New Folder** or **Delete** .

<figure><img src="../../../../.gitbook/assets/image (30) (1).png" alt=""><figcaption></figcaption></figure>

#### **Advanced use cases**

Here are instructions for advanced features you can do on S3 Browser:

**ACL**

**ACLs** are a feature on S3 that allows you to control access permissions for each object in your S3 bucket. They define which users or groups of users can access the object and what actions they can perform, such as downloading, uploading, deleting, or overwriting the object.

To set up ACL for a bucket using S3 Browser, right-click on the bucket, then select Edit Permission (ACL). In the permission section, check the permissions you want to grant to the user. For more details, see [https://s3browser.com/share-s3-bucket-edit-acls.aspx](https://s3browser.com/share-s3-bucket-edit-acls.aspx)

<figure><img src="../../../../.gitbook/assets/image (31) (1).png" alt=""><figcaption></figcaption></figure>

**SSE-S3**

SSE-S3 (Server-Side Encryption with S3 Managed Keys) is a server-side data encryption feature provided by Amazon S3. With SSE-S3, your data is automatically encrypted when uploaded to S3 and automatically decrypted when you download it. **To implement this feature on S3 Browser, you need to use S3 Browser Pro version. If your application does not currently support the implementation of the feature, please submit a request to use the feature via a ticket to GreenNode.** For more details, please visit [https://s3browser.com/amazon-s3-server-side-encryption.aspx](https://s3browser.com/amazon-s3-server-side-encryption.aspx)

**SSE-C**

**SSE-C** (Server-Side Encryption with Customer-Provided Keys) is a server-side data encryption feature provided by Amazon S3. Like SSE-S3, SSE-C encrypts your data automatically when it is uploaded to S3 and decrypts it automatically when you download it. However, with SSE-C, you provide and manage your own encryption keys, instead of using keys managed by AWS. **To implement this feature on S3 Browser, you need to use S3 Browser Pro. If your application does not currently support the implementation of the feature, please submit a request to use the feature via a ticket to GreenNode.** For more details, please visit [https://s3browser.com/amazon-s3-server-side-encryption.aspx](https://s3browser.com/amazon-s3-server-side-encryption.aspx)

**Object Locked**

**Object Lock** is a feature that protects your data from being deleted or overwritten for a fixed period of time or indefinitely. It uses the **WORM** (Write Once, Read Many) model, which means that once an object is uploaded to S3 and locked, it cannot be deleted or changed by anyone, including the root user.

To set up Object Locked for a bucket using S3 Browser, when creating a new bucket, you need to select the **Enable S3 Objected Lock option.**

<figure><img src="../../../../.gitbook/assets/image (535).png" alt=""><figcaption></figcaption></figure>

Next, when the bucket is successfully created, right-click on the bucket, then select **Object Locked** . You can set the object locked in both **Retention** (**Compliance mode** only, Governance mode is not supported yet) and **Legal Hold** modes through S3 Browser. For more details, please visit [https://s3browser.com/amazon-s3-object-lock.aspx](https://s3browser.com/amazon-s3-object-lock.aspx)

<figure><img src="../../../../.gitbook/assets/image (33) (1).png" alt=""><figcaption></figcaption></figure>

**Versioning**

Versioning is a feature that supports storing multiple past versions of objects stored in a bucket. You can use versioning to save, retrieve, and restore any version of an object stored in your bucket. When versioning is enabled, when uploading/deleting an object, instead of deleting the object from the system, we will move the deleted or overwritten objects to the versioning version. From there, you can easily restore mistakenly deleted objects or download old versions of data when needed.

To set up Versioning for a bucket using S3 Browser, right-click on the bucket, then select **Edit Versioning Settings** . For more details, see [https://s3browser.com/amazon-s3-versioning.aspx](https://s3browser.com/amazon-s3-versioning.aspx)

<figure><img src="../../../../.gitbook/assets/image (34) (1).png" alt=""><figcaption></figcaption></figure>

**Lifecycle rotation**

**Lifecycle rotation** is a feature that manages the lifecycle of objects in a bucket. This feature allows you to automate actions such as deleting objects after a certain period of time.

To set up Lifecycle rotation for a bucket using S3 Browser, right-click on the bucket, then select **Lifecycle Configuration** . For more details, see [https://s3browser.com/bucket-lifecycle-configuration.aspx](https://s3browser.com/bucket-lifecycle-configuration.aspx)

<figure><img src="../../../../.gitbook/assets/image (35) (1).png" alt=""><figcaption></figcaption></figure>

**Lifecycle transit**

Region HCM04 supports multiple storage classes (**Gold**, **Instant Archive**), so you can use Lifecycle transit to move objects between storage classes. Note: Transition rules are only supported on Pay-as-you-go projects.

**CORS**

CORS (Cross-Origin Resource Sharing) is a security mechanism that allows websites hosted on one domain to access resources from another domain. When you use S3 to host static content and want to access that content from a website hosted on another domain, you need to configure CORS for your S3 bucket.

To set up CORS for a bucket using S3 Browser, right-click on the bucket, then select **CORS Configuration** . For more details, see [https://s3browser.com/s3-bucket-cors-configuration.aspx](https://s3browser.com/s3-bucket-cors-configuration.aspx)

<figure><img src="../../../../.gitbook/assets/image (36) (1).png" alt=""><figcaption></figcaption></figure>

**Public/ Private bucket**

**Public buckets** are a feature that allows users to share buckets publicly in the cloud. Users from outside the internet can access the bucket through a URL without having to authenticate access to the system. Public access poses a security risk, so if your scenario does not require such access, we recommend that you do not enable public access to the bucket. At any point, if you no longer want the bucket to be public, you can make the bucket private.

To set a bucket to public using S3 Browser, right-click on the bucket, then select **Public Access block Configuration** . For more details, see [https://s3browser.com/amazon-s3-public-access-block-configuration.aspx](https://s3browser.com/amazon-s3-public-access-block-configuration.aspx)

<figure><img src="../../../../.gitbook/assets/image (37) (1).png" alt=""><figcaption></figcaption></figure>

**Bucket policy**

**A Bucket Policy** is a type of access policy used to control access to a specific S3 bucket. It allows you to define which users or groups can access the bucket and what operations they can perform, such as uploading, downloading, deleting, or listing objects in the bucket.

To set up a bucket policy using S3 Browser, right-click on the bucket, then select **Edit Bucket Policy** . For more details, see [https://s3browser.com/working-with-amazon-s3-bucket-policies.aspx?v=11.7.5\&fam=x64#amazon-s3-bucket-policies-examples](https://s3browser.com/working-with-amazon-s3-bucket-policies.aspx?v=11.7.5\&fam=x64#amazon-s3-bucket-policies-examples)

<figure><img src="../../../../.gitbook/assets/image (334).png" alt=""><figcaption></figcaption></figure>

***

## Delete S3 keys <a href="#xoa-s3-keys" id="xoa-s3-keys"></a>

To cancel (delete) one or more previously created S3 keys, follow the instructions below:

1. Log in to [https://vstorage.console.greennode.ai with ](https://vstorage.console.greennode.ai/storage/list)Root User Account or IAM User Account .
2. Select region **HCM04**
3. Select the icon ![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FzBejUW7ARqXZMMLNJPI2%252Fimage.png%3Falt%3Dmedia%26token%3D67d600f9-d645-434f-b403-be01af3603e0\&width=37\&dpr=4\&quality=100\&sign=46e8d333\&sv=2)in the project you just created and then select **Identity and Access Management.**
4. In List **of S3 keys of this project** , select **the S3 key** you want to delete and then select **Delete.**

Once the S3 key is successfully cancelled, you will no longer be able to use this S3 key to access vStorage. Be careful when cancelling (deleting) an S3 account as you will not be able to recover this deleted account.

<figure><img src="../../../../.gitbook/assets/image (22) (1).png" alt=""><figcaption></figcaption></figure>
