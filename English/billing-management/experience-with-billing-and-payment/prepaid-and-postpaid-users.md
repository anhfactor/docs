# Prepaid & Postpaid Users

Use this document to better understand the types of resource usage for different types of users. At the GreenNode Service level, we support two main types of users:

* **Prepaid users:** Users who must pay for resource usage before they are allowed to use them. Payment for resource usage is based on the configuration and time they want to use (they need to determine the time to stop using resources).
* **Postpaid users:** Users who are allowed to use resources first and pay later, based on the actual resource usage cost. The amount to be paid will be determined at the end of each month until the user stops using the resource.

Let's take a look at some differences in concepts, rights, and functions between these two types of users for GreenNode services, such as:

* Process actions on resources: Create, Resize, Renew, Recover, Delete.
* Resource provisioning process.
* Resource management.
* Invoice management.
* Payment management.

## Process actions on resources

**Prepaid users**

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

**Postpaid users**

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Resource provisioning process

* **Prepaid users:**
  * After successful payment confirmation, the Product team will provide resources according to the configuration requested by the user.
  * During the resource provisioning process, if there is a process error, the system will refund the user's previously paid service fee. The refunded money will be converted into Credit and transferred to the GreenNode wallet.
* **Postpaid users:**
  * At the "Confirmation" step, the Product team will provide resources according to the user's requested configuration, and the system will record the start time of resource usage.

→ Note: Postpaid users do not need to complete the payment step when taking actions on resources.

## Resource management

Basically, the features that users can perform on resources are:

* **For prepaid users:**
  * Create new resources
  * Change configuration
  * Renew resources
  * Recover resources
  * Auto-renew resources
  * Delete resources
* **For postpaid users:**
  * Create new resources
  * Change configuration
  * Delete resources

For more details, see [Resource management](https://dashboard.console.greennode.ai/resource).

## Invoice management

* **Prepaid users**
  * At the successful payment step, after the resource is provisioned, the system generates an invoice for the resource, which is **marked as paid**.
* **Postpaid users**
  * Invoices are generated at the end of each month based on actual usage during that month, and are **marked as unpaid**.
  * Invoices are paid automatically from the Credit balance in your GreenNode wallet. You only need to top up Credit, and the system pays your unpaid invoices automatically every day.
  * Learn more in Buy Credits and Automatic invoice payment.

## Payment Management

* **Prepaid Users**
  * Payment history will appear immediately in the User Portal's [Payment history](https://dashboard.console.greennode.ai/payment-history) section after the user makes a resource payment.
* **Postpaid users**
  * A payment history entry is recorded each time the system automatically pays an invoice from your Credit balance, and appears in the User Portal under Payment history.

## How to switch from prepaid to postpaid and vice versa?

* When users register a new account at GreenNode, the system defaults to **prepaid users**.
* To **switch to postpaid**, users need to contact the Sales / Support team for assistance.
* If a postpaid user wants to **switch back to prepaid**, they also need to contact the Sales / Support team for assistance.
