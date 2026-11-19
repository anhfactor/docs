---
description: >-
  The Service Level Agreement (SLA) for GreenNode AI MaaS, version 2026.1:
  committed uptime, scope, service credits, maintenance, response times and the
  complaint process.
---

# SLA

{% hint style="info" %}
This page summarises the **AI MaaS (Model as a Service) Service Level Agreement, version 2026.1, effective from November 9th 2026**. The legally binding text is at [GreenNode Terms of Service — SLA](https://greennode.ai/terms-of-service/vietnam/service-level-agreement). If anything here differs, that text prevails.
{% endhint %}

## Committed monthly uptime

| Service | Committed Monthly Uptime Percentage | Calculation Unit | Acceptable Downtime Equivalent |
| --- | --- | --- | --- |
| AI MaaS | **99.90%** | Model | Equivalent to 43 minutes 28 seconds |

**Scope of commitment:** the commitment applies to the availability of the Service for **GreenNode Models**. GreenNode does not commit to any SLA for:

* Third-party Models;
* Performance metrics of the Service, including but not limited to tokens per minute (TPM), requests per minute (RPM), response speed and similar metrics.

## Concepts and definitions

| Term | Definition |
| --- | --- |
| **GreenNode Model** | AI models directly deployed and operated by GreenNode on GreenNode's infrastructure. |
| **Third-party Model** | AI models operated by a third-party provider and made available to the Customer by GreenNode through the Service. The list of models and their classification are published and updated on the Service Console. |
| **Unavailable State** (Downtime) | The period during which the Service is unavailable due to GreenNode's fault, excluding maintenance periods, the permitted unavailability cases and other cases excluded in the SLA. |
| **Monthly Uptime Period** | Total minutes in the month minus the minutes the Service is in the Unavailable State due to GreenNode's fault, excluding maintenance periods, suspension caused by a Force Majeure Event and other excluded cases. |
| **Monthly Downtime Percentage** | Total time in the Unavailable State divided by the total time in the month, multiplied by 100. |
| **Monthly Uptime Percentage** | 100% minus the Monthly Downtime Percentage. |
| **Force Majeure Event** | An event that happens in an objective, unpredictable and irreparable manner despite all necessary measures, including but not limited to natural disasters, enemy sabotage, extreme weather, sabotage actions, protests, strikes and bans from Government Agencies. |
| **Credit** | The value recorded in the Customer's Service account and used to pay for the Service in accordance with GreenNode's pricing policy. |

### When the Service is in the Unavailable State

The Unavailable State is determined when one or more of the following occurs:

* a. The Service system stops responding to the Customer's API requests;
* b. The server operating the Service stops operating.

Time in the Unavailable State is counted from the earlier of (i) the time GreenNode's monitoring system records the incident and (ii) the time the Customer notifies GreenNode of the incident, provided that GreenNode confirms the incident falls within the scope of the Service, until the Service resumes operation.

## Formula

| Service | Formula |
| --- | --- |
| AI MaaS | Uptime = 100% − Monthly Downtime Percentage |

## Service credits

If the Service fails the committed Monthly Uptime Percentage, GreenNode provides a Service credit as **Credit added to the Customer's Service account**:

| Monthly Uptime Percentage | Service Rate to compensate |
| --- | --- |
| From 95% to less than 99.90% | 10% |
| From 90% to less than 95% | 30% |
| Below 90% | 100% |

The compensation value is calculated as follows:

* **Token plan:** when any GreenNode Model in the plan fails the commitment, the Monthly Uptime Percentage is determined for the entire plan and the compensation is calculated on the value of the plan in that month's payment cycle.
* **Pay-as-you-go:** the Monthly Uptime Percentage is determined separately for each affected GreenNode Model and the compensation is calculated on the total Credit the Customer used for that model in the month of the incident.

## Permitted unavailability

* The Service is interrupted due to maintenance under **System maintenance** below.
* The Service is inaccessible due to a Force Majeure Event.
* The Service is unavailable due to interruption, performance degradation, change or discontinuation on the part of the Third-party Model provider, beyond GreenNode's control.
* The Service is unavailable due to causes not arising from GreenNode's fault; Downtime is counted only when the Unavailable State arises from GreenNode's fault.
* Other cases excluded under the SLA, GreenNode's Terms of Service or the service contract (if any).

## System maintenance

Maintenance can be scheduled on any day of the week (including weekends) and at any time of day; GreenNode endeavours to carry it out when it least affects Customers. When maintenance requires a temporary suspension of the Service, GreenNode notifies Customers by telephone, email or on the homepage [greennode.ai](https://greennode.ai/):

| Case | Notice |
| --- | --- |
| Periodic maintenance | Three (03) working days in advance |
| Emergency maintenance | At least thirty (30) minutes in advance |
| Incidents beyond GreenNode's control, including Force Majeure Events | Within four (4) working hours of the incident |

Total maintenance time affecting the Customer's Service in one (1) month **does not exceed 120 minutes**.

## Response and resolution times

Contact: 24/7 support call centre **1900 1549**, website [greennode.ai](https://greennode.ai/) or email [support@greennode.ai](mailto:support@greennode.ai).

| Item | Time |
| --- | --- |
| Response to a troubleshooting request | Within 15 minutes of receiving the request |
| Response and troubleshooting | From 15 minutes up to 48 working hours after responding to the request |
| Serious problems | May be longer, but not more than 72 working hours after responding to the request |

## Complaint process

Send in writing or by email to [support@greennode.ai](mailto:support@greennode.ai), including:

* Email or document subject: **"Request to compensate according to SLA commitment"**;
* The affected account;
* The specific dates, times and moments the Service was in the Unavailable State;
* Error logs or screenshots at the time of the error (blur or hide confidential information);
* Data-loss claims are considered only with an official assessment from an independent, legally authorised assessment organisation; the Customer bears its cost;
* Damages and their value, with supporting documents and invoices;
* The compensation requested.

| Item | Deadline |
| --- | --- |
| Filing a complaint | Within three (3) months of the incident; later complaints are not accepted |
| Response and resolution | Within 15 working days of receipt |

If the Customer is dissatisfied with the resolution, they can send feedback again; it is handled as a new complaint.
