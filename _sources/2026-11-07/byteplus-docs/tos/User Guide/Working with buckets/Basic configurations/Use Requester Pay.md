---
title: "Use Requester Pay"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Using-requester-pays"
---

Requester pays is a billing model that transfers data access costs to the requester. The user initiating the data request pays for traffic and request fees incurred during access, while the bucket owner only pays for storage and other related fees. If you want to share data but avoid paying the access costs, you can enable requester pays for your bucket. This article explains the use cases, cost details, and steps to enable requester pays.

<span id="f1175bdf"></span>
## Use cases


* Sharing datasets

   To meet customer demands for data resources, cloud data integrators often need to share large datasets, but costs increase as access volumes grow. Requester pays ensures that users who actually use the data bear the access costs, preventing the data owner from incurring extra expenses.

   The configuration steps are as follows:

   1. First, set the read and write permissions of the shared dataset's bucket to public read. For detailed steps, see [Configuring a Bucket ACL](https://docs.byteplus.com/docs/tos/docs-configuring-a-bucket-acl).

   2. Next, you need to enable the requester pays feature for the bucket.

* Deliver production data

   The bioinformatics company needs to collect and analyze a large amount of data, then send the analysis results to the end customers. After enabling requester pays, end customers bear the cost when accessing the data, reducing the bioinformatics company's operating expenses.

   Follow these configuration steps:

   1. First, set the read and write permissions of the production data bucket to private. For detailed steps, see [Configuring a Bucket ACL](https://docs.byteplus.com/docs/tos/docs-configuring-a-bucket-acl).

   2. Second, enable the requester pays feature for the bucket.

   3. Then, grant the end customers access to the required data through the bucket policy.


<span id="62b0c8f8"></span>
## Fee Description

Before enabling requester pay on the bucket, all fees are covered by the bucket owner. After enabling requester pay on the bucket, the requester pays for traffic and request counts generated during access, while the bucket owner only pays for storage and other fees. The billing items each party must pay are described as follows:


|**Category** |**Billable Item** |**Payer** |
|---|---|---|
|[Storage Fee](https://docs.byteplus.com/docs/tos/docs-storage-fee) |Storage Fee |Bucket Owner |
||Storage Fee for Insufficient Duration |Bucket Owner |
|[Traffic Fee](https://docs.byteplus.com/docs/tos/docs-traffic-fee) |Public Network Egress Traffic Fee |Requester |
||CDN Origin Traffic Fee |Requester |
||Cross\-region replication traffic fee |Bucket owner |
||Cross\-domain access traffic fee |Bucket owner |
|[Request Fee](https://docs.byteplus.com/docs/tos/docs-request-fee) |Put request count fee |Requester |
||Get request count fee |Requester |
||Retrieval request count fee |Requester |
|[Data Retrieval Fee](https://docs.byteplus.com/docs/tos/docs-data-retrieval-fee) |Data retrieval fee |Bucket owner |
|[Data Processing Fee](https://docs.byteplus.com/docs/tos/docs-data-processing-fee) |Image processing fee |Bucket owner |
||Image advanced compression fee |Bucket owner |
||Video frame extraction fee |Bucket owner |
||Anomalous image detection fee |Bucket owner |
||intelligent tiered storage object monitoring fee |bucket owner |
|[Temporary Storage Fee](https://docs.byteplus.com/docs/tos/docs-temporary-storage-fee) |temporary storage fee |bucket owner |


<span id="87df5c3a"></span>
## Request Instructions

When accessing a requester pay bucket, a requester other than the bucket owner must include `x-tos-request-payer` with the value `requester` in the request to indicate awareness and acceptance of associated fees; otherwise, the request fails. The specific method to include this parameter is as follows:


* For POST API requests, the requester must add the `x-tos-request-payer: requester` parameter in the request body.

* For PUT, GET, and other API request types, the requester must add the `x-tos-request-payer: requester` parameter in the request header.

* For presigned URLs, the requester must add the `x-tos-request-payer=requester` parameter in the request query.


For example, when calling GetObject to download an object from a requester pay bucket, a request example is as follows:

```JSON
GET /objectName HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
x-tos-request-payer: requester
```


The requester pays feature only controls which account is charged and does not replace existing permission controls. Requesters other than the bucket owner must include `x-tos-request-payer: requester` in the request and have bucket access rights to successfully initiate the request.

The bucket owner does not need to include the `x-tos-request-payer` parameter when accessing a requester pays bucket. When the bucket owner accesses the bucket as the requester, traffic and request fees are charged to the bucket owner’s account.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">buckets enabled with requester pays do not support anonymous access. requesters must provide authentication information when accessing such buckets so TOS can identify and charge them.</div>


<span id="7af1d8b3"></span>
## Enable requester pay


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. In the left navigation pane,select **Basic configurations \> Requester Pay**.

4. On the **Requester pay** page, click **Edit**.

5. Select **Enable** for requester pays, then click **Select**.

6. In the pop\-up dialog, click **Confirm**.


<span id="78308d90"></span>
## Disable requester pay

After disabling requester pays, access fees generated by the bucket will be borne by the bucket owner, not the requester.


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. In the left navigation pane,select **Basic configurations \> Requester Pay**.

4. On the **Requester pay** page, click **Edit**.

5. Select **Disabled** for requester pays, then click **Select**.

6. In the pop\-up dialog, click **Confirm**.
