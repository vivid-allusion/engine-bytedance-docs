---
title: "Using Function Service to trigger TOS for CDN refresh and preload"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Using_Function_Service_to_trigger_CDN_refresh_and_preload_from_TOS"
---

The following content introduces how to use the FaaS to trigger CDN refreshing and preloading based on TOS.

<span id=".5Zy65pmv5LuL57uN"></span>
## Scenario introduction

Most internet applications adopt a static\-dynamic separation architecture, which stores static resources such as videos, audio, pictures, and JS scripts in Torch Object Storage (TOS) and uses CDN to accelerate access. When the resources in TOS are updated or upgraded, the content cached on CDN nodes needs be synchronized to ensure visitors always get the latest update.

CDN allows refreshing and preloading cached data manually. However, manual operations are inefficient and error\-prone. The FaaS can help you realize automatic CDN refreshing/preloading when TOS changes, greatly improving maintenance efficiency.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information


* **CDN**: BytePlus CDN provides content providers with transmission acceleration services for static content such as images, audio, video, and webpages, delivering a better user experience. For more information, refer to [Overview of BytePlus CDN](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-overview-of-byteplus-cdn).

* **Refresh**: delete cached content or mark it as expired on the CDN node. When visitors request that content on the node afterward, the node will pull the latest content from the original sites, return it to visitors, and save a copy as well.

* **Preload**: CDN nodes actively pull specific files (usually large files such as videos or installation packages) from the original site and cache them on the nodes. By doing that, the nodes can instantly start file transmission to visitors on receipt of requests. This reduces the delay caused by nodes fetching files from the original sites and avoids excessive download pressure on those sites when too many download requests for large files come in simultaneously.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Content delivery network

   * Permission for using BytePlus CDN has been obtained.

   * The site domains that need acceleration have been added and bound to your TOS bucket (i.e., using the TOS Bucket as the original sites). For details, refer to [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

   * The API access keys (AK and SK) are ready with permissions for CDN cache preloading (SubmitPreloadTask) and cache refreshing (SubmitRefreshTask). For details, refer to  [API Key Management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-access-keys).

* FaaS

   * Permission for using FaaS has been obtained.

* Torch Log Service

   * To use the logging feature, you need to apply for permission in advance to use BytePlus Log Service.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit


* Preloading and refreshing are only applicable to files, not directories currently.

* A function can either perform preloading or refreshing, but not both simultaneously.

* CDN has a daily refreshing/preloading quota limit. Tasks cannot be performed if the quota has run out. For details, refer to [Purge Quota](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-purge#purge-quota) and [Prefetch Quota](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-prefetch#prefetch-quota).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5L2_55So5Luj56CB5qih5p2_5Yib5bu65Ye95pWw"></span>
### Step 1: create a function using a code template

Use **vefaas\-golang\-cdn\-refresh\-preload** code template to create a function and the required AK and SK to set environment variables.


1. Log in to [Function Service Console](https://console.byteplus.com/vefaas).

2. In the top bar, select the target region.

3. On the Function page, click **Create function**.

4. The key options on the page and their descriptions are shown below. For other options, see [Create Event function](https://docs.byteplus.com/en/docs/faas/Creating_event_functions).

   
   |Parameter |Description |
   |---|---|
   |Function type |Select **Create [Event function]** . |
   |**Basic configuration** ||
   |Name |Enter a function name according to the prompts on the page. Function names cannot be changed after created. |
   |**Function code** ||
   |Runtime |Select **Golang**. |
   |Deployment method |Select **Function template** \> **vefaas\-golang\-cdn\-refresh\-preload**. |
   |**Advanced configuration** ||
   |Logging |Enable logging to save logs. |
   |Environment variables |You need to set following 4 environment variables:<br><br><br>* `CloudAPI_AccessKey`: enter the ID of API secret access key.<br><br>* `CloudAPI_SecretKey`: enter the API secret access key.<br><br>* `TOS_EVENT_TASK_KIND`: enter the type of task to execute. Available types:<br><br>   * `refresh`: (default) file refreshing.<br><br>   * `preload`: file preloading.<br><br>* `BASE_URL_LIST`: enter the URL for which the task is about to execute, e.g., `http://cdndomain1/,http://cdndomain2/,http://cdndomain3/`. Multiple URLs can be added with commas as separators. When the TOS event triggers the function, each URL in the list will be appended with a TOS file name and then passed on to CDN for refreshing/preloading. |
   

5. Click **Create** to create the function.


<span id=".5q2l6aqk5LqM77ya5Y-R5biD5Ye95pWw"></span>
### Step 2: release the function

Release code and configurations online for the function.


1. On the function details page, click **Release** in the upper right corner.

2. Select **Latest** as the **function version**. Other options can be configured as required.

3. Click **OK** and wait until the function release is finished. The function is successfully released if you see the following information on the page.


<span id=".5q2l6aqk5LiJ77ya6YWN572uIFRPUyDop6blj5Hlmag="></span>
### Step 3: Configure the TOS trigger

Configure the rules of TOS trigger for the function.


1. Switch to the Trigger tab and click **Create trigger**.

2. Configure the trigger as required. For details, see [Creating TOS triggers](https://docs.byteplus.com/en/docs/faas/Creating_a_TOS_trigger).

   
   |Parameter |Description |
   |---|---|
   |Trigger type |Select Torch Object Storage. |
   |Trigger name |Enter a trigger name according to prompts on the page. |
   |TOS Bucket |Select the TOS Bucket you created according to the prerequisites above. |
   |Trigger event |Select **tos:ObjectCreated:Put** and **tos:ObjectCreated:CompleteUpload** in this example.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The options <strong>tos:ObjectCreated:Put</strong> and <strong>tos:ObjectCreated:CompleteUpload</strong> need to be selected if you about to upload a large file through multipart requests. Otherwise, you can just select <strong>tos:ObjectCreated:Put</strong>, which triggers the function after a simple object is uploaded.</div><br> |
   |Filter conditions |Filter conditions can confine the events that you need to listen for by accurately matching the specified objects,  effectively reducing trigger frequency and cost. It is left empty in this example. |
   

3. Click **Create** to start creating API Gateway Trigger.


<span id=".57uT5p6c6aqM6K-B"></span>
## **Result validation**


* **Console validation**

   1. On the trigger tab, select the TOS trigger you just created, click the Bucket name to open the corresponding Bucket page. Click **Upload file** to upload a file from your local device.

   2. On the configuration page of the function, click Resource management tab. Click **Logging** to view the real\-time log. You can find messages in the log indicating the refreshing/preloading task has been successfully submitted as shown in the screenshot below.

   3. If logging is enabled for the function, you can go to the **Logging** tab. On this tab, the same messages can be found as evidence of success.

   4. Go to the CDN console and click **Refresh & Preheat** in the left navigation bar, then select **Operation Log** tab on the page. The information shown in the following screenshot indicates the refreshing/preloading tasks have been performed successfully.

* **Business validation**

   * Send GET requests to a URL which has been refreshed. The first request will get a response from the TOS of the original site, but the subsequent requests will get from the CDN cache.

   * Send GET requests to a URL which has been preloaded. The first request will get a response from the CDN cache.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can determine whether the CDN cache is hit by the <code>X-Bdcdn-Cache-Status</code> field in the response header.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>X-Bdcdn-Cache-Status: TCP_HIT</code> indicates a hit.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>X-Bdcdn-Cache-Status: TCP_MISS</code> indicates a miss.   </div>
