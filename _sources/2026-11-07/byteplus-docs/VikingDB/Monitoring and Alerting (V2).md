---
title: "Monitoring and Alerting (V2)"
product: "Vector Database Cloud"
product_code: "VikingDB"
section: "Document"
source: "https://docs.byteplus.com/en/docs/VikingDB/monitor"
---

To proactively manage the health and performance of your VikingDB Vector Database, you can use the integrated BytePlus Cloud Monitor. This guide shows you how to access monitoring dashboards directly from the console, grant the required permissions, and view key metrics for collections, indexes, and resources. You will learn to track performance indicators like QPS and latency, monitor resource usage, and configure alerts to stay informed of your database's status.


* If you need SMS or voice notifications from the alert center and event center, refer to Cloud Monitor documentation to [enable pay-as-you-go billing](https://www.volcengine.com/docs/6408/192702?lang=en).

* When you create alert contacts, you can configure notification delivery channels such as email, phone call, or SMS. After creation, Cloud Monitor will send a verification message to the email address or mobile number you set. After receiving the verification message, you must click the link in the message within 24 hours to complete verification. Otherwise, you will not be able to receive alert or event notifications. For details, refer to [Create alert contacts](https://www.volcengine.com/docs/6408/69466?lang=en).

* For an introduction to monitoring metrics for the vector database, refer to [Vector database monitoring metrics](https://console.volcengine.com/cloud_monitor/docs?namespace=VCM_VikingDB).


<span id="region-availability"></span>
# Region availability


|**Region** |**Cloud Monitor** |
|---|---|
|North China |Supported |
|East China |Supported |
|South China |Supported |
|Johor |Supported |


<span id="prerequisites"></span>
# Prerequisites

Complete Volcano Engine real\-name verification. For details, refer to [Real-name verification](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

<span id="access-authorization"></span>
# Access authorization

After entering the console, select the monitoring product data you want to view in the left navigation pane.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f43337aa186947418351536d47f95a1e~tplv-goo7wpa0wc-image.image) </span>

If the redirected page indicates that the sub\-account has not configured a Cloud Monitor access policy, it means the sub\-account does not have Cloud Monitor access permissions. You can configure the policy as follows.


1. Log in to the [Volcano Engine console](https://console.byteplus.com/home) with the primary account or a user that has **Access Control** permissions. Scroll down and find [Access Control](https://console.byteplus.com/iam/policymanage?search=cloud+monitor) to enter the corresponding page.

2. In the left navigation pane, select **Permission Policies** to open the policy management page. Search for **Cloud Monitor** in the search box to find Cloud Monitor permission policies.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fda064ed17b9433b9549ab150e26f37a~tplv-goo7wpa0wc-image.image) </span>


3. Select the **CloudMonitorFullAccess** policy and click **Add Permissions**. Under **Authorized Identities**, choose a sub\-user or user group to grant permissions to, then submit.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23b3ec98323349409fe3a2450b97039c~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/520a1edda4e54886bcc12b3a7b0f6148~tplv-goo7wpa0wc-image.image) </span>

After the permissions are granted, you can enter Cloud Monitor to view and manage monitoring and alerts for the vector database.

<span id="procedure"></span>
# Procedure


1. In the [console](https://console.byteplus.com/vikingdb/region:vikingdb+ap-southeast-1/bohr/start), **Viking Vector Database** provides three monitoring entries. Click an entry to open the monitoring product details page.

   1. The entries are:

      1. Collection monitoring

      2. Index monitoring

      3. Resource monitoring

   2. After you enter the monitoring product details page, you can click the title to switch between monitoring items.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/34f4b0f8d2fb4734818a1d56d0fba2ad~tplv-goo7wpa0wc-image.image) </span>


2. Viking Vector Database \- Collections

   1. On the **Collection management monitoring** page, you can view **Create collection, Delete collection, Update collection, Get collection, List collections** within the selected time range, as well as QPS, latency, and error rate metrics for control plane operations. You can also create and view alert policies.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/94a4924aeedf408eab13c704c363e0f0~tplv-goo7wpa0wc-image.image) </span>


2. On the **Data management monitoring** page, you can select a specific collection to view **Data write, Data update, Data delete, Data fetch** within the selected time range, as well as QPS, latency, error rate metrics for control plane operations, total synchronous/asynchronous write entries, and total write volume. You can also create and view alert policies. The list displays alert name, project, status, alert severity, notification method, and enabled status.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a5a3b05f2b746628131db62e17e9251~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cbec452c38b64fc5b0ba156bc68e8810~tplv-goo7wpa0wc-image.image) </span>


3. Viking Vector Database \- Indexes

   1. On the **Index management monitoring** page, you can view **Create index, Delete index, Update index, Get index, List indexes** within the selected time range, as well as QPS, latency, and error rate metrics for control plane operations. You can also create alert policies.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1b76292498674baca8969237403c7279~tplv-goo7wpa0wc-image.image) </span>


2. On the **Search and resource monitoring** page, you can select a specific index to view QPS, latency, and error rate metrics for each search operation within the selected time range, including **Vector search, Multimodal search, ID search, Scalar sort search, Random search, Keyword search, Aggregate statistics, Fetch data in index**. On the **Resources** tab, you can view CPU usage and memory usage for the index. You can also create and view alert policies. The list displays alert name, project, status, alert severity, notification method, and enabled status.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b3becc5f04649c2844245e9b76feb44~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a3a22446a20b4a3cb39bb2625c7704c5~tplv-goo7wpa0wc-image.image) </span>


4. Viking Vector Database \- Resources

   1. On the **Viking Vector Database \- Resources** page, you can view instance details (instance name, instance status, deployment region). Click the instance name to enter the instance monitoring and alert policy page.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06dddea9ed0140ad9892e2ccebabb858~tplv-goo7wpa0wc-image.image) </span>


2. On the **Monitoring** tab, you can select a vectorization model to view token usage for different modalities within the selected time range. On the **Resources** tab, you can view instance bandwidth. You can also click **Alert Policies** to create and view policies. The list displays alert name, project, status, alert severity, notification method, and enabled status.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/13c4325146f44de4920eb961e0ec1039~tplv-goo7wpa0wc-image.image) </span>


5. For more features of Cloud Monitor, refer to the [Cloud Monitor documentation](https://www.volcengine.com/docs/6408/68109?lang=en).
