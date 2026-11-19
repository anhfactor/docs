# How to calculate a Snapshot Service Charges

The Snapshot service offers two payment methods to serve different financial goals and strategies of each customer. The two payment methods implemented for the Snapshot service at GreenNode include:

* Prepaid Payment Method.
* Postpaid Payment Method.

These payment methods and fee calculation provide flexibility and control over Snapshot service costs. Users can choose the payment method that best suits their financial strategy and usage needs. It is important to understand the chosen payment method to efficiently manage snapshot costs and maintain continuous access to this service.

#### **1.** Fee Calculation for Snapshots <a href="#cachtinhgiadichvusnapshot-1.cachtinhphisnapshot" id="cachtinhgiadichvusnapshot-1.cachtinhphisnapshot"></a>

The fee calculation for Snapshots applies to both payment methods, including Prepaid and Postpaid.

* **Formula:** The cost of creating a snapshot is calculated based on the size of the snapshot (in gigabytes) and its usage time (typically measured in hours).
* **Usage time:** Users will be charged for the existence time of the snapshot. This time is recorded in hours.
* **Example:** For instance, if you have a snapshot with a size of 100GB and the unit price for the Snapshot Service is 7.7 VND per GB-hour, then the cost will be calculated as follows:
  * Per hour: 7.7 VND \* 100 GB = 770 VND per hour.
  * Per day: 770 VND \* 24 = 18,480 VND per day.
  * Per month: 18,480 \* 30 = 554,400 VND per month.
* **Note:** The unit price provided is for reference only. The actual usage time of the snapshots is recorded hourly, based on the actual size of your snapshots.

#### 2. Prepaid Payment Method <a href="#cachtinhgiadichvusnapshot-2.phuongthucthanhtoantratruoc" id="cachtinhgiadichvusnapshot-2.phuongthucthanhtoantratruoc"></a>

For Prepaid users, GreenNode applies the Hold Credit method to support usage and cost calculation for the Snapshot service. Learn more about Hold Credit at <mark style="background-color:red;">Hold Credit</mark>.

* **Method:** Under the Hold Credit method, users must maintain a prepaid balance sufficient to cover the usage portion of the service in their account.
* **Snapshot Activation:** When activating Snapshot for the first time, users will be directed to GreenNode's payment gateway to record the funds used for the Snapshot service. Note that this action is solely for recording the funds used, users do not incur any fees for the first activation.
* **Snapshot Creation Fee:** When users create a snapshot, the system will not immediately charge the fee, but it will be recorded every hour thereafter. Once a day, the system will perform a Hold Credit for the service usage, this fee is determined based on the size of the snapshot and the usage time on that day.&#x20;
* **Balance Management:** Users are responsible for managing their prepaid balance to ensure it is sufficient to cover the planned usage of snapshots, this balance must be enough to cover the service usage up to the current time and the next 3 days. See details at Hold Credit.
* **Low Balance Notification:** To avoid service interruption, the system will send a notification when the prepaid balance drops below a specific threshold, recommending users to top up. In cases where reminders have been sent multiple times, but the balance still continuously fails to meet the requirement, GreenNode will temporarily suspend the service ([Disable Snapshot service](disable-snapshot-service.md)) for the user.

#### **3.** Postpaid Payment Method <a href="#cachtinhgiadichvusnapshot-3.phuongthucthanhtoantrasau" id="cachtinhgiadichvusnapshot-3.phuongthucthanhtoantrasau"></a>

For Postpaid users, GreenNode applies the pay-as-you-go method, similar to other services.

* **Payment Cycle:** Users using the postpaid payment method do not need to maintain a prepaid balance. Instead, service fees for snapshots are calculated at the end of each monthly billing cycle.
* **Flexibility in Snapshot Usage:** With postpaid payment, users can activate & create snapshots as needed without worrying about available balances, providing greater flexibility.
* **Monthly Payment Invoice:** Snapshot service fees are listed on the monthly payment statement, providing users with a clear summary of snapshot-related costs.&#x20;
* **On-time Payment:** Paying the monthly bill on time is crucial to ensure continuous access to the Snapshot service.
* **Usage Tracking:** Users can track their Snapshot usage through the payment gateway, helping them understand resource usage and costs..

#### &#x20;<a href="#cachtinhgiadichvusnapshot-4.chudelienquan" id="cachtinhgiadichvusnapshot-4.chudelienquan"></a>
