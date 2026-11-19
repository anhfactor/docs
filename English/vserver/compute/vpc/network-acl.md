# Network ACL

### **Overview** <a href="#networkacl-overview" id="networkacl-overview"></a>

Network ACL is a feature that helps you control network traffic in and out of subnets in your VPC. Simplify, Network ACL is the security layer of a subnet. It is associated to the subnet, and all traffic entering or leaving the subnet must be approved by the **Network ACL**. Specifically:

* When traffic travels from the internet to a **vServer instance**, it must first pass through the **Network ACL** before reaching the **Security Group**.
* When traffic travels from a **vServer instance**, it must first pass through the **Security Group** before reaching the **Network ACL**.

***

### **Basic knowledge about Network ACL:** <a href="#networkacl-basicknowledgeaboutnetworkacl" id="networkacl-basicknowledgeaboutnetworkacl"></a>

* Each VPC will not have any Network ACLs default after being created.
* You can create a new Network ACL and associate it to one or more subnets in your VPC. We provide you with available inbound rules, you can add the desired rules according to the instructions below.
* A Network ACL can be associated to multiple subnets, but a subnet can only be associated to one Network ACL at a time.
* A Network ACL has rules to allow and deny traffic. Each rule is marked with a unique priority.
* When deciding to allow or deny traffic, we will evaluate the rules in order, starting with the rule with the lowest number.
* Network ACL rules only apply when traffic enters or leaves a subnet, not to traffic within a subnet or NAT traffic from Floating IP.
* There is a limit on the number of Network ACLs per VPC and the number of rules per Network ACL.

***

### **Differences between Security Group and Network ACL** <a href="#networkacl-differencesbetweensecuritygroupandnetworkacl" id="networkacl-differencesbetweensecuritygroupandnetworkacl"></a>

Please refer to the table below to distinguish between Security Group and Network ACL

| **Feature**            | **Security Group**                                                                                                                                                                                                                                                   | **Network ACL**                                                                                                                                                                                                                                                                  |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Level of operation** | Instance level                                                                                                                                                                                                                                                       | Subnet level                                                                                                                                                                                                                                                                     |
| **Applies to**         | Only applies to instances associated to that security group.                                                                                                                                                                                                         | Applies to all instances deployed in the subnet associated to that Network ACL.                                                                                                                                                                                                  |
| **Rules**              | Only supports allow rules for traffic from **public**.                                                                                                                                                                                                               | Supports both allow and deny rules for traffic in **internal**.                                                                                                                                                                                                                  |
| **Rule evaluation**    | Evaluates all rules before deciding to allow traffic                                                                                                                                                                                                                 | Evaluates in order, starting from the rule with the lowest number                                                                                                                                                                                                                |
| **State**              | <p><strong>Stateful</strong>: </p><ul><li>If specific <strong>traffic</strong> is allowed to the instance in the <strong>inbound rule</strong>, then the <strong>outbound rule</strong> will automatically allow traffic to leave the instance, and versa.</li></ul> | <p><strong>Stateless</strong>: </p><ul><li>If specific <strong>traffic</strong> is allowed to the subnet in the <strong>inbound rule</strong>, then the <strong>outbound rule</strong> will not automatically allow traffic to leave the subnet, and versa.</li></ul><p><br></p> |

***

### **Components of a Network ACL rule:** <a href="#networkacl-componentsofanetworkaclrule" id="networkacl-componentsofanetworkaclrule"></a>

A Network ACL consists of the following basic components:

* Network ACL name: The name of the Network ACL.
* VPC: The VPC that the Network ACL is associated to.
* Inbound rules/Outbound rules:
  * Priority: The weight of the rule. Rules are evaluated based on this weight, starting with the rule with the lowest number.
  * Protocol: The access protocol. For example, TCP, UDP, ICMP, etc.
  * Port range: The port number or range of ports to start and end.
  * Source: The desired IP or IP range/CIDR to allow/deny access in Inbound rules.
  * Destination: The desired IP or IP range/CIDR to allow/deny access in Outbound rules.
  * Allow/Deny: Allow or deny the specified traffic.
* Subnet: The subnet that the Network ACL is associated to.

Each Network ACL has 2 default inbound rules (1 allow rule and 1 deny rule) and 2 default outbound rules (1 allow rule and 1 deny rule). **You cannot modify or delete these default deny rules.**

* **Inbound rules:**

<table><thead><tr><th width="123">Priority</th><th>Type</th><th width="98">Protocol</th><th width="102">Port range</th><th width="122">Source</th><th width="80">Allow/ Deny</th><th>Ghi chú</th></tr></thead><tbody><tr><td>0</td><td>Inbound</td><td>ANY</td><td>0-65535</td><td>0.0.0.0/0</td><td>Allow</td><td>Can Delete/Edit Inbound rules.</td></tr><tr><td>2000</td><td>Inbound</td><td>ANY</td><td>0-65535</td><td>0.0.0.0/0</td><td>Deny</td><td>Cannot Delete/Edit Inbound rules.</td></tr></tbody></table>

* **Outbound rules:**

| Priority | Type     | Protocol | Port range | Destination | Allow/ Deny | Ghi chú                            |
| -------- | -------- | -------- | ---------- | ----------- | ----------- | ---------------------------------- |
| 0        | Outbound | ANY      | 0-65535    | 0.0.0.0/0   | Allow       | Can Delete/Edit Outbound rules.    |
| 2000     | Outbound | ANY      | 0-65535    | 0.0.0.0/0   | Deny        | Cannot Delete/Edit Outbound rules. |

***

### **Working with Network ACLs** <a href="#networkacl-workingwithnetworkacls" id="networkacl-workingwithnetworkacls"></a>

#### Creating a Network ACL <a href="#networkacl-creatinganetworkacl" id="networkacl-creatinganetworkacl"></a>

You can create a custom Network ACL for your VPC. By default, the Network ACL you create will deny all inbound and outbound traffic until you add rules, and it is not associated with any subnets until you explicitly associate it with a subnet.

To create a Network ACL, follow these steps:

1. Access the vServer service home page at the following link: [https://hcm-3.console.greennode.ai/vserver/](https://hcm-3.console.greennode.ai/vserver/)
2. In the left-hand menu, select **Network**, then select **Network ACLs**.
3. Select **Create Network ACL**.
4. Enter a **Name** and select **1 active VPC** where you want to create the Network ACL. Note: The Network ACL name only allows letters (a-z, A-Z, 0-9, '\_', '-') and the length of your input data must be between 5 and 50.
5. Select **Create**.

Your Network ACL is now created with the default Inbound rule and Outbound rule described in the table above. Continue using the instructions below to edit the Inbound rule, Outbound rule, and associate the Subnet with the newly created Network ACL.

***

#### Editing the Inbound Rules List

To edit the Inbound rule list (rules that allow traffic to enter), follow these steps:

1. Access the vServer service home page at the following link: [https://hcm-3.console.greennode.ai/vserver/](https://hcm-3.console.greennode.ai/vserver/)
2. In the left-hand menu, select **Network**, then select **Network ACLs**.
3. In the list of created Network ACLs, select a **Network ACL**.
4. In the **Inbound rules** section, select **Edit Inbound rules**.
5. Select **Add rule** if you want to create a new rule, or select the icon <img src="https://docs.vngcloud.vn/download/thumbnails/71729277/image2024-2-24_17-45-8.png?version=1&#x26;modificationDate=1708921940000&#x26;api=v2" alt="" data-size="line">if you want to **delete** the newly created rule.
6. Edit **Priority:** enter the weight (priority) for the rule. The rule weight must not be the same as a number already in the Network ACL. We process rules by weight, starting from the lowest to the highest, regardless of Allow or Deny. The maximum weight you can set is **32766**.
7. Edit **Protocol:** add the access protocol you want to allow/deny to enter the Subnet. We are providing you with 1 of 4 options: ANY, TCP, UDP, ICMP.
8. Edit **Port range:** the port number or range of ports to start and end.
9. Edit **Source:** the desired IP or IP range/CIDR to allow/deny access according to Inbound rules.
10. Edit **Allow/Deny:** allow or deny the specified traffic.
11. If you want to add more Inbound rules, continue to select **Add rule** and repeat steps 6, 7, 8, 9, and 10.
12. If you want to delete multiple Inbound rules, continue to select the icon  <img src="https://docs.vngcloud.vn/download/thumbnails/71729277/image2024-2-24_17-45-8.png?version=1&#x26;modificationDate=1708921940000&#x26;api=v2" alt="" data-size="line"> at the rules you want to delete. <mark style="color:red;">**Note: You cannot edit or delete the default Inbound rules deny created by us.**</mark>
13. Select **Save** to save the entered/selected edits or select **Cancel** to cancel the edit changes.

***

#### Editing the Outbound Rules List

To edit the Outbound rule list (rules that allow traffic to exit), follow these steps:

1. Access the vServer service home page at the following link: [https://hcm-3.console.greennode.ai/vserver/](https://hcm-3.console.greennode.ai/vserver/)
2. In the left-hand menu, select **Network**, then select **Network ACLs**.
3. In the list of created Network ACLs, select a **Network ACL**.
4. In the **Outbound rules** section, select **Edit Outbound rules**.
5. Select **Add rule** if you want to create a new rule, or select the icon<img src="https://docs.vngcloud.vn/download/thumbnails/71729277/image2024-2-24_17-45-8.png?version=1&#x26;modificationDate=1708921940000&#x26;api=v2" alt="" data-size="line"> if you want to delete the newly created rule.
6. Edit **Priority:** enter the weight (priority) for the rule. The rule weight must not be the same as a number already in the Network ACL. We process rules by weight, starting from the lowest to the highest, regardless of Allow or Deny. The maximum weight you can set is **32766**.
7. Edit **Protocol:** add the access protocol you want to allow/deny to exit the Subnet. We are providing you with 1 of 4 options: ANY, TCP, UDP, ICMP.
8. Edit **Port range:** the port number or range of ports to start and end.
9. Edit **Destination:** the desired IP or IP range/CIDR to allow/deny access according to Outbound rules.
10. Edit **Allow/Deny:** allow or deny the specified traffic.
11. If you want to add more Outbound rules, continue to select **Add rule** and repeat steps 6, 7, 8, 9, and 10.
12. If you want to delete multiple Outbound rules, continue to select the icon <img src="https://docs.vngcloud.vn/download/thumbnails/71729277/image2024-2-24_17-45-8.png?version=1&#x26;modificationDate=1708921940000&#x26;api=v2" alt="" data-size="line">at the rules you want to delete. <mark style="color:red;">**Note: You cannot edit or delete the default Outbound rules deny created by us.**</mark>
13. Select **Save** to save the entered/selected edits or select **Cancel** to cancel the edit changes.

***

#### Associating/Disassociating a Subnet with a Network ACL

To apply the rules of a Network ACL to a specific subnet, you need to associate that subnet with the Network ACL. You can associate a Network ACL with multiple subnets, but a subnet can only be associated with one Network ACL at a time.

To associate a subnet with a Network ACL, follow these steps:

1. Access the vServer service home page at the following link: [https://hcm-3.console.greennode.ai/vserver/](https://hcm-3.console.greennode.ai/vserver/)
2. In the left-hand menu, select **Network**, then select **Network ACLs**.
3. In the list of created Network ACLs, select a **Network ACL**.
4. In the **Subnet association** section, select **Edit Subnet Association**.
5. In the Edit Subnet Association screen, you can associate/disassociate a Subnet with a Network ACL by:
   1. In the **Available Subnets** section, you can select one or more **Subnets** to associate using the icon  <img src="https://docs.vngcloud.vn/download/thumbnails/71729277/image2024-2-24_18-9-10.png?version=1&#x26;modificationDate=1708921940000&#x26;api=v2" alt="" data-size="line">.
   2. In the **Associated Subnets** section, you can disassociate a **Subnet** from the **Network ACL** by selecting the Subnet you want to disassociate.
6. Select **Save** to save the entered/selected edits or select **Cancel** to cancel the edit changes.

{% hint style="info" %}
**Notes:**

* When you associate a subnet with a new Network ACL, the Inbound rules and Outbound rules of the new Network ACL will start to apply to traffic to and from that subnet.
* You can associate a subnet with a different Network ACL at any time. At this time, we will disconnect the old association and perform the new association according to your edit, ensuring that at any time a subnet can only be attached to one Network ACL. Changing the subnet association can affect the traffic to and from that subnet.
{% endhint %}

***

#### **Delete a Network ACL** <a href="#networkacl-deleteanetworkacl" id="networkacl-deleteanetworkacl"></a>

You can only delete a Network ACL if it is not associated with any subnets. If the Network ACL you want to delete is still associated with subnets, follow the instructions above to **Disassociate Subnets from a Network ACL** before deleting the Network ACL.

**To delete a Network ACL, follow these steps:**

1. Access the vServer service home page at the following link: [https://hcm-3.console.greennode.ai/vserver/](https://hcm-3.console.greennode.ai/vserver/)
2. In the left-hand menu, select **Network**, then select **Network ACLs**.
3. At the Network ACL you want to delete, select the icon <img src="https://docs.vngcloud.vn/download/thumbnails/71729277/image2024-2-24_18-17-12.png?version=1&#x26;modificationDate=1708921940000&#x26;api=v2" alt="" data-size="line">.
4. In the delete confirmation screen, select **Delete** if you are sure you want to delete this Network ACL, or **Cancel** if you want to cancel the deletion.

<br>
