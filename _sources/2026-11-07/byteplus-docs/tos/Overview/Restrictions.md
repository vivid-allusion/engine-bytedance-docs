---
title: "Restrictions"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-restrictions"
---

This topic describes restrictions on using certain features of TOS.

<span id="68a40616"></span>
## Bandwidth

The maximum bandwidth limit for each main account in each region is as follows:


|**Region** |**Total upload bandwidth for internal and external networks** |**Upload bandwidth for external network** |**Total download bandwidth for internal and external networks** |**Download bandwidth for external network** |
|---|---|---|---|---|
|Asia Pacific (Johor) |10Gbps |5Gbps |10Gbps |5Gbps |
|China (Hong Kong) |10Gbps |5Gbps |10Gbps |5Gbps |
|Asia Pacific (Jakarta) |10Gbps |1Gbps |10Gbps |1Gbps |
|China (Beijing) |10Gbps |5Gbps |10Gbps |5Gbps |
|China (Guangzhou) |10Gbps |5Gbps |10Gbps |5Gbps |
|China (Shanghai) |10Gbps |5Gbps |10Gbps |5Gbps |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If the bandwidth reaches this threshold, all requests will trigger flow control. After triggering flow control, requests will be throttled and the response header will include <code>x-tos-qos-delay-time: number</code> (where <code>number</code> represents the duration of flow control for the current request) or respond quickly with status code 429.</div>


* <div data-tips="true" data-tips-type="tip">It is advisable to configure appropriate alert policies based on constraints to avoid impacts on your business operations due to flow control activation. For detailed steps on configuring alert policies, please refer to <a href="https://docs.byteplus.com/docs/tos/Set-metric-alerts">Set Metric Alerts</a>.</div>


* <div data-tips="true" data-tips-type="tip">If your business has greater bandwidth requirements, please <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001170">submit a ticket</a> to contact technical support.</div>



<span id="cfe3299f"></span>
## Performance and storage type


|**Restriction** ||**Description** |
|---|---|---|
|QPS ||* GET requests: 10,000 QPS per account per region by default.<br><br>* PUT requests: 10,000 QPS per account per region by default.<br><br>* ListObjects requests: 1,000 QPS per account per region by default.<br><br><br>If you need a higher performance, submit a ticket for application. |
|Bandwidth ||The maximum bandwidth for upload or download per account per region is 10 Gbit/s. If this limit is exceeded, traffic control will be triggered. If you need a higher bandwidth, submit a ticket for application. |
|Storage type |Infrequent Access Storage |* If a file is smaller than 64 KiB, the occupied storage is regarded as 64 KiB. If it is larger than or equal to 64 KiB, the occupied storage is the actual file size.<br><br>* The minimum storage duration is 30 days. If a file is updated or deleted before the duration ends, fees for the remaining days will still be charged. |
||Flashback Archive |* If a file is smaller than 64 KiB, the occupied storage is regarded as 64 KiB. If it is larger than or equal to 64 KiB, the occupied storage is the actual file size.<br><br>* The minimum storage duration is 90 days. If a file is updated or deleted before the duration ends, fees for the remaining days will still be charged. |
||Intelligent Tiering Storage |* When creating a bucket, you cannot select Intelligent Tiering Storage as the storage type.<br><br>* Files smaller than 64 KiB will be stored at the Frequent Access Layer and will not be transitioned to other layers.<br><br>* Files smaller than 64 KiB are monitored for free. |
||Archive Storage |* You need to restore files before reading them.<br><br>* If a file is smaller than 64 KiB, the occupied storage is regarded as 64 KiB. If it is larger than or equal to 64 KiB, the occupied storage is the actual file size.<br><br>* The minimum storage duration is 90 days. If a file is updated or deleted before the duration ends, fees for the remaining days will still be charged. |
||Cold Archive |* You need to restore files before reading them.<br><br>* If a file is smaller than 64 KiB, the occupied storage is regarded as 64 KiB. If it is larger than or equal to 64 KiB, the occupied storage is the actual file size.<br><br>* The minimum storage duration is 180 days. If a file is updated or deleted before the duration ends, fees for the remaining days will still be charged. |


<span id="97fa48b0"></span>
## Bucket


|**Restriction** |**Description** |
|---|---|
|Bucket |* Each account can create up to 100 buckets.<br><br>* After creating a bucket, you cannot rename it or change its region.<br><br>* For more information on bucket naming conventions, see [Common Concepts](https://docs.byteplus.com/en/tos/docs/common-concepts?version=1.0.0).<br><br>* The number of files and storage capacity of a bucket are not limited. |
|Lifecycle rule |* The number of lifecycle rules for a bucket cannot exceed 1,000, and the total size of JSON descriptions for these rules cannot exceed 20 KB.<br><br>* It takes some time for a modified lifecycle rule to take effect on all objects in a bucket. Specifically, TOS will load the rule within 24 hours after the rule is created. After loading, TOS executes the rule at 2:00 AM (Beijing time) every day. |


<span id="7f41fd4d"></span>
## Object


|**Restriction** ||**Description** |
|---|---|---|
|File upload ||* The maximum size of an object that can be uploaded with a non\-multipart upload is 5 GiB.<br><br>* Use multipart uploads for larger objects. You can upload a single object of up to 48.8 TiB in size, divided into a maximum of 10,000 parts, each of which can be up to 5 GiB.<br><br>* For more information on file naming conventions, see [Common Concepts](https://docs.byteplus.com/en/tos/docs/common-concepts?version=1.0.0). |
|Data processing |Image processing |* The original image can be in the format of JPG, PNG, BMP, GIF, WEBP, or TIFF.<br><br>* The original image can be up to 20 MB.<br><br>* The original image can have up to 30,000 pixels (both width and height) and 250 million pixels in total (the width and height cannot exceed 4,096 pixels for rotation).<br><br>* The resized image can have up to 16,384 pixels (both width and height) and 16,777,216 pixels in total.<br><br>* A bucket supports up to 100 image styles. |
||Video processing |You can process H.264\- and H.265\-encoded video files only. |
