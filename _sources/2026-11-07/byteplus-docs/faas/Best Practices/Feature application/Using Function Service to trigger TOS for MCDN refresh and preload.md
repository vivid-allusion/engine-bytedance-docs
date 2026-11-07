---
title: "Using Function Service to trigger TOS for MCDN refresh and preload"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Using_Function_Service_to_trigger_TOS_for_MCDN_refresh_and_preload"
---

This article introduces how to schedule BytePlus CDN refresh/preload tasks using Function Service (FaaS).

<span id=".5Zy65pmv5LuL57uN"></span>
## Scenario introduction

Refreshing or preloading CDN nodes to ensure consistency between CDN cache and origin content is a common operation for CDN users. Some financial enterprises have strict timing requirements for changes, such as allowing changes only in the early morning daily. In such scenario, manually refreshing and preloading are cumbersome and prone for errors. Scheduling refresh/preload tasks through the FaaS can solve user demands.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information


* **CDN**: BytePlus CDN provides content providers with transmission acceleration services for static content like pictures, audios and videos, web pages, and download packages distributed over the Internet, optimizing user access experience and increasing download speed. For more details, refer to [Overview of BytePlus CDN](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-overview-of-byteplus-cdn).

* **Refresh**: Delete the specified cached content on the CDN nodes or mark it as expired. When users access the node to obtain content next time, the node will pull the latest content from the origin site, and return it to the user and cache it.

* **Preload**: The CDN node actively pulls specific files (usually large files such as video files or installation packages) from the origin site and caches them on the node. Thus when users request the corresponding files, the CDN node can directly return these files. This method reduces the delay caused by nodes obtaining files from the origin site and prevents excessive download pressure on the origin site when many users request large files simultaneously.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Content Delivery Network

   * The CDN is activated.

   * Your site domain has been added as an acceleration domain. For detailed operations, refer to [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

   * The API access keys (AK and SK) have been obtained, and these keys have permissions for CDN cache preloading (SubmitPreloadTask) and cache refreshing (SubmitRefreshTask). For detailed operations, refer to  [API Key Management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-access-keys).

* FaaS

   * The FaaS is activated.

* Torch Log Service (TLS)

   * If you need to use the log feature of the function, activate the BytePlus TLS in advance.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Use restrictions

CDN has quota limits for daily refresh/preload. Exceeding the daily quota may cause task failure on the day of execution. For details, refer to [Purge Quota](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-purge#purge-quota) and [Prefetch Quota](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-prefetch#prefetch-quota).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5L2_55So5Luj56CB5qih5p2_5Yib5bu65Ye95pWw"></span>
### Step One: Create the function using a code template

Create the function using the **vefaas\-golang\-cdn\-refresh\-preload** code template, and configure the AK and SK required by the code as environment variables.


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

2. **Function revision** uses Latest. Fill in **Version description** as needed. Keep **Maximum number of instances** at default settings.

3. Click **OK**, and the function will start releasing. The function is successfully released as shown below.


<span id=".5q2l6aqk5LiJ77ya5Yib5bu65bm25ZCv55So5a6a5pe26Kem5Y-R5Zmo"></span>
### Step Three: Create and enable a scheduled trigger

Configure a Timer Trigger for the current function and set the rules to trigger the function.


1. Switch to the Trigger tab and click **Create trigger**.

2. Configure the trigger information as required.

   * Trigger type: Select Timer trigger.

   * Trigger name: Customize the trigger name according to the interface prompt rules.

   * Push time: Set the trigger cycle and time according to business needs. This example is set to trigger every minute.

   * Enable immediately: Turn on to allow the trigger to work properly.

   * Request concurrency: After turning on, when the specific trigger has not finished the last request, it will not wait until the last request is finished and directly processes the next request in concurrency. This example does not enable it.

   * Trigger message: Pass information such as the task type (refresh/preload) and execution target (URL) to the function through the trigger message.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Each Timer trigger can only specify one task type.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The trigger message must be in JSON object format. Supported fields are listed in the table below:      </div>
      

      
      |field name |Field type |Required or Not |Description |
      |---|---|---|---|
      |TaskKind |string |Yes |Task type. Optional values include:<br><br><br>* refresh: Refresh<br><br>* preload: Preload |
      |TaskType |string |No |Refresh task type, only required when TaskKind = refresh. For more information, refer to [CDN API reference Type field](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-submitrefreshtask).<br><br>Optional values include:<br><br><br>* file (default): File refresh<br><br>* dir: Directory refresh |
      |Urls |string |Yes |Specify one or more content URLs. For more information, refer to [CDN API reference Urls field](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-submitrefreshtask).<br><br><br>* Content URLs start with `http://` or `https://`.<br><br>* Separate multiple content URLs with `\n`.<br><br>* When the specified directory refreshes, end with`/`.<br><br>* Example: `http://example.com/1.txt\nhttp://www.example.com/2.txt` |
      |ConcurrentLimit |int |No |When TaskKind = preload, specify the number of files the CDN requests from the origin site each time it processes a preload task. For more information, refer to the [CDN API reference ConcurrentLimit field](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-submitpreloadtask).<br><br>The default value is 10, with a range of 1 to 1,000. |
      

3. Click **Confirm** to complete the Timer trigger creation.


<span id=".57uT5p6c6aqM6K-B"></span>
## Result validation


1. Go to the **Resource management** tab of the current function. Click **Logs** to view real\-time logs of the function instance. You will see the refresh/preload task was successfully submitted.

2. If the log feature is enabled, go to the **Logs** tab of the current function. Check the execution logs of the current function to see that the refresh/preload task was successfully submitted.

3. Go to the **Refresh and preload** page in the CDN console and switch to the **Operation records** tab to check if the refresh/preload task was executed successfully and if the trigger intervals meet expectations.
