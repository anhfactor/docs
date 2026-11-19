---
description: >-
  This document describes how MaaS usage is billed, including general principles
  for each model type and specific rules for Prepaid and Postpaid accounts.
---

# Pricing

### 1. Pricing Overview

MaaS supports multiple model types, and pricing depends on the type of model used.

Per-model unit prices are shown directly on the [AI Platform Portal](https://aiplatform.console.greennode.ai/models).

#### Model Classification for Billing

Currently, there are two main model groups:

* **Token-based models**
* **Image-based models**

***

### 2. General Principles

#### 2.1. oken-based Models

Applies to models such as:

* Chat
* Completion
* Embedding
* Rerank
* Speech-to-text / Text-to-speech _(_&#x69;f converted into token&#x73;_)_

**Pricing Method**

* Tokens are divided into three types:
  * **Input tokens**
  * **Cache tokens** _(if applicable)_
  * **Output tokens**
* Each token type has **its own unit price**.

<figure><img src="../../.gitbook/assets/image (451).png" alt=""><figcaption></figcaption></figure>

* Pricing is calculated **per 1,000,000 tokens**.

Pricing Formula

```
Total Cost =
((Input tokens − Cache tokens) / 1,000,000) × Input price
+ (Cache tokens / 1,000,000 × Cache price)
+ (Output tokens / 1,000,000 × Output price)
```

Cache tokens are subtracted from input tokens only for models that bill cache tokens separately; for other models all input tokens are billed at the Input price.

***

#### 2.2. Image Generation Models (Gen-Image)

Applies to models such as:

* Text-to-image
* Image-to-image

**Pricing Method**

Pricing is based on:

* Number of images generated
* Configuration of each image, such as:
  * Resolution (kích thước)
  * Quality
  * Style / Model version

⇒ Each image configuration has a different price.

<figure><img src="../../.gitbook/assets/image (452).png" alt=""><figcaption></figcaption></figure>

***

### 3. Detailed Rules by Account Type

#### 3.1. Prepaid Account

**3.1.1.** Usage Principles

* Users must purchase user credits in advance using the Top-up credits feature.

<figure><img src="../../.gitbook/assets/image (455).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (465).png" alt=""><figcaption></figcaption></figure>

* For each model usage:
  * Generated tokens and/or images will be:
    * Calculated based on the corresponding pricing
    * Deducted directly from the current user credit quota
* When quota = 0:
  * All models will be disabled
  * Users must purchase additional quota to continue usage

***

**3.1.2.** User Credit Expiration

* User credits are valid for 1 year
* The validity period is calculated from the most recent top-up date

When user credits expire:

* All models will be disabled
* Users can:
  * Recover user credits from the Billing page

After recovery:

* Previous user credit quota will be lost
* The system will only use the newly recovered quota

Recovery Expiration

* If more than 7 days have passed since user credit expiration:
  * Users must:
    * Reactivate billing
    * Purchase additional user credits if they wish to continue using the service

> It is recommended that users estimate usage in advance and proactively top up credits to avoid service interruptions due to exhausted quota or expired credits.
>
> (The Quota Alarm feature is under development and will be updated in the future.)

***

#### 3.2. Postpaid Account

**3.2.1. Usage Principles**

* User credits have unlimited validity
* Users can use models without pre-purchasing quota
* Usage will be:
  * Recorded in real time
  * Aggregated and billed at the end of each month

***

### 4. Usage Monitoring

To view detailed usage:

* Go to the [**Model Usage**](https://aiplatform.console.greennode.ai/model-usage) **page**
* You can:
  * Select a specific time range
  * View details such as:
    * Tokens input / output / cache
    * Number of generated images
    * Corresponding costs
