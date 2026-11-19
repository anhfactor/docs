# Online payment

Online payment is one of the main payment methods at GreenNode Service. Currently, online payment method applies to:

* **Target audience:** Prepaid users.
* **Source of funds:**
  * GreenNode Wallet (Credit Wallet).
  * Online payment gateway: MoMo, ZaloPay, etc.
  * Direct bank transfer to GreenNode's bank account:
    * Account name: CÔNG TY CỔ PHẦN DỊCH VỤ - DỮ LIỆU CÔNG NGHỆ THÔNG TIN VI NA
    * Account number: 04301010052860
    * Bank: MSB / Maritime Bank (Vietnam Maritime Commercial Joint Stock Bank)
    * Branch: Tan Binh
    * Transfer description: your order code
* **Tasks:**
  * Users choose the payment method and confirm the payment.
  * The system performs the payment.
    * Successful payment: Resources are provided according to the configuration, and transaction occurs in [Payment History](https://dashboard.console.greennode.ai/payment-history) and [Credit History](https://dashboard.console.greennode.ai/credit-history) (if using credit).
    * Payment failed: Cancel the task.
  * Provide resources according to the configuration:
    * Success: Generate invoice history in [Billing History](https://dashboard.console.greennode.ai/billing-report).
    * Failure: Refund (generate refund transaction in [Credit History](https://dashboard.console.greennode.ai/credit-history)), Cancel the task.
* **Result when completing the task:**
  * Generate transaction histories in [Credit History](https://dashboard.console.greennode.ai/credit-history), [Payment History](https://dashboard.console.greennode.ai/payment-history), and [Billing History](https://dashboard.console.greennode.ai/billing-report).

**Currently, the online payment feature at GreenNode supports the following payment methods:**

* **Payment with GreenNode Wallet (Credit)**
  * Pay the entire order with Credit (if the available balance is sufficient).
  * In case of insufficient Credit balance, users can choose **Top up & Pay**: Use the entire available credit balance, and the remaining amount will be topped up via the online payment gateway
* **Pay through the payment gateway:** Pay the full value of the order through the online payment gateway without affecting the Credit Wallet (currently supporting payment methods such as MoMo, Zalo Pay, etc.).

In addition, when selecting the payment method through the payment gateway, GreenNode Service provides another payment method called Payment on Behalf.

#### Payment on Behalf

Payment on Behalf is generated to support business or individual customers who are prepaid users and need to use GreenNode Service resources but depend on the financial aspect of other individuals/businesses.

Payment on Behalf is only available when users choose to pay through the online payment gateway.

At the step of confirming the deduction, instead of pressing Pay, users **click Share**, with the purpose of authorizing the payment:

* Step 1: Click **Share**.
* Step 2: Enter the email of the person authorized to **pay**, then click **Confirm**.
  * The system sends an email with a link to the order payment page. The link is valid for 3 days from the time the email is received.
* Step 3: The authorized person accesses the URL sent in the email (provided the URL is still valid).
* Step 4: The authorized person confirms the order payment.
* Step 5: The system will provide the resources after the successful confirmation of payment.
* Step 6: After the resources are provisioned, the system generates the corresponding invoice for the user who requested the payment on behalf. If an error occurs during provisioning, the task is cancelled and the amount is refunded to the GreenNode wallet of the user who requested the payment on behalf.

