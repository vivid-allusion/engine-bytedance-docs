---
title: "Overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/TOS-Overview"
---

BytePlus TOS now offers TOS Agent, an intelligent service powered by large language models. TOS Agent facilitates natural language interactions for managing buckets and objects, diagnosing access anomalies, analyzing data, and viewing billing details. It also provides semantic retrieval and conversational capabilities for multimodal data, including videos, images, and documents. Furthermore, TOS Agent can automatically parse user intent, plan and execute multi\-step tasks based on API chaining, and visualize the execution process and results within the workspace. All operations are governed by risk\-based controls to ensure data security.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">TOS Agent is currently in closed beta. Please contact your account manager for access.</div>


<span id="IaahHJzA"></span>
## Prerequisites


* You have created a BytePlus account and completed real name verification.

* You have [activated TOS](https://docs.byteplus.com/en/docs/tos/docs-quick-start_1).

* For an Identity and Access Management (IAM) user to manage a bucket via TOS Agent, that user must have the necessary permissions. For information on obtaining the necessary permissions, see [Access control overview](https://docs.byteplus.com/en/docs/tos/docs--overview).

* To use Chat to SenseFlow to manage data in a bucket, make sure the SenseFlow multimodel retrieval module is enabled for that bucket.


<span id="6h2T7j5U"></span>
## Notes


* TOS Agent has built\-in guardrails that effectively prevent the accidental deletion of user data. You can use it with confidence.

* The maximum length of a single prompt is 8,000 characters.

* Any content generated or results identified by TOS Agent based on prompts are for reference only.


<span id="dEQDm1M1"></span>
## Features

<span id="JiPWJQoo"></span>
### Intelligent O&M

TOS Agent can perform O&M operations, such as bucket configuration, access anomaly diagnosis, and health checks, based on natural language inputs. This makes it ideal for scenarios requiring rapid, multi\-step configuration; troubleshooting access anomalies; or performing periodic health assessments of buckets.


* **Access anomaly diagnosis**

   You can send inaccessible object links or error messages to TOS Agent. The agent will then automatically initiate multi\-step diagnostics, identify the root cause, and provide actionable repair suggestions.

* **Bucket health check**

   You can ask TOS Agent to perform a health check on a bucket. The agent will then review four dimensions: security, data protection, capacity management, and basic information. The agent will output the status and description of each dimension, as well as provide optimization recommendations for those posing risks. Once you confirm the recommendations, the agent can execute the necessary repairs step by step.


<span id="E6eSw5l8"></span>
### Data analytics

TOS Agent can act as your data analysis assistant. It supports queries about bucket resource usage, such as storage status, bandwidth, throttling, and overall assessment. This helps you understand your resource usage.

<span id="CpcRd2Ts"></span>
### Multimodal retrieval (Chat to SenseFlow)

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The multimodal semantic retrieval capability relies on the TOS SenseFlow feature.</div>


With SenseFlow's data indexing capability, TOS Agent can conduct natural language searches and have conversations with you about the multimodal data in your bucket, such as videos, images, and documents. This is useful when you need to find files in large amounts of unstructured data based on their content, such as when retrieving security footage, media assets, or enterprise documents.

<span id="ob6L2kcu"></span>
### Q&A

TOS Agent integrates the TOS knowledge base to provide intelligent Q&A regarding features, billing, quotas, and best practices.

<span id="eev6v0TJ"></span>
### Guardrails

TOS Agent implements risk grading to ensure that all operations are performed within safe and controlled boundaries. High\-risk and unauthorized operations are blocked, and users are directed to the official console to perform these operations manually.


|**Risk level** |**Operations included** |**Response** |
|---|---|---|
|Low (read operations) |Bucket/object information queries, configuration viewing, usage and billing analysis, access log retrieval, QoS/quota monitoring, and other List/Get/Describe/Stat API operations. |The agent will perform the operation immediately and provide results in real time. |
|Medium (write operations) |Creating buckets, enabling encryption, enabling versioning, configuring access logs, and configuring Torch Log Service (TLS) access. |Before execution, the agent will display a parameter form in the workspace for your review and confirmation. |
|High (destructive operations) |Batch deletion of buckets/objects, lifecycle rule creation or deletion, WORM rule modifications, cross\-region replication (CRR) configuration, overwriting, static website hosting, and high\-risk bucket policy modifications. |The agent will not perform the operation directly. Instead, it will provide a console link and step\-by\-step instructions. |


<span id="2LpkZgZn"></span>
## Quotas and limits


|**Category** |**Value** |
|---|---|
|Top\-K for multimodal retrieval |Default: 10. Maximum: 20. |
|Pre\-signed URL validity |15 minutes. Generate a new pre\-signed URL after the old one expires. |


<span id="CsBKdMcg"></span>
## Billing notes

TOS Agent is currently free. However, operations on TOS resources triggered via the agent are billed according to standard TOS pricing. For more information, see [Billing overview](https://docs.byteplus.com/en/docs/tos/docs-billing-overview).
