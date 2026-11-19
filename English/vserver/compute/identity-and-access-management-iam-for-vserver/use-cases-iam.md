# Use Cases IAM

This article describes a simple business use case for IAM to help you understand how to implement the service to control user access to the GreenNode services you use. This example illustrates two ways that the company Example can apply IAM, including using GreenNode vServer.

***

## Initial Setup <a href="#cactruonghopsudungiam-thietlapbandau" id="cactruonghopsudungiam-thietlapbandau"></a>

Sasha Nguyen and Alex Thompson are the co-founders of Example Company. When founding the company, they understood the importance of a robust identity access management system to protect their resources. They decided to implement Identity Access Management (IAM) for their organization to ensure that only authorized individuals could access the company’s resources and services.

First, Sasha and Alex created a GreenNode account (Root user account). They used this account to access the IAM service. Their account was attached to the AdministratorAccess policy, meaning they had full control over all company resources and services with the Root user account.

As the company expanded, Sasha and Alex began hiring employees for various positions. Sasha took on the responsibility of overseeing company operations, while Alex managed the engineering teams. However, they couldn't grant Root user account access to these employees, as it would exceed the authority of each job position. Therefore, they needed to provide employees with User accounts derived from the Root user account on the IAM homepage with specific permissions to access and use the resources.

First, they identified the different roles within the company. For example, they had roles for developers, network administrators, database administrators, and support staff. Each role would have different access permissions to the company's resources and services. Sasha and Alex then created User accounts and user groups (Groups) corresponding to each role. These user groups would contain employees with similar access and roles, making it easier to manage access permissions for each group.

To manage access permissions, Sasha and Alex used IAM policies. They defined what each role and user group could and could not do. They assigned policies and roles to different groups to provide users with the correct level of access to GreenNode resources. They used GreenNode-managed policies for job functions in the IAM Management Console to create the following permission groups:

* _Administrator_
* _Billing_
* _Developers_
* _Network administrators_
* _Database administrators_
* _System administrators_
* _Support users_

They then assigned these policies to User accounts or Groups with the corresponding roles and provided usernames and passwords for the User accounts to employees to access and use the resources.

To guide the implementation of the IAM Identity Center, Sasha and Alex referred to the comprehensive "[Getting Started](./)" section in the GreenNode IAM User Guide. This step-by-step guide provided detailed instructions for initial configuration. Additionally, they consulted the "[Permission List for GreenNode Account Access](actions-resources-and-required-conditions-for-vserver-access-decentralization.md)" section of the user guide to better understand how to grant user access within the IAM Identity Center.

As the innovative company continued to grow, Sasha and Alex remained diligent in reviewing and updating access permissions for each employee. They regularly adjusted access permissions and levels to ensure that employees had the appropriate access privileges for their roles and responsibilities within the organization or revoked them as needed.

***

## IAM Use Case with vServer <a href="#cactruonghopsudungiam-truonghopsudungiamvoivserver" id="cactruonghopsudungiam-truonghopsudungiamvoivserver"></a>

A company like Example often uses IAM to interact with services such as GreenNode vServer. To understand this part of the use case, you need a basic understanding of GreenNode vServer. For more information on GreenNode vServer, see the [vServer User Guide](../getting-started/).

### vServer Permissions for User Groups <a href="#cactruonghopsudungiam-quyenvserverchonhomnguoidung" id="cactruonghopsudungiam-quyenvserverchonhomnguoidung"></a>

At Example, different user groups require different permissions:

<table data-header-hidden><thead><tr><th width="166"></th><th width="181"></th><th></th></tr></thead><tbody><tr><td><strong>Nhóm quyền</strong></td><td><strong>Phân quyền</strong></td><td><strong>Mô tả</strong></td></tr><tr><td><strong>System Administrator</strong></td><td>vServerFullAccess</td><td>This user group typically requires extensive permissions to manage all aspects of the resources. They may need permissions to create and manage resources, configure networks, set up security controls, and manage IAM policies and roles. Therefore, they need permissions to create and manage Images, Servers, VPCs, Volumes, Security Groups, etc. Alex attached the managed policy vServerFullAccess to the System Administrators user group to grant its members permission to perform all actions on vServer.</td></tr><tr><td><strong>Developer</strong></td><td>ListServer, GetServer, StartServer, StopServer, RebootServer</td><td>Since they only need to work with the Servers, Alex created and attached a policy to the Developers user group that allows developers to invoke the following permissions: ListServer, GetServer, StartServer, StopServer, RebootServer.</td></tr><tr><td><strong>Support</strong></td><td>vServerReadOnlyAccess</td><td>They should not be able to perform any vServer actions except listing the existing vServer resources. Therefore, Alex created and attached a policy to the Support user group that only allows them to invoke vServerReadOnlyAccess.</td></tr></tbody></table>

***

### **Assigning System Administrator Permissions to a User Group** <a href="#cactruonghopsudungiam-phanquyensystemadministratorchonhomnguoidung" id="cactruonghopsudungiam-phanquyensystemadministratorchonhomnguoidung"></a>

Taylor Smith was hired as a project manager, so he needs access to all company resources to manage access and deploy IT projects related to GreenNode infrastructure. Therefore, Alex granted Taylor a User account with vServerFullAccess permissions following these steps:

#### **Step 1: Create a User Account in the IAM System** <a href="#cactruonghopsudungiam-buoc1-taotaikhoannguoidung-useraccount-trenhethongiam" id="cactruonghopsudungiam-buoc1-taotaikhoannguoidung-useraccount-trenhethongiam"></a>

1. Alex created a GreenNode account on the homepage: [https://sso.vngcloud.vn/cas/login?service=https%3A%2F%2Fportal3.vngcloud.vn%2F](https://sso.vngcloud.vn/cas/login?service=https%3A%2F%2Fportal3.vngcloud.vn%2F) using the Root user account information: **Admin@vngcloud.vn**, password: **12345678@!**
2. Navigate to the IAM homepage:  [https://iam.console.greennode.ai/](https://iam.console.greennode.ai/)  using the Root user account to log in.
3. Open the User account tab.
4. Select "**Create a user account**."
5. In the **Account user name** field, Alex entered the **name** for the User account as **Sysad01**.
6. Enter the password for the User account in the **Account password** field.
7. Then click "**Create User Account**."

At this point, Alex created a separate User account for Taylor with the following information:

* User account: Username: **Sysad01** ; Password: **Asddehj**

**Step 2: Create a User Group**

After creating the User account, Alex proceeded to create a user group:

1. Open the Group tab at  [https://iam.console.greennode.ai/user-groups](https://iam.console.greennode.ai/user-groups).
2. Select "**Create a group**."
3. Alex entered the Group name as **SysAd** in the **Name** field and added a description in the **Description** field.
4. Proceed to the next step. In the **User** field, **Alex** selected the **Sysad01** User account to add to the **Group**.
5. Then click "**Create a Group**."

A Group named **SysAd** will be created, including the User account: **Sysad01.**

**Step 3: Assign Permissions to the User Group**&#x20;

Currently, IAM provides several default policies that help users quickly and efficiently set up access permissions. Therefore, for the SysAd user group, Alex added the **vServerFullAccess** policy following these steps:

1. Open the Policy tab at [IAM Policies](https://iam.console.greennode.ai/policies).
2. Click to view the details of the **vServerFullAccess** policy on the list page.
3. Then, in the **Policy usage** menu, click **Attach**.
4. In the **Group tab**, **Alex** selected the **SysAd** group and clicked **Add**.

After completing these steps, the SysAd group will include the User account Sysad01 with the vServerFullAccess policy.

**Step 4: Access Resources Using the IAM Account (User account)** After creating the User account: Sysad01, Alex granted this account to Taylor, who then used it to access the company's resources:

1. Access the vServer dashboard at: [GreenNode vServer](https://hcm-3.console.greennode.ai/vserver/).
2. On the **login** screen, select "**SIGNIN WITH IAM USER ACCOUNT.**"
3. Enter the **Root email information: Admin@vngcloud.vn, User name: Sysad01, Password: Asddehj**.
4. The screen will navigate to the vServer management page, where you can interact with the resources granted in the Policy assigned to the User account.

***

### Assigning Developer Permissions to a User Group

Johnson Miles and Scott Enzi joined the company as Developers, so they need permissions to work with Servers, such as viewing the list, starting, or stopping Servers. However, they cannot create or change Server configurations and view billing information. Therefore, Alex granted them User accounts in the Devs user group with the Developer policy. Johnson and Scott can then use the User account username and password to access and use the granted resources:

**Step 1: Create a User Account in the IAM System**

1. Access the IAM homepage at: [IAM Console](https://iam.console.greennode.ai/).
2. Open the User account tab.
3. Select "Create a user account."
4. In the Account user name field, Alex entered the name for the User account as Dev01.
5. Enter the password for the User account in the Account password field.
6. Then click "Create User Account."

At this point, Alex created two separate User accounts for Johnson Miles and Scott Enzi with the following information:

* **User account 1:** Username: **Dev01** ; Password: **Asddehj1**
* **User account 2:** Username: **Dev02** ; Password: **Aseeeghe2**

**Step 2: Create a User Group**

After creating the User accounts, Alex proceeded to create a user **group:**

1. Open the Group tab at [IAM User Groups](https://iam.console.greennode.ai/user-groups).
2. Select "**Create a group**."
3. Alex entered the Group name as **DevGroup** in the **Name** field and added a description in the **Description** field.
4. Proceed to the next step. In the **User** field, **Alex** selected the **Dev01** and **Dev02** User accounts to add to the **Group**.
5. Then click "**Create a Group**."

A Group named **DevGroup** will be created, including the two User accounts: **Dev01** and **Dev02**.

**Step 3: Assign Permissions to the User Group**&#x20;

After creating the Group, Alex needed to create a policy to assign to the Group:

1. Open the Policy tab at [IAM Policies](https://iam.console.greennode.ai/policies).
2. Create a new policy by clicking "**Create a Policy.**"
3. In the Information screen, in the **Name** field, Alex entered the name of the Policy as **Developers**.
4. Proceed to the **Permissions** step. Alex selected **Product: vServer**.
5. In the **Action** field, Alex selected the permissions: **ListServer, GetServer, StartServer, StopServer, RebootServer.**
6. Currently, Alex grants the Developer group permissions to all Servers, so he selected **All Resources** in the **Resource** field.
7. Then click "**Create Policy**" to create the new policy.
8. After that, on the Policy list page, select the newly created Developers policy.
9. On the Policy detail page, select the **Policy usage tab** and click **Attach**.
10. In the **Group** tab, **Alex** selected the **DevGroup** and clicked **Add**.

After completing these steps, the **SysAd** group will include the two User accounts **Dev01** and **Dev02** with the **Developers** policy.

#### **Bước 4: Truy cập vào tài nguyên sử dụng IAM account (User account)** <a href="#cactruonghopsudungiam-buoc4-truycapvaotainguyensudungiamaccount-useraccount-.1" id="cactruonghopsudungiam-buoc4-truycapvaotainguyensudungiamaccount-useraccount-.1"></a>

Sau khi tạo 2 User account: Dev01, Dev02, Alex đã cấp quyền sử dụng account này cho Johnson và Scott, họ  đã sử dụng để truy cập vào tài nguyên của Công ty và sử dụng chúng:

1. Truy cập vào bảng điều khiển vServer tại: [**https://hcm-3.console.greennode.ai/vserver/**](https://hcm-3.console.greennode.ai/vserver/)
2. Tại màn hình **Đăng nhập:** chọn **SIGNIN WITH IAM USER ACCOUNT**
3. Nhập thông tin **Root email: Admin@vngcloud.vn,** Username: **Dev01 ;** Pasword: **Asddehj1 /** Username: **Dev02 ;** Pasword: **Aseeeghe2**
4. Màn hình sẽ điều hướng sang trang quản lý vServer, tại đây có thể thao tác vào các tài nguyên được cấp quyền trong Policy đã gán với User account.

**Step 4: Access Resources Using the IAM Account (User account)**&#x20;

After creating the two User accounts: Dev01 and Dev02, Alex granted these accounts to Johnson and Scott, who then used them to access the company's resources:

1. Access the vServer dashboard at: [GreenNode vServer](https://hcm-3.console.greennode.ai/vserver/).
2. On the **login** screen, select "**SIGNIN WITH IAM USER ACCOUNT**."
3. Enter the **Root email** information: **Admin@vngcloud.vn**, Username: **Dev01** ; Password: **Asddehj1** / Username: **Dev02** ; Password: **Aseeeghe2**.
4. The screen will navigate to the vServer management page, where you can interact with the resources granted in the Policy assigned to the User account.

***

### Assigning Support Permissions to a User Group

**Step 1: Create a User Account in the IAM System**

1. Access the IAM homepage at: [IAM Console](https://iam.console.greennode.ai/).
2. Open the User account tab.
3. Select "**Create a user account**."
4. In the **Account user name** field, Alex entered the **name** for the User account as **Supo01**.
5. Enter the password for the User account in the **Account password** field.
6. Then click "**Create User Account**."

At this point, **Alex** created a separate User account for **Taylor** with the following information:

* **User account**: Username: **Supo01** ; Password: **Asddehj3**

**Step 2: Create a User Group**

After creating the User account, Alex proceeded to create a user **group**:

1. Open the Group tab at [IAM User Groups](https://iam.console.greennode.ai/user-groups).
2. Select "**Create a group**."
3. Alex entered the Group name as **SupportGroup** in the **Name** field and added a description in the **Description** field.
4. Proceed to the next step. In the **User** field, **Alex** selected the **Supo01** User account to add to the **Group**.
5. Then click "**Create a Group**."

A Group named **SupportGroup** will be created, including the User account: **Supo01**.

**Step 3: Assign Permissions to the User Group** Currently, IAM provides several default policies that help users quickly and efficiently set up access permissions. Therefore, for the SupportGroup user group, Alex added the **vServerReadOnlyAccess** policy following these steps:

1. Open the Policy tab at [IAM Policies](https://iam.console.greennode.ai/policies).
2. Click to view the details of the **vServerReadOnlyAccess** policy on the list page.
3. Then, in the **Policy usage** menu, click **Attac**h.
4. In the Group **tab**, **Alex** selected the **SupportGroup** and clicked **Add.**

After completing these steps, the SupportGroup will include the User account Supo01 with the vServerReadOnlyAccess policy.

**Step 4: Access Resources Using the IAM Account (User account)** After creating the User account: Supo01, Alex granted this account to Taylor, who then used it to access the company's resources:

1. Access the vServer dashboard at: [GreenNode vServer](https://hcm-3.console.greennode.ai/vserver/).
2. On the **login** screen, select "**SIGNIN WITH IAM USER ACCOUNT**."
3. Enter the **Root email information: Admin@vngcloud.vn, User name: Supo01, Password: Asddehj3.**

The screen will navigate to the vServer management page, where you can interact with the resources granted in the Policy assigned to the User account.\
