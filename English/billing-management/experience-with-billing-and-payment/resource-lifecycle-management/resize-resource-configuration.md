# Resize resource configuration

Use this document as a guide to modify resource configurations. The document will describe in detail the processing steps related to resource management and the cost changes when changing configurations. Other steps will be simplified and mentioned as part of the process.

The resource configuration change feature applies to:

* Target user: Prepaid and postpaid users.
* Source of money: GreenNode Wallet or other sources (performed through payment gateway)
* Resources: All resources of GreenNode products that allow configuration changes

## Prepaid users change resource configuration

### Process of changing resource configuration

* Step 1: Select new resources and configurations.
  * 1.1 Access the vServer, vStorage, vMonitor product page.
  * 1.2 Select the resources and configurations you want to use on the product page.
  * 1.3 Confirm the configuration change to proceed to the payment step: At this point, the system will redirect the user to the resource payment page.
* Step 2: Pay for resources
  * See the detailed instructions in Payment.
* Step 3: Check resource and payment information
  * 3.1 Check resource information on the product page.
  * 3.2 Check payment information and invoices at User Portal: [https://dashboard.console.greennode.ai/](https://dashboard.console.greennode.ai/).
* Step 4: System Implementation
  * Invoice generated according to the new configuration.

### Instructions on how to calculate resource prices when changing configurations

The displayed price at the payment step when changing vServer resource configurations (similarly applied to other resources) is calculated as follows:

The price displayed at the payment step when changing a vServer resource configuration (similarly applied to other resources) is calculated as in the example below. The resource was created on 06-03-2023 and expires on 06-06-2023. For simplicity, the example assumes 30 days per month.

| Action         | Configuration                 | Action date | Days remaining (1) | Old configuration unit price (VND / 30 days) (2) | New configuration unit price (VND / 30 days) (3) | Unused value of old configuration (VND) (4) = (2) / 30 × (1) | Value of new configuration (VND) (5) = (3) / 30 × (1) | Amount to pay (VND) (6) = (5) − (4) |
| -------------- | ----------------------------- | ----------- | ------------------ | ------------------------------------------------ | ------------------------------------------------ | ------------------------------------------------------------ | ----------------------------------------------------- | ----------------------------------- |
| **Create**     | s-general-1x1                 | 06-03-2023  | 90                 |                                                  | 181,000                                          |                                                              | 181,000 / 30 × 90 = 543,000                           | 543,000                             |
| **1st change** | s-general-1x1 → s-general-2x4 | 16-04-2023  | 50                 | 181,000                                          | 520,000                                          | 181,000 / 30 × 50 = 301,667                                  | 520,000 / 30 × 50 = 866,667                           | 565,000                             |
| **2nd change** | s-general-2x4 → s-general-1x1 | 16-05-2023  | 20                 | 520,000                                          | 181,000                                          | 520,000 / 30 × 20 = 346,667                                  | 181,000 / 30 × 20 = 120,667                           | −226,000                            |

→ **1st change, upgrading from s-general-1x1 to s-general-2x4:** the user pays an additional 565,000 VND.

→ **2nd change, downgrading from s-general-2x4 to s-general-1x1:** the user is refunded 226,000 VND to their Credit wallet.

Note:

* The unused resource value is calculated to the minute.
* Some services may not be eligible for refunds, depending on the terms of use of each product (vServer, vStorage, vMonitor).

## Postpaid users change resource configuration

* Step 1: Configure resources on the product page
  * 1.1 Access the vServer, vStorage, vMonitor product page.
  * 1.2 Select the resource and configuration to use on the product page.
  * 1.3 Confirm the configuration change.
  * 1.4 Check resource information
* Step 2: The system sends confirmation to the user
  * Records the start time of using the new configuration.
