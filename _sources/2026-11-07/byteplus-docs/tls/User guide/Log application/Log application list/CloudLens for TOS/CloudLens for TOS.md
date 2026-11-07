---
title: "CloudLens for TOS"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/CloudLens_for_TOS"
---

This topic introduces the CloudLens for TOS features provided by the TLS app store for log observation of cloud products.

<span id="b31f5186"></span>
## Feature description

The CloudLens for TOS log application provides log observability for cloud products built on TOS buckets, supporting log analysis and storage lens.

Both log analysis and storage lens serve to monitor and analyze TOS data, offering visual statistics on bucket operations and asset data. The comparison of their capabilities is described in the following chart. You can choose the appropriate method to view bucket usage as needed, helping with operational monitoring and maintenance decisions. For billing details, see [Billing notes](https://docs.byteplus.com/docs/tls/CloudLens_for_TOS#4fe96fce).


* Comparison: log analysis vs. pivot dashboards

   
   |Dimension |[Log analysis](https://docs.byteplus.com/docs/tls/CloudLens_for_TOS#60b59098) |[Storage Lens](https://docs.byteplus.com/docs/tls/CloudLens_for_TOS#0b58509c) |
   |---|---|---|
   |Features overview |Collect access detail logs of the storage bucket in real time with second\-level reporting frequency to facilitate metric retrieval and analysis. With high timeliness with near real\-time data, it is suitable for scenarios like troubleshooting and access auditing where immediate results are needed. |Configure the bucket metric collection range on demand, aggregate storage and access metrics daily, and support quick view, trends, distribution, and Top N analysis. Unified observation across multiple buckets, ideal for scenarios requiring long\-term, multidimensional statistics, such as usage comparison between buckets, cost allocation, and hotspot prefix analysis. |
   |Time dimension |Real\-time collection (the storage period defaults to 7 days and can be customized) |Aggregated daily (retention period defauls to 450 days and modification is not supported) |
   |Data range |Bucket level. |* Region / Storage type / Bucket level.<br><br>* Advanced features support prefix dimension. |
   |Chart description |Resource usage, heat statistics, access analysis, security analysis, and query and analysis. |Total storage, object count, bucket count, current/historical version bytes, unmerged shard bytes (advanced features also include upload/delete byte counts), and more. |
   |Data source/implementation |Access detail logs for TOS API requests can be viewed directly in the console. |Pivot dashboards are required. |
   |Feature positioning |Traffic statistics for TOS API requests, troubleshooting, exception analysis, and access audit. |Analyze growth trends and optimize costs |
   

* Use cases

   
   |Use cases |Description |
   |---|---|
   |[Log analysis](https://docs.byteplus.com/docs/tls/CloudLens_for_TOS#60b59098) |* Quickly view recent usage, traffic, requests, bandwidth, and status codes for a bucket or all buckets.<br><br>* Monitor daily operations and quickly troubleshoot sudden spikes in traffic/requests or exceptions in status codes.<br><br>* Only overview\-level data is needed; no additional configuration is required.<br><br>* Since the data is derived from access logs rather than actual measurements, it is not suitable for precise reconciliation or billing. |
   |[Storage Lens](https://docs.byteplus.com/docs/tls/CloudLens_for_TOS#0b58509c) |* Manage storage assets in detail, optimize costs, analyze capacity growth trends, and identify the fastest\-growing buckets or prefixes.<br><br>* Perform multidimensional statistics by region, storage type, bucket, or prefix (prefix dimension requires advanced features).<br><br>* Monitor version bytes, unmerged fragments, and uploaded/deleted bytes to manage assets.<br><br>* Advanced features incur fees.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="default">The <strong>Prefix aggregation</strong> feature within the <strong>Advanced features</strong> functions is not currently supported.</div><br> |
   


<span id="60b59098"></span>
### Log analysis

The CloudLens for TOS log analysis dashboard presents essential telemetry data for object storage buckets, including resource usage, access trends, traffic analysis, and security analysis. For details on log fields, see [Log analysis fields](https://docs.byteplus.com/docs/tls/Log-analysis-fields).

The log analysis dashboard displays key monitoring data such as bucket usage and traffic, and supports running query and analysis statements to analyze access logs generated during TOS usage.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/742b24e3ccfe4bdc88c574261f8c1414) </span>

Log analysis dashboard features:


|Log analysis |Chart description |Feature purpose |
|---|---|---|
|[Resource usage](https://docs.byteplus.com/docs/tls/Configure-log-analysis-dashboard#e786f898) |View bucket traffic trends, request trends, bucket traffic/bandwidth top 1000, and bucket request top 1000. |* The trend chart helps analyze overall traffic and request patterns.<br><br>* The top chart helps you to quickly identify the target bucket after confirming an abnormal time window. |
|[Heat statistics](https://docs.byteplus.com/docs/tls/Configure-log-analysis-dashboard#08105eba) |Display Operation statistics for the bucket, object size distribution, global access QPS, QPS grouped by bucket, access data volume by prefix, percentage of Top 5 prefix access data volume, read/write ratio by bandwidth, read/write ratio by request count, directory access heat, and prefix metric queries |* Quickly find the directory with the highest heat<br><br>* Quickly identify main access types and exception operation types.<br><br>* Quickly analyze the access heat distribution of large and small files. |
|[Access analysis](https://docs.byteplus.com/docs/tls/Configure-log-analysis-dashboard#f3521c67) |Display the followings: upload volume, download volume, delete volume, PV, UV, upload volume top 1000, download volume top 1000, delete volume top 1000, refer request top 1000, client access top 1000, status code trends, PV/UV trends, error access count, data outbound/external outbound, mirror back\-to\-origin status code trends, file access statistics Top 1000. |* Identify the source of user access<br><br>* Analyze the data volume of user access<br><br>* Determine the entity responsible for abnormal access |
|[Security analysis](https://docs.byteplus.com/docs/tls/Configure-log-analysis-dashboard#60fc6484) |Display file operation trends in the bucket, bucket file deletion statistics, bucket file deletion IP statistics, and file deletion trends. |* Identify trends of high\-risk operations.<br><br>* Evaluate user bucket space. |
|[Query and analysis](https://docs.byteplus.com/docs/tls/Configure-log-analysis-dashboard#ff86a08e) |Go to the query and analysis page for log topics, and customize your query for the relevant log topic. |* Customize flexible queries and analyze logs.<br><br>* Customize visual analysis charts. |


<span id="0b58509c"></span>
### Storage Lens

The pivot dashboard for CloudLens for TOS aggregates data daily by account, region, and bucket, and provides insights into activity metrics, summary metrics, cost optimization, and data protection to help you quickly understand how object storage resources are used. For details on log fields, see [Storage Lens](https://docs.byteplus.com/docs/tls/Data-pivot-fields).

With the pivot dashboard, you can track storage capacity growth trends and identify the fastest\-growing buckets and prefixes. This helps you to determine whether storage growth aligns with expectations and optimize storage costs.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/f38de45fa3b846258fa31cb94910d1a4) </span>

How pivot dashboard metrics are collected:


<Tabs>
<Tab zoneid="T40Q4rXgS2" title="Free metrics">
<TabTitle>Free metrics</TabTitle>

Collect free metrics. This feature is available for all regions and buckets. The metric details are as follows:


* **Summary metrics**: total storage and total number of objects.

* **Cost optimization metrics**: historical version bytes, number of historical version object, number of unmerged multipart upload bytes, and number of unmerged multipart upload object.

* **Data protection metrics**: current version bytes and current version object count.


</Tab>
<Tab zoneid="yGr32Yl0qe" title="Advanced metrics">
<TabTitle>Advanced metrics</TabTitle>

Building on basic metrics, supports activity metrics and prefix aggregation, available only for specific regions and buckets.


* **Activity metrics**:

   Offers advanced metrics such as **uploaded bytes** and **deleted bytes** to help you manage resources more precisely.

* **Prefix aggregation**:

   In addition to statistics based on region, storage type, and bucket dimensions, prefix\-level statistics are also supported. This means that metrics supported include the following: total storage, object count, current version bytes, current version object count, historical version bytes, historical version object count, incomplete multipart upload bytes, and incomplete multipart upload object count.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The <strong>Prefix aggregation</strong> feature within the <strong>Advanced features</strong> functions is not currently supported.   </div>
   


</Tab>
</Tabs>


Dashboard detail overview:

The metrics are presented from perspectives such as overview, region, storage type, bucket, and prefix, including charts for trends, distribution, snapshots, bubble diagrams, and detailed data.


* Trend and distribution charts: used to identify key metric targets.

* Bubble diagram: A data\-visualization diagram that maps data using bubble size to represent a third variable, showing relationships among three numerical variables.



|Storage lens feature |Chart description |Feature purpose |
|---|---|---|
|[Overview](https://docs.byteplus.com/docs/tls/Configure-pivot-dashboard#84bab49a) |Display metric snapshots, metric details, trends and distribution, TopN snapshots, and incremental TopN prefix. |View total TOS storage, total object count, and total bucket count from an overview perspective. |
|[Region](https://docs.byteplus.com/docs/tls/Configure-pivot-dashboard#9f87f946) |Display the trends, distribution, bubble diagram, and data details of the corresponding metrics within the specified area. |Identify capacity concentration and regional differences from a geographic perspective to support cross\-region capacity planning. Conduct in\-depth analysis with summary metrics, cost optimization metrics, and data protection metrics. |
|[Storage types](https://docs.byteplus.com/docs/tls/Configure-pivot-dashboard#1f805bf2) |Display the corresponding metrics trends, distributions, bubble chart, and detailed data for the specified storage type. |Compare capacity trends, daily distribution, and object count for each storage type from a storage perspective. Check if infrequently accessed data remains in standard storage and validate the effectiveness of your tiering strategy. |
|[Bucket](https://docs.byteplus.com/docs/tls/Configure-pivot-dashboard#1fb4b120) |Display trends, distributions, bubble charts, and detailed data for corresponding metrics in the specified bucket. |Identify high\-priority buckets from the bucket perspective, and distinguish between "large capacity with few objects" and "not large capacity but many objects." |
|[Prefix](https://docs.byteplus.com/docs/tls/Configure-pivot-dashboard#f0cdb26f) |Displays the trends, distributions, bubble charts, and detailed data for the specified metrics under the given prefix. |From the prefix perspective (if advanced metrics enable prefix aggregation), locate capacity growth to specific directories using prefix aggregation metrics. |


<span id="d3ebf829"></span>
## Permissions


* When you first access the CloudLens for TOS log application, follow the prompts to complete cross\-service access authorization.

* By default, the main account has full permissions and IAM sub\-accounts have no permissions. If you need to perform this operation using a sub\-account, the main account must grant the following permissions to the sub\-account. For details, see [IAM overview](https://docs.byteplus.com/docs/tls/Managing_permissions_on_Identity_and_Access_Management).

   
   |Feature category |Permissions |
   |---|---|
   |Log application |* tls:CreateApp<br><br>* tls:ModifyApp<br><br>* tls:DescribeApp<br><br>* tls:DescribeApps<br><br>* tls:DeleteApp |
   |Log analysis |* tls:ModifyCloudLensInstanceStatus<br><br>* tls:DescribeCloudLensInstances<br><br>* tls:DescribeCloudLensInstanceStatus<br><br>* tls:DescribeCloudLensTargetTopics<br><br>* tls:DescribeCloudLensOverview |
   |Storage lens |* tls:CreateTosLensTask<br><br>* tls:ModifyTosLensTask<br><br>* tls:DescribeTosLensTasks<br><br>* tls:DescribeTosLensTask<br><br>* tls:DeleteTosLensTask |
   


<span id="884c5f82"></span>
## Resource management

After integrating the CloudLens for TOS log application, the following dedicated log projects and related resources will be generated:


|Dimension |Log project |Log topic |Table topic |
|---|---|---|---|
|Log analysis |`tos-log-<account_id>-<region_id>` |`tos-log-topic`<br><br><br>* Tag is set to `tos`.<br><br>* Pay by feature<br><br>* Used for log analysis and stores TOS API access logs. For field details, see [Log analysis fields](https://docs.byteplus.com/docs/tls/Log-analysis-fields). |None |
|Storage lens |`tos-project-<account_id>-<region_id>` |`tos-lens-topic`<br><br><br>* Labeled as `tls_cloudlens_free`<br><br>* Free of charge<br><br>* Used for storage lens, storing summary metrics and results from prefix statistics tasks. For field details, see [tos-lens-topic (log topic) field description](https://docs.byteplus.com/docs/tls/Data-pivot-fields#c3adf3bc). |`The name of the bucket in object storage`<br><br><br>* Automatically generated only when prefix aggregation is enabled; each bucket corresponds to one table topic.<br><br>* The tag is `tls_cloudlens`<br><br>* Used for storage lens, storing process data for prefix statistics tasks and raw object\-level data. For field details, see [Object storage bucket name (table topic) field description](https://docs.byteplus.com/docs/tls/Data-pivot-fields#ddacd3a4).<br><br>* It is in closed beta and free of charge for now. The billing start date will be announced separately. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Notice</div>


<div data-tips="true" data-tips-type="default">All storage lens dashboard tasks generate data and share the same set of log topics/table topics:</div>



* <div data-tips="true" data-tips-type="default">Basic summary statistics and prefix statistic task metrics are stored in a single log topic: <code>tos-lens-topic</code>.</div>


* <div data-tips="true" data-tips-type="default">Process data for prefix statistics tasks: stored in table topics named after bucket names. If multiple tasks involve the same bucket, they use the same table topic. Data is stored only once and not duplicated.</div>



<span id="4fe96fce"></span>
## Billing notes

The log application itself does not incur charges, but log topics and related data storage, read traffic, data transformation, and log shipping generated through the log application will incur fees.

If you need to view detailed billing information for a specific project, refer to [split bills](https://docs.byteplus.com/en/docs/byteplus-platform/SplitBills). After enabling the split billing service, you can view detailed split bill data on the split bills page.


|Dimension |Billing notes |
|---|---|
|Log analysis |Log topics are billed by feature.<br><br>Billing items include storage space, data reading, delivering, processing, indexing traffic, API calls, and more. For details, see [Billing items based on pay-by-feature mode](https://docs.byteplus.com/docs/tls/Billing_items_based_on_pay-by-feature_mode). |
|Storage lens |* Log topics are free of charge.<br><br>* The table topic is currently in closed\-beta. During this stage table topic is for free and is expected to charge from October 2026.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Notice</div><br><br><br><div data-tips="true" data-tips-type="default">If you enable the metrics export feature, data will be stored in the target TOS bucket and TOS will charge storage fees. For details, see <a href="https://docs.byteplus.com/en/docs/tos/docs-storage-fee">Storage capacity fees</a>.</div><br> |


<span id="1ac638ef"></span>
## Notice


* Once CloudLens for TOS log application is integrated, it can not be canceled.

* Deleting the `tos-lens-topic` log topic from the pivot dashboard and modifying index configuration are not supported.

* Deleting the `tos-log-topic` log topic in log analysis may cause the TLS feature for cloud products to stop working. If a topic needs to be deleted, ensure related resources under this topic are deleted or disabled before deleting the log topic.

* Do not integrate other data to exclusive log topics.
