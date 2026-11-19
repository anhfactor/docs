# Charging Fee

## Overview

We currently support **2 types of users**: prepaid and postpaid, with **2 billing methods**: Pay monthly and Pay as you go.

* **Pay monthly (Package):** You purchase a fixed amount of data in advance and pay a fixed fee regardless of how much you use. Advantages include stable costs and easy budgeting, suitable for stable, predictable workloads. The price per GB is usually cheaper if you're close to using your full quota. However, it can be wasteful if you don't use your entire quota.
* **Pay as you go (PAYG):** Precisely measures your usage across different storage tiers — you pay only for what you use. Advantages include cost optimization, especially for fluctuating usage, and no forecasting is required. Suitable for startups or those with unstable workloads. However, costs are difficult to predict, and you must constantly monitor usage to avoid sudden spikes.

When you create a new project, we support changing the quota of the storage package to a certain value.

Initially, when you successfully register for a GreenNode account, we classify you as a **prepaid user** by default. That means you need to pay for a storage package before you can use the service, and the storage package will have a duration depending on the cycle you choose.

If you have the need and ensure some conditions on spending indicators, we can support **converting your user form from prepaid to postpaid**, or you might consider using a payment plan based on storage capacity. In that case, you do not need to pay when purchasing a storage package — the monthly invoice value will be calculated based on the actual capacity, requests, etc. that you use.

You can choose the appropriate form to optimize your or your unit's storage costs. For more details, please refer to [Manage invoices, costs & resources on GreenNode](../../billing-management/).

***

## Storage Pricing

The pricing below applies to all Object Storage regions (HCM03, HAN02, HCM04).

|                                  | Gold        | Gold (PAYG)   | Gold High Perf | Gold High Perf (PAYG) | Instant Archive | Instant Archive (PAYG) |
| -------------------------------- | ----------- | ------------- | -------------- | --------------------- | --------------- | ---------------------- |
| **Storage price** (VND/GB/month) | 1,000       | 1,400         | 3,400          | 4,760                 | 530             | 742                    |
| **Request**                      | Unlimited   | Unlimited     | Unlimited      | Unlimited             | Unlimited       | Unlimited              |
| **Traffic download (free)**      | Free x10    | Free x10      | —              | —                     | Free x2         | Free x2                |
| **Traffic upload**               | Free        | Free          | —              | —                     | Free            | Free                   |
| **Data retrieval time**          | Immediately | Immediately   | —              | —                     | Immediately     | Immediately            |
| **Billing method**               | Package     | Pay as you go | Package        | Pay as you go         | Package         | Pay as you go          |
| **Billing unit**                 | GB          | GB            | GB/30 days     | GB                    | GB              | GB                     |
| **Minimum package size**         | 30 GB       | 1 GB          | 30 GB          | 1 GB                  | 30 GB           | 1 GB                   |

***

## Extra Fees

|                                             | Gold    | Gold High Perf & Gold High Perf PAYG | Gold (PAYG) | Instant Archive | Instant Archive (PAYG) |
| ------------------------------------------- | ------- | ------------------------------------ | ----------- | --------------- | ---------------------- |
| **Domestic download traffic** (VND/GB)      | 280     | 280                                  | 280         | 280             | 280                    |
| **International download traffic** (VND/GB) | 330–580 | 330–580                              | 330–580     | 330–580         | 330–580                |

> **Notes on free Traffic download:**
>
> * **Gold:** Free download quota equals 10× your storage size (e.g., storing 30 GB → 300 GB free download/month).
> * **Instant Archive:** Free download quota equals 2× your storage size (e.g., storing 30 GB → 60 GB free download/month).
> * When exceeding the free tier, traffic is charged at the **Domestic / International download** rates shown in the Extra Fees table above.
