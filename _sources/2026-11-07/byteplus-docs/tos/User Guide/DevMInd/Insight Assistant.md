---
title: "Insight Assistant"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/DevMind-Insight-Assistant"
---

Insight Assistant provides access to [TOS Agent](https://docs.byteplus.com/en/docs/tos/TOS-Overview?lang=en) for data insights scenarios. TOS Agent, designed by BytePlus for object storage applications, is an intelligent assistant built on large language models. You can interact with the agent using natural language. The agent can perform O&M tasks and multimodel retrieval. It can also provide data insights and recommendations. This eliminates the need to navigate console menus or consult documentation.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">TOS Agent is currently in closed beta. Please contact your account manager for access.</div>


<span id="BvTCaqGk"></span>
## Preset cards

Insight Assistant provides preset cards with recommended questions that are categorized by business purpose. Submit your request directly by clicking a card, or rewrite the prompt to better fit your needs.

<span id="UqTQDSXE"></span>
## Use cases


<Tabs>
<Tab zoneid="OFnYZNhjRG" title="Log analysis">
<TabTitle>Log analysis</TabTitle>

<span id="PNNhlziu"></span>
### Recommended use cases


* **Daily operations and troubleshooting**: Use natural language to identify periods with abnormal traffic, requests, or status codes, as well as the affected buckets, without writing SQL statements.

* **Hotspot identification and delivery optimization**: Analyze hotspots based on client IP address, referrer, the most frequently accessed objects, and data transfer (egress). Receive recommendations for access paths and caching strategies.

* **Root cause analysis of errors**: Quickly reconstruct the context of a single anomalous request by drilling down into raw access logs and filtering by ErrorCode, HTTPStatus, Operation, RequestId, and other conditions.

* **Security audit**: Quickly trace high\-risk operations, such as deletions, overwrites, and multipart uploads. Export the operation time, source IP address, and requester identity for compliance auditing purposes.

* **Near\-real\-time capacity change analysis**: Quickly calculate storage increases and historical object version changes caused by requests over a specified time period based on DeltaDataSize and HistoricalVersionDeltaSize in logs.


<span id="sI03lYdi"></span>
### Example

Suppose you enter a query into the chat box. The agent would compile statistics from the access logs by operation and HTTP status. Then, the agent would return a top N table of operations by request count, highlighting the dominant operations and those with concentrated error codes.

Sample query:

```JSON
Bucket: * | SELECT
          "Operation" AS Action,
          COUNT(*) AS `Request Count`, 
          HTTPStatus AS `Response Code`,
          COUNT(*) * 100.0 / NULLIF(SUM(COUNT(*)) OVER (), 0) AS `Request Percentage(%)`
        WHERE "Operation" IS NOT NULL AND "Operation" <> '-'
        GROUP BY "Action", `Response Code`
        ORDER BY `Request Count` DESC
        LIMIT 50 
```





</Tab>
<Tab zoneid="LhUolbpjlf" title="Storage Lens">
<TabTitle>Storage Lens</TabTitle>

<span id="AqGbPETL"></span>
### Recommended use cases


* **Capacity planning:**  View long\-term growth trends in storage usage and object count. Quickly assess whether current storage capacity meets business expectations. Break down growth sources by region, bucket, or storage type.

* **Cost optimization:**  Quickly identify your top storage consumers by bucket or prefix. Pinpoint the primary cost drivers and prioritize governance efforts.

* **Storage tiering:**  Analyze how your data is distributed and accessed across various storage types, such as Standard Storage, Infrequent Access Storage, Archive, and Cold Archive. This will help you determine if your current tiering strategy is appropriate.

* **Historical version governance:**  Identify buckets with the largest amount of historical object version bytes and receive governance recommendations. Please note that Insight Assistant cannot delete lifecycle rules involving historical object versions for you.

* **Incomplete multipart upload governance:**  Identify long\-running multipart uploads and the associated buckets. Estimate wasted storage costs.

* **Governance of multi‑workload shared buckets** Use prefix aggregation to identify growth in storage usage and the number of objects in each workload's directory.


<span id="jQqrzUlP"></span>
### Example

Suppose you type "**Find the largest bucket in Region XX**" into the chat box. Then, the agent would return a list of buckets in that region, ranked by data size. Along with each bucket, you would receive its data size, stability notes, and an overall conclusion. This can help you quickly identify the main cost sources and abnormal fluctuations.


</Tab>
</Tabs>


<span id="zXCYrFez"></span>
### 

&nbsp;
