---
title: "Using Function Service to trigger CDN refresh/preload at a scheduled time"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Using_Function_Service_to_trigger_CDN_refresh_and_preload_at_a_scheduled_time"
---

This article introduces how to trigger CDN refresh/preload tasks at a scheduled time using Function Service (FaaS).

<span id=".5Zy65pmv5LuL57uN"></span>
## Scenario introduction

Refreshing or preloading CDN nodes to ensure the consistency between CDN cache and origin server content is a common operation for CDN users. Some financial enterprises have strict requirements for change timing, such as allowing changes only during early morning hours daily. In such cases, manually refreshing and preloading is cumbersome and error\-prone. Scheduling refresh/preload tasks using FaaS effectively addresses user needs.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information


* **CDN**: BytePlus CDN provides content providers with accelerated delivery services for static content such as images, audio and video, webpages, and download packages distributed over the Internet, optimizing user experience and increasing download speeds. For more information, refer to [Overview of BytePlus CDN](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-overview-of-byteplus-cdn).

* **Refreshing**: Deleting specified cached content or marking it as expired on CDN nodes. When users obtain the content from accessing the nodes the next time, the node will pull the latest content from the origin server and return it to users to cache it.

* **Preloading**: CDN nodes actively pull specific files (usually large files such as video files or installation packages) from the origin server, and cache them on the nodes. This allows CDN nodes to return files directly when users request the corresponding files. This method reduces the latency caused by the nodes obtaining files from the origin server, and prevents excessive download pressure on the origin server when users request large files simultaneously.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* BytePlus CDN

   * The CDN is activated.

   * Your site domain has been added as an acceleration domain. For detailed operations, refer to [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

   * You have obtained the API access keys (AK and SK) and ensured these keys have permissions for CDN cache preloading (SubmitPreloadTask) and cache refreshing (SubmitRefreshTask). For specific operations, refer to  [API Key Management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-access-keys).

* Function Service

   * FaaS has been activated.

* Torch Log Service (TLS)

   * To use the log feature of the function, activate the BytePlus TLS in advance.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Use restrictions

CDN has daily quotas for refresh/preload. If refresh/preload exceeds the daily quota on the day of execution, it might cause the task failure. For details, refer to [Purge Quota](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-purge#purge-quota) and [Prefetch Quota](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-prefetch#prefetch-quota).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5L2_55So5Luj56CB5qih5p2_5Yib5bu65Ye95pWw"></span>
### Step One: Create a function using the code template

Use the code template **vefaas\-golang\-cdn\-refresh\-preload** to create a function, and configure the AK and SK required as environment variables.


1. Log in to the [Function Service Console](https://console.byteplus.com/vefaas).

2. On the top navigation bar, select the target region.

3. On the function list page, click **Create function**.

4. On the Create function page, the major parameters are configured according to the following instructions, and the other parameters are configured as needed according to [Creating Event function](https://docs.byteplus.com/en/docs/faas/Creating_event_functions).

   
   |Parameter |Description |
   |---|---|
   |Function creation method |Select **Create [Event function]** . |
   |**Basic configuration** ||
   |Name |Customize the function name according to the naming rules prompted by the interface. After successfully creating the function, the name cannot be changed. |
   |**Function code** ||
   |Runtime |Select **Golang**. |
   |Deployment method |Select **Function template** \> **vefaas\-golang\-cdn\-refresh\-preload**. |
   |**Advanced settings** ||
   |Logging |Enable the log feature, and specify the default log set. |
   |Environment variables |Add two new environment variables and configure the AK and SK prepared in the Prerequisites as environment variables. Configuration format:<br><br><br>* `CloudAPI_AccessKey:xxx`<br><br>* `CloudAPI_SecretKey:xxx` |
   

5. Click **Create** to complete creating the function.


<span id=".5q2l6aqk5LqM77ya5Y-R5biD5Ye95pWw"></span>
### Step Two: Release the function

Release the current code and configuration of the function online.


1. On the function details page, click **Release** in the upper\-right corner.

2. Use Latest for the **function revision**. Fill in the **revision description** as needed, and keep the **maximum instance number** at default.

3. Click **confirm,**  and the function will be releasing. Successful function release is shown in the figure below.


<span id=".5q2l6aqk5LiJ77ya5Yib5bu65bm25ZCv55So5a6a5pe26Kem5Y-R5Zmo"></span>
### Step Three: Create and enable a scheduled Trigger

Configure a Timer Trigger for the current function and set the rules for triggering the function.


1. Switch to the Trigger tab and click **Create Trigger**.

2. Configure the Trigger information as required.

   * Trigger type: Select Timer Trigger.

   * Trigger name: Customize the Trigger name according to the rules prompted by the interface.

   * Push time: Set the Trigger cycle and time according to business needs. This example is set to trigger every minute.

   * Enable now: After enabling, the Trigger can work properly.

   * Request concurrency: After turning on, when the specific Trigger has not finished the last request, it will not wait until the last request is finished and directly processes the next request in concurrency. This example does not enable request concurrency.

   * Trigger message: Pass on the task type (refresh/preload) to be executed and execution object (URL) and other information to the function through trigger message.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Each scheduled Trigger can specify only one task type.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The trigger message must be in json object format. See the table below for supported fields.      </div>
      

      
      |Field name |Field type |Required or Not |Description |
      |---|---|---|---|
      |TaskKind |string |Yes |Task type. Optional values include:<br><br><br>* refresh: Refresh<br><br>* preload: Preload |
      |TaskType |string |No |This is the refresh task type. Only fill in when TaskKind = refresh. For more information, refer to [CDN API reference Type field](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-submitrefreshtask).<br><br>Optional values include:<br><br><br>* file (default): File refresh<br><br>* dir: Directory refresh |
      |Urls |string |Yes |Specify one or more content URLs. For more information, refer to [CDN API reference Urls field](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-submitrefreshtask).<br><br><br>* Content URLs start with `http://` or `https://`.<br><br>* Multiple content URLs are separated by `\n`.<br><br>* When a specific directory refreshes, it must end with`/`/.<br><br>* Example: `http://example.com/1.txt``\n``http://www.example.com/2.txt` |
      |ConcurrentLimit |int |No |This indicates, when TaskKind = preload, the number of files requesting the origin server each time when the specified CDN is processing preload tasks. For more information, refer to [CDN API reference ConcurrentLimit field](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-submitpreloadtask).<br><br>The default value is 10, with a value range of 1\-1,000. |
      

3. Click **Confirm**, to complete creating the Timer Trigger.


<span id=".57uT5p6c6aqM6K-B"></span>
## Result validation


1. Enter the **Resource management** tab of the current function. Click **Logs** to view the real\-time logs of the function instance and see that the refresh/preload tasks have been successfully submitted.

2. If you want to enable the log feature, enter the **Logs** tab of the current function. Query the execution logs of the current function to see that the refresh/preload tasks have been successfully submitted.

3. Go to the **Refresh and Preload** page of the CDN console, and switch to the ** Operation Records** tab, thus you can check whether the refresh/preload tasks have been successfully executed, and if the trigger time interval meets the expectation.
