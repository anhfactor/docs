# Delete resource

Use this document as a guide for deleting resources. The document will describe in detail the steps related to resource management and the costs incurred when deleting resources. Other steps will be streamlined and only mentioned as part of the process.

**The feature of deleting resources applies to**

* Target: Prepaid and postpaid users.
* Money source: GreenNode Wallet (in case of refund).
* Resources: All resources belonging to GreenNode products.

## Prepaid user deletes resources

**Resource deletion process**

* Step 1: Select the resource to delete
  * 1.1 Access the vServer, vStorage, vMonitor product page.
  * 1.2 Select the resource to be deleted on the product page.
  * 1.3 Confirm the resource deletion.
* Step 2: The system performs resource deletion.
  * The selected resource is permanently deleted and cannot be restored.
  * Refund unused resource costs for applicable resources.
* Step 3: Check information
  * Check the refund information in the user portal, on the [Credit history](https://dashboard.console.greennode.ai/credit-history).

**Guide to calculating the refunded resource price**

Below is a guide to calculating the refunded price when deleting a Server resource, users can apply the formula to calculate similarly for other resources in the GreenNode Service system.

Example: a Server resource is created on 06-03-2023 with an end date of 06-05-2023, and is deleted on 16-04-2023. For simplicity, the example assumes 30 days per month.

| Action     | Configuration | Action date | Unit price at creation (VND / 30 days) | Days remaining until end date | Unused resource value (VND) | Refunded amount (VND) |
| ---------- | ------------- | ----------- | -------------------------------------- | ----------------------------- | --------------------------- | --------------------- |
| **Create** | s-general-1x1 | 06-03-2023  | 181,000                                | 60                            |                             |                       |
| **Delete** | s-general-1x1 | 16-04-2023  | 181,000                                | 20                            | 181,000 / 30 × 20 = 120,667 | 120,667               |

From the example above, the user is refunded 120,667 VND to their Credit wallet for deleting the Server resource on 16-04-2023.

From the example above, the user will be refunded 122,667 VND to their Credit wallet for deleting the Server resource at the time of 16-04-2023.

(\*) Note:

* The unused resource value is calculated to the minute.
* Some services may not be eligible for refunds, depending on the terms of use of each product (vServer, vStorage, vMonitor).

## Deleting resources for postpaid users

Resource deletion process

* Step 1: Select the resource to be deleted
  * 1.1 Access the vServer, vStorage, and vMonitor product pages.
  * 1.2 Select the resource to be deleted on the product page.
  * 1.3 Confirm the deletion of the resource.
* Step 2: The system performs resource deletion
  * The selected resource is permanently deleted and cannot be restored.
  * Record the time when the user stopped using the resource for billing purposes at the end of each month.
