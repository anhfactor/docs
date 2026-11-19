# Resource POC

The POC resource is created to support users to experience the services at GreenNode in the best way possible.

**Conditions for using POC resources:**

* Target: Target: Prepaid users who are granted POC wallets.
* Source of money: POC wallets.
* Resources: Resources: All resources eligible for POC.
* Usage time: Depends on the time limit of the granted POC wallet.

## Initializing POC resources

* Step 1: Configure resources
  * 1.1 Access the vServer, vStorage, vMonitor product page.
  * 1.2 Select the resources and configuration to use on the product page.
  * 1.3 Click to use POC resources.
  * 1.4 Confirm the use of resources to proceed to payment: At this point, the system will redirect users to the resource payment page.
* Step 2: Pay for resources using the POC wallet
* Step 3: System Implementation
  * Provide resources.
  * Email notification of newly created resource information.

**Some notes when initializing POC resources**

* The default usage time of POC resources is the same as the end time of the POC wallet.
* POC wallets can only be used to pay for POC resources.
* For POC resources, the system will not generate corresponding resource invoices.
* The pricing method for using POC resources is similar to regular resources. See details here

## Changing the configuration of POC resources

The pricing process and methods are similar to when changing configurations when using regular resources. See details here.

## Renewing POC resources

In case the usage time of the user's POC wallet is extended after POC resources have been initialized, the user can proceed to extend the corresponding POC resources with the new end time of the wallet. The pricing process and methods are similar to when extending regular resources. See details here.

## Stopping POC for POC resources

Users can stop POC for a POC resource at any time while the POC wallet is valid. **Stopping POC means converting the resource from POC to a paid service**: the resource keeps its configuration and continues to be used as a regular resource.

When the user stops POC, the system will:

* Refund the remaining POC resource usage fee (if any) to the POC wallet.
* Redirect the user to the payment page. The user must pay the usage fee through payment methods other than the POC wallet, such as GreenNode Credit or a payment gateway.

After payment succeeds, the resource is treated as a regular resource.

## POC wallet expiration

When the POC wallet expires, the system will:

* End POC for all POC resources currently in use. Resources are **not** automatically converted to a paid service:
  * For resources that use **Credit hold**, the system stops the service and deletes the POC resource immediately. If you want to keep using the resource, stop POC yourself (convert it to a paid service) before the POC wallet expires. See the list of services that use Credit hold.
  * For resources paid in advance from the POC wallet, the resource is suspended for 7 days before being permanently deleted. During this time, you can renew the resource if you want to keep using it.
* Disable the POC wallet: users cannot use resources in the POC form until the POC wallet is enabled again.
