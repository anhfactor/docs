---
hidden: true
---

# Converting resource from POC to Prepaid

At GreenNode Service, we support users to flexibly change the purpose of using resources, from the POC stage to a paid service on the same resource. Changing the purpose of using brings significant benefits such as _**saving time to initialize new resources (configuration, payment, ...), optimizing usage costs, reusing old data for new purposes, ...**_

To perform the conversion, please follow the instructions below:

* **Step 1:** Access the resource management website
* **Step 2:** In the resource information management section, select the action "Stop POC"
* **Step 3:** Confirm to stop POC when a confirmation window pops up, at this time the user will be redirected to the resource payment page
* **Step 4:** At the payment page, users perform the same as new purchases, according to their usage needs.
  * Select resource usage time
  * Turn on auto-renewal
  * Choose to pay by GreenNode credit or directly from the payment gateway
* **Step 5:** After successful payment, users will be redirected to the resource management website to check information and continue using resources.

At this time, the system has recorded the resource has completed the conversion process to paid service, users can check the service invoice information (except K8s service (vContainer)) at the vConsole website - Invoice history: [https://dashboard.console.greennode.ai/billing-report](https://dashboard.console.greennode.ai/billing-report)

## **K8s Resource Migration (vContainer)** <a href="#chuyendoihinhthucsudungtupocsangdichvutraphi-chuyendoitainguyenk8s-vcontainer" id="chuyendoihinhthucsudungtupocsangdichvutraphi-chuyendoitainguyenk8s-vcontainer"></a>

***

To help users have a more detailed view of the above process, below are the steps to guide you in converting a type of resource, specifically a Cluster (in the K8s/vContainer service group) to a paid service:

* **Step 1:** Access the resource management website at vServer portal [https://hcm-3.console.greennode.ai/vserver/billing](https://hcm-3.console.greennode.ai/vserver/billing)
* **Step 2:** Select the POC cluster to convert (use the search toolbar, search by name/resource identifier to filter out the cluster to find). Refer to the image below:
* **Step 3:** Select the action " **Stop POC** " for the cluster found in Step 2
* **Step 4:** Confirm the conversion again in the pop-up window, now the user will be redirected to the payment page
  * Check the price information at the Check **out page.** Click **"Continue"** to continue the process.
  * **Confirm payment by "Hold"** method : learn more about "Hold" method [here](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/quan-ly-hoa-don-chi-phi-and-tai-nguyen-tren-vng-cloud/trai-nghiem-billing-and-kenh-thanh-toan/ve-billing-and-payment/thanh-toan/tam-giu-credit)
  * The system will temporarily hold credit for the above resource for 3 days of service use.
* **Step 5:** After successful payment, users will be redirected to the vServer website to check information and continue using resources.

{% hint style="info" %}
**Hint:**

* For resources belonging to the K8s/vContainer service group, the system will not issue invoices at the time of conversion, but invoices will be recorded in the monthly reconciliation period of this service based on actual usage costs.
* Converting cluster resources to paid services means converting the entire persistent volume (initialized during the cluster POC process) to paid services at the same time.
{% endhint %}
