# Create resource

Use this document as a guide to initialize resources. The document will describe in detail the processing steps related to resource management during initialization. Other steps will be simplified and only referred to as part of the process.

Resource initialization feature applies to:

* Target user: Prepaid and postpaid users
* Source of money: GreenNode wallet or other sources (performed through payment gateway).
* Resources: All resources belonging to GreenNode products.

## Prepaid user initializes resources

### Resource initialization process

* Step 1: Configure resources
  * 1.1 Access the vServer, vStorage, vMonitor product page.
  * 1.2 Select the resources and configurations to use on the product page.
  * 1.3 Confirm the use of resources to proceed to payment: At this point, the system will redirect the user to the resource payment page.
* Step 2: Pay for resources.
* Step 3: Check resource and payment information
  * 3.1 Check resource information on the product page.
  * 3.2 Check [payment](https://dashboard.console.greennode.ai/payment-history) information at User Portal.
* Step 4: System Implementation
  * Generate the corresponding invoice: see [Invoice management](https://dashboard.console.greennode.ai/billing-report) for how the amount and invoice information are calculated.

### Resource pricing guide

The price displayed at the resource payment step is also the price displayed on the corresponding invoice for that resource.

Below is a guide to calculate the price when initializing a Server, users can apply the formula to calculate similarly for other resources in the GreenNode Service system.

_An example formula for calculating the invoice value when initializing a Server includes information:_

| Server configuration (1)         | Unit price (incl. VAT) (2) | Usage period (3) | Coupon value (4) | Amount = (2) × (3) |
| -------------------------------- | -------------------------- | ---------------- | ---------------- | ------------------ |
| Image (dev.v1.small1x1)          | 90,000 VND / 30 days       | 60 days          | 20,000 VND       | 180,000            |
| Root disk (Size 20GB, IOPS 3000) | 35,000 VND / 30 days       | 60 days          |                  | 70,000             |

**Amount to pay** = Total amount − Coupon value = 180,000 + 70,000 − 20,000 = **230,000 VND**

## Postpaid user initializes resources

### Resource initialization process

* Step 1: Configure resources on the product page
  * 1.1 Access the vServer, vStorage, vMonitor product page
  * 1.2 Select the resources and configuration to be used on the product page
  * 1.3 Confirm the use of resources.
  * 1.4 Check resource information.
* Step 2: The system sends confirmation to the user
  * Records the start time of resource usage, used to calculate the usage cost at the end of the month.
