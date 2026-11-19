# Identity and Access Management (IAM) for vServer

Identity and access management (IAM) for virtual machines is a system for managing and controlling access to virtual machines (VMs) and their resources in a cloud computing environment. It provides a way to control who can access the virtual machine and what actions they can perform on it.&#x20;

Virtual machine IAM typically includes functions such as identity management, authentication, authorization, and auditing. It allows administrators to define policies that specify who can access virtual machines and what actions they can take on virtual machines, such as starting, stopping, or modifying virtual machines.

In a cloud computing environment, IAM for virtual machines is an important security control because virtual machines are often used to store sensitive data and run business-critical applications. By controlling access to these resources, IAM for virtual machines helps ensure the security, integrity, and availability of an organization's data and services.

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802611/image2023-5-17_17-31-9.png?version=1&#x26;modificationDate=1685006577000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

### Overview <a href="#identityandaccessmanagement-iam-forvserver-overview" id="identityandaccessmanagement-iam-forvserver-overview"></a>

You need to complete the following steps to be able to use the IAM service for our vServer product:

***

### **Bước 1: Define your requirements:** <a href="#identityandaccessmanagement-iam-forvserver-buoc1-defineyourrequirements" id="identityandaccessmanagement-iam-forvserver-buoc1-defineyourrequirements"></a>

* Determine the level of access control you need for your server and resources.
* Define the roles and responsibilities of different users or groups of users.
* Define the permissions and privileges required for each user role or group.

***

### **Step 2: Choose the solution and plan the appropriate IAM strategy** <a href="#identityandaccessmanagement-iam-forvserver-step2-choosethesolutionandplantheappropriateiamstrategy" id="identityandaccessmanagement-iam-forvserver-step2-choosethesolutionandplantheappropriateiamstrategy"></a>

* Research and choose the IAM solution that meets your requirements.
* Create a plan to deploy IAM on your servers and resources.
* Define policies for user authentication and authorization.

***

### **Step 3: Create a user account (User account) on the system vIAM** <a href="#identityandaccessmanagement-iam-forvserver-step3-createauseraccount-useraccount-onthesystemviam" id="identityandaccessmanagement-iam-forvserver-step3-createauseraccount-useraccount-onthesystemviam"></a>

After setting up the IAM strategy plan, you need to create a Personal User account on our IAM homepage from your Root user account for each person who needs to access the server:

1. Visit IAM homepage: [click here](https://iam.console.greennode.ai/).
2. Open the **User account** tab
3. Select **Create a user account.**
4. n the **Account user name** field, enter a Name for your User account. User account name must be between 5 and 50 characters long and can only contain letters, numbers, underscore (\_), period (.), dash (-).
5. Enter the password for the User account in the **Account password** section (The password must be between 8 and 50 characters long. The password must contain at least 1 uppercase letter, 1 lowercase letter, 1 number, and 1 special character), need to set up a password. Strong and unique password for each user account.

***

### **Step 4: Set up a Group** <a href="#identityandaccessmanagement-iam-forvserver-step4-setupagroup" id="identityandaccessmanagement-iam-forvserver-step4-setupagroup"></a>

Next you need to create a group of people (Group) based on common roles or responsibilities:

1. Open the **Group tab** at  [https://iam.console.greennode.ai/user-groups](https://iam.console.greennode.ai/user-groups).
2. Select **Create a group.**
3. Enter the Group name in the **Name** field (The name must be from 1 to 50 characters long and can only include letters, numbers, underscores (\_), periods (.), hyphens (-) and spaces. ), then enter the note information in the **Description** field.
4. Go to the next step and assign the appropriate Policy to the user account in the **Policy** section, then assign the appropriate user to the group in the **User** section, with the Users added to the group will have permissions on the selected Policy. in Group

***

### **Step 5: Define access Policies** <a href="#identityandaccessmanagement-iam-forvserver-step5-defineaccesspolicies" id="identityandaccessmanagement-iam-forvserver-step5-defineaccesspolicies"></a>

Create an access policy that specifies what actions each user group or role can take, define detailed permissions to restrict unnecessary access, and regularly review and update access policies. Access when needed:

1. Open the Policy tab at  [https://iam.console.greennode.ai/policies](https://iam.console.greennode.ai/policies).
2. Select **Create a Policy**.
3. Enter the Group name in the Name field (The name must be from 1 to 50 characters long and can only include letters, numbers, underscores (\_), periods (.), hyphens (-) and spaces. ), then enter the note information in the **Description** field.
4. Go to the next step, select the **vserver** product in the **Product** section, then select the list of permissions for your policy in the **Action** section.&#x20;
5. &#x20;Continue to select the resources you want to apply to the selected permissions in the list above in the **Resource** section, here you can choose to all resources or specific resources.
6. Select the necessary conditions to exercise the above rights in the **Request conditions** section.
7. **Create Policy**\
   Then assign the created policies to **User accounts** that match the job functions or responsibilities, assign users to roles based on their job functions, thereby grouping **User accounts** with the same permissions in **Group.**

\


For detailed information and meanings of actions (Actions), resources (Resources), and requirements (Request conditions) to set up a complete set of access policies (Policies), please see the content at [Policy configuration page](actions-resources-and-required-conditions-for-vserver-access-decentralization.md)

***

### **Step 6: Login to vServer by using IAM account (User account)** <a href="#identityandaccessmanagement-iam-forvserver-step6-logintovserverbyusingiamaccount-useraccount" id="identityandaccessmanagement-iam-forvserver-step6-logintovserverbyusingiamaccount-useraccount"></a>

The final step is to use the IAM User Account to access vServer resources via the vServer portal:

1. Access path: [https://dashboard.console.greennode.ai/](https://dashboard.console.greennode.ai/)
2. If you haven't signed in with this browser before, the main sign-in page will appear. **Select SIGN IN WITH IAM USER ACCOUNT**.
3. Enter the email address of the Root user when registering a GreenNode account.
4. Enter the **username** and **password** of the IAM user account (User account) created on the vIAM system.
5. Select **SIGN IN WITH IAM USER ACCOUNT**.\
   If you have previously signed in as an IAM user account in this browser, your browser may remember the IAM user account address. If so, you should see the screen shown in step 3. After successfully logging in with IAM user account, the main screen of vServer will show the type of user you are using to log in (Root user account or IAM user account).

***

### **Bước 7: Truy cập vào vServer sử dụng IAM account (User account)** <a href="#identityandaccessmanagement-iam-forvserver-buoc7-truycapvaovserversudungiamaccount-useraccount" id="identityandaccessmanagement-iam-forvserver-buoc7-truycapvaovserversudungiamaccount-useraccount"></a>

Bước cuối cùng là sử dụng **IAM User Account** truy cập vào tài nguyên vServer qua vServer portal:

1. Truy cập vào đường dẫn: [https://dashboard.console.greennode.ai/](https://dashboard.console.greennode.ai/)
2. Nếu trước đây bạn chưa đăng nhập bằng trình duyệt này, trang đăng nhập chính sẽ xuất hiện. Chọn **ĐĂNG NHẬP VỚI IAM USER ACCOUNT**.
3. Nhập địa chỉ **email** của người dùng Root khi đăng ký tài khoản GreenNode.
4. Nhập **tên người dùng** và **mật khẩu** của tài khoản IAM user account (User account) được tạo trên hệ thống vIAM.
5. Chọn **ĐĂNG NHẬP VỚI IAM USER ACCOUNT**.\
   Nếu trước đó bạn đã đăng nhập với tư cách người dùng IAM user account trong trình duyệt này, thì trình duyệt của bạn có thể nhớ địa chỉ tài khoản IAM user account. Nếu vậy, bạn sẽ thấy màn hình hiển thị ở bước 3. \
   Sau khi đăng nhập thành công với IAM user account, trên màn hình chính của vServer sẽ thể hiện loại user mà bạn đang sử dụng để đăng nhập (Root user account hay IAM user account). Bạn có thể truy nhập vào tài nguyên đã được phân quyền theo Policy để sử dụng các chức năng của chúng.

**Step 7: Access vServer using IAM account (User account)**

The last step is to use  IAM User Account  to access vServer resources via vServer portal:

1. Access the link:  [https://dashboard.console.greennode.ai/](https://dashboard.console.greennode.ai/)
2. If you have not previously logged in with this browser, the main login page will appear. Select LOG IN WITH IAM USER ACCOUNT.
3. Enter the email  address of the Root user when registering for a GreenNode account.
4. Enter the username and password  of the IAM user account (User account) created on the viIAM system.
5. Select **LOG IN WITH IAM USER ACCOUNT**.\
   If you have previously logged in as an IAM user account in this browser, your browser may remember the account address IAM user account. If so, you should see the screen shown in step 3.\
   After successfully logging in with the IAM user account, the main screen of vServer will show the type of user you are using to log in (Root user account or IAM user account). You can access the resources that have been authorized according to the Policy to use their functions.

***

### **Step 8: Regularly review and check access rights** <a href="#identityandaccessmanagement-iam-forvserver-step8-regularlyreviewandcheckaccessrights" id="identityandaccessmanagement-iam-forvserver-step8-regularlyreviewandcheckaccessrights"></a>

* Conduct periodic checks on user access and permissions.
* Remove any unnecessary access privileges.
* Regularly review user accounts and access policies and change as necessary to ensure they match current requirements.

\
