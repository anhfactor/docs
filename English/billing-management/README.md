# Billing & Payment

**Billing & Payment** lets you pay, receive invoices and track costs for every GreenNode service, such as vServer, vStorage, vMonitor and vCDN, in one place, without reconciling each product separately.

***

## How Billing & Payment works

Whenever you create, resize, renew or delete a resource on a product page, Billing & Payment records the action, processes the payment and issues an invoice for that exact resource. Invoices, payment history and Credit balance changes from every product are collected in **vConsole** at [dashboard.console.greennode.ai](https://dashboard.console.greennode.ai/).

For prepaid users, creating a resource takes 3 steps:

1. **Configure the resource**: choose the resource and its configuration on the product page, then confirm to go to the payment page.
2. **Pay**: choose the quantity and usage period, enter a coupon if you have one, then pay with your Credit balance, **Top up & Pay** or a linked account.
3. **Check the result**: the resource appears on the product page, and the invoice and payment history appear in vConsole.

***

## Prepaid and postpaid users

Every GreenNode account is one of two user types. The user type decides when you pay, when invoices are issued and which actions you can take on a resource.

| Criteria              | Prepaid                                                                                    | Postpaid                                                               |
| --------------------- | ------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------- |
| When you pay          | Before use, based on the configuration and usage period you choose                         | After use, based on actual usage cost, closed at the end of each month |
| Resource provisioning | After payment succeeds. If provisioning fails, the money is refunded to your Credit wallet | As soon as you confirm, with no payment step                           |
| Invoice               | Issued once the resource is provisioned, already marked as paid                            | Issued at the end of each month, marked as unpaid                      |
| How invoices are paid | Not needed, the invoice is already paid when issued                                        | Automatic invoice payment                                              |
| Actions on resources  | Create, resize, renew, auto-renew, recover, delete                                         | Create, resize, delete                                                 |

{% hint style="info" %}
New accounts are prepaid by default. To switch to postpaid, or from postpaid back to prepaid, contact Sales / Support.
{% endhint %}

***

## Key features

### Payment

Billing & Payment supports several payment methods: online payment, payment of POC resources, Credit hold and automatic invoice payment. You can pay for several resources at once. In that case, the payment history records one combined amount, while each resource gets its own invoice.

### Invoice management

Every action on a resource, such as create, resize or renew, issues an invoice for that exact resource, so you can reconcile costs down to each resource.

### Resource lifecycle management

The system tracks each resource's status from creation to deletion and emails you before a prepaid resource expires. If the product supports auto-renewal and you have turned it on for the resource, the system renews it for you so your usage is not interrupted. A prepaid resource that expires without being renewed is suspended and then permanently deleted.

### Tracking costs in vConsole

| Page                                                                                                                    | Use it to                                                                    |
| ----------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| [Billing History](vconsole-management-channel-for-billing-and-resources/getting-started/billing-history.md)             | View invoices and their payment status across all products                   |
| [Payment History](vconsole-management-channel-for-billing-and-resources/getting-started/payment-history.md)             | View the amount, method and date of each payment                             |
| [Credit History](vconsole-management-channel-for-billing-and-resources/getting-started/credit-history.md)               | View changes to your Credit wallet balance: top-ups, payments, refunds       |
| [Usage Report](vconsole-management-channel-for-billing-and-resources/getting-started/usage-report.md)                   | View usage time and configuration changes of each resource, with costs       |
| [Cost Explorer](vconsole-management-channel-for-billing-and-resources/getting-started/cost-explorer.md)                 | Analyze and forecast costs by product, resource type and individual resource |
| [Notification Settings](vconsole-management-channel-for-billing-and-resources/getting-started/notification-settings.md) | Receive emails about invoices, system maintenance and service alerts         |

***

## Getting started with Billing & Payment

| I want to...                                           | Go to                                                                                                                                          |
| ------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| Top up Credit to my wallet                             | [Buy Credits](vconsole-management-channel-for-billing-and-resources/getting-started/other-features/buy-credits.md)                             |
| Understand the difference between prepaid and postpaid | [Prepaid & Postpaid Users](experience-with-billing-and-payment/prepaid-and-postpaid-users.md)                                                  |
| Use a coupon when paying                               | [Apply coupon at payment step](experience-with-billing-and-payment/payment/apply-coupon-at-payment-step.md)                                    |
| Pay postpaid invoices                                  | [Automatic invoice payment](experience-with-billing-and-payment/payment/automatic-invoice-payment.md)                                          |
| Renew a resource                                       | [Renew resource](experience-with-billing-and-payment/resource-lifecycle-management/renew-resource.md)                                          |
| Recover an expired resource                            | [Recover resource](experience-with-billing-and-payment/resource-lifecycle-management/recover-resource.md)                                      |
| Grant other members access to vConsole                 | [Access Management via IAM](vconsole-management-channel-for-billing-and-resources/getting-started/other-features/access-management-via-iam.md) |
