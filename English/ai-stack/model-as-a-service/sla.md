---
description: >-
  The Service Level Agreement (SLA) for GreenNode AI MaaS, version 2026.1,
  effective from November 9th 2026.
---

# SLA

{% hint style="info" %}
The content below is quoted verbatim from the AI MaaS Service Level Agreement at [greennode.ai/terms-of-service/vietnam/service-level-agreement](https://greennode.ai/terms-of-service/vietnam/service-level-agreement).
{% endhint %}

**AI MaaS (Model as a Service)**

_Version 2026.1, effective from November 9th 2026_

This Service Level Agreement ("SLA") is a commitment of Vi Na Data Information Technology - Service Joint Stock Company ("GreenNode") to the Customer, the party using the services of GreenNode, and is considered as a commitment on service quality to ensure benefits for all Customers.

This SLA applies to GreenNode's AI MaaS (Model as a Service) service (the "Service") – a service that provides artificial intelligence (AI) models through an application programming interface (API), which is further described [here](https://docs.greennode.ai/ai-stack/model-as-a-service).

## 1. CONCEPTS AND DEFINITIONS

**1.1.** "Customer"/ "Service User": means any individual or entity using GreenNode's Service.

**1.2.** "GreenNode Model": means the AI models directly deployed and operated by GreenNode on GreenNode's infrastructure. "Third-party Model": means the AI models operated by a third-party provider and made available to the Customer by GreenNode through the Service. The list of available models and theirification are published and updated by GreenNode on the [Service Console](https://aiplatform.console.greennode.ai/models).

**1.3.**

"Unavailable State" or "Downtime": refers to the period during which the Service is unavailable due to GreenNode's fault and excludes: (i) maintenance periods; (ii) periods during which the Service falls under any of the permitted unavailability cases as stipulated in Clause 4 of this SLA; and (iii) any other cases as excluded in this SLA.

The "Unavailable State" of the Service shall be determined when one or more of the following cases occurs:

* a. The Service system stops responding to the Customer's API requests;
* b. The server operating the Service stops operating.

The time in the Unavailable State is counted from the earlier of (i) the time GreenNode's monitoring system records the incident and (ii) the time the Customer notifies GreenNode of the incident in accordance with Clause 6 of this SLA, provided that GreenNode confirms the incident falls within the scope of the Service, until the time the Service resumes operation.

**1.4.** "Monthly Uptime Period": means the total number of minutes in the month minus the total number of minutes in that month during which the Service is in the Unavailable State due to GreenNode's fault, excluding maintenance periods, Service suspension caused by a Force Majeure Event and other cases excluded in this SLA.

**1.5.** "Monthly Downtime Percentage": is calculated by dividing the total time the Service is in the Unavailable State by the total time in the month, then multiplied by 100.

**1.6.** "Monthly Uptime Percentage": is calculated as 100% minus the "Monthly Downtime Percentage".

**1.7.** "Force Majeure Event": means an event that happens in an objective, unpredictable and irreparable manner despite the application of all necessary measures and in the permissible capacity, including but not limited to natural disasters, enemy sabotage, extreme weather phenomena, sabotage actions, protests, strikes, and bans from Government Agencies.

**1.8.** "Credit": means the value recorded in the Customer's Service account and used to pay for the use of the Service in accordance with GreenNode's pricing policy.

## 2. MONTHLY UPTIME PERCENTAGE FORMULA

| **Service** | **Formula** |
| --- | --- |
| AI MaaS | Uptime = 100% - "Monthly Downtime Percentage" |

## 3. GREENNODE'S COMMITMENT ON MONTHLY UPTIME PERCENTAGE

**3.1.**

Service Level Commitment

| **Services** | **Committed Monthly Uptime Percentage** | **Calculation Unit** | **Acceptable Downtime Equivalent** |
| --- | --- | --- | --- |
| AI MaaS | 99.90% | Model | Equivalent to 43 minutes 28 seconds |

Scope of commitment: the above commitment applies to the availability of the Service for GreenNode Models. GreenNode does not commit to any SLA for:

* a. Third-party Models;
* b. Performance metrics of the Service, including but not limited to tokens per minute (TPM), requests per minute (RPM), response speed and similar metrics.

**3.2.**

GreenNode's responsibility for failure of Service Level Commitment

In case that the Service fails the committed Monthly Uptime Percentage as stated above, GreenNode is responsible for providing the corresponding Service credit to the Customer in the form of Credit added to the Customer's Service account. The Service rate to compensate shall be determined as follows:

| **Monthly Uptime Percentage** | **Service Rate to compensate** |
| --- | --- |
| From 95% to less than 99.90% | 10% |
| From 90% to less than 95% | 30% |
| Below 90% | 100% |

The compensation value is calculated based on the above percentage as follows:

* a. For Customers using a token plan: when any GreenNode Model included in the plan fails the commitment, the Monthly Uptime Percentage is determined for the entire plan and the compensation value is calculated on the value of the plan in the payment cycle of that month;
* b. For pay-as-you-go Customers: the Monthly Uptime Percentage is determined separately for each affected GreenNode Model and the compensation value is calculated on the total Credit the Customer has used for that model in the month in which the incident occurs.

## 4. PERMITTED UNAVAILABILITY

**4.1.** Service is interrupted due to the maintenance in accordance with Clause 5 of this SLA.

**4.2.** The Service is inaccessible due to Force Majeure Event.

**4.3.** The Service is unavailable due to interruption, performance degradation, change or discontinuation on the part of the Third-party Model provider, which is beyond GreenNode's control.

**4.4.** The Service is unavailable due to causes not arising from GreenNode's fault; Downtime is counted only when the Unavailable State arises from GreenNode's fault.

**4.5.** Other cases excluded under this SLA, GreenNode's Terms of Service or the service contract (if any).

## 5. SYSTEM MAINTENANCE

**5.1.** System maintenance is mandatory to ensure the continuity of the Service provided to Customer. The maintenance can be scheduled on any day of the week (including weekend) and at any time of the day. However, GreenNode shall endeavor to carry out the maintenance at the time that least affects Customer's use of the Service.

**5.2.**

When performing mandatory system maintenance requiring temporary suspension of the Service, GreenNode shall notify Customer in advance via telephone or email on GreenNode's system or on the homepage [https://greennode.ai/](https://greennode.ai/), within the advance notice period as follows:

* a. Three (03) working days in advance before expected day of periodic maintenance.
* b. Thirty (30) minutes in advance before expected time of maintenance in emergency maintenance cases.
* c. Within four (4) working hours since the time the incident occurs for emergency maintenance due to incidents beyond the control of GreenNode, including the occurrence of any Force Majeure Event.

**5.3.** GreenNode commits that the total maintenance time affecting the Customer's Service in one (1) month shall not exceed one hundred and twenty (120) minutes.

## 6. COMMITMENT ON THE TIME FOR FEEDBACK, RESPONSE AND RESOLUTION OF PROBLEMS

**6.1.**

Forms of contact for receiving and solving problems:

* a. Via 24/7 support call center: 1900 1549
* b. Via website or email: [https://greennode.ai/](https://greennode.ai/); [support@greennode.ai](mailto:support@greennode.ai)

**6.2.**

Response time:

* a. Response time for troubleshooting request: within 15 minutes since the time the request is received.
* b. Response time and troubleshooting time for the Customer's problems: within 15 minutes up to 48 working hours since the time of responding to troubleshooting request.
* c. For serious problems, response time can be longer, but not exceed 72 working hours since the time of responding to troubleshooting request.

## 7. PROCESS OF RECEIVING AND RESPONDING TO COMPLAINTS

Forms of contact for receiving complaints: in document or send email via [support@greennode.ai](mailto:support@greennode.ai)

**7.1.**

Content of complaints: in order to save the Customer's time, when sending complaints to GreenNode, the Customer should sufficiently provide the following information:

* a. Email or Document subject must be clearly stated: "Request to compensate according to SLA commitment";
* b. The information of the account affected;
* c. Specific date and time and the moments when the system, and Service used by the Customer fall into the Unavailable State;
* d. Logs recording errors or screenshots at the time the error occurs (the Customer's confidential information should be blurred or hidden);
* e. All claims regarding data loss shall only be received and considered by GreenNode when accompanied by an official assessment document issued by an independent assessment organization with legal functions (which clearlyentifies the cause of data loss, the list and volume of lost data). The entire cost related to this assessment shall be borne by the Customer.
* f. Damages to the Customer and the value of damages accompanied by relevant documents and invoices;
* g. The level of compensation that the Customer requires.

**7.2.** Time to receive complaints: within three (3) months since the incident occurs; more than the above-mentioned time, GreenNode shall not accept and resolve any relevant complaints.

**7.3.** Time to respond and resolve complaints: within 15 (fifteen) working days since the day the complaint is received.

**7.4.** In case the Customer is dissatisfied with the resolution documents of GreenNode, the Customer can resend feedback to GreenNode; in this case, the Customer's feedback shall be received and processed as a new Complaint.
