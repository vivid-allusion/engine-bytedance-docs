---
title: "Project setting"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/project_setting"
---

Project settings include multiple basic configuration items, such as reporting configuration, JavaScript error aggregation, slow pages, slow loading, slow requests, metric baseline, pageload performance score, and alert acknowledgement. By modifying project parameters, you can obtain monitoring data that is better suited to your business needs.

<span id="5df1d971"></span>
## Prerequisites

If an IAM user needs to perform project settings, the root user must grant the **Administrator** role to them. For details, refer to [Permission management](https://docs.byteplus.com/en/docs/apmplus/Client_permissions_management).

<span id=".5LiK5oql6YWN572u"></span>
## Report configuration

After integrating the SDK into the web service, when reporting data, the SDK not only uses the configuration specified in the integration code but also loads the configuration delivered by the platform. After completing the reporting configuration, updating the SDK's reporting configuration eliminates the need to update the SDK configuration, perform release and go\-live, and go through a series of cumbersome processes.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After the configuration is reported, it will take effect within 5 to 15 minutes after it is saved.</div>


<span id="06462039"></span>
### Configure allowlist customers


1. Log in to the [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client).

2. On the top navigation bar, select the target region.

3. In the left\-side menu, select **Client Monitoring**, click the target application name, and then click **Webpro client monitoring** under the target application.

4. In the upper left corner of the console, select **All features \> project setting**.

5. Under the **Reporting configuration** module, click **Basic configuration**.

6. In the **allowlist customer** text box, enter userId so that the corresponding user can report all types of data and ensure they are included in the allowlist.


<span id="b47efa88"></span>
### Modify SDK reporting configuration


1. Log in to the [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client).

2. On the top navigation bar, select the target region.

3. In the left\-side menu, select **client Monitoring**, then click the target application name, and then click **webpro Monitoring** under the target application.

4. In the upper left corner of the console, select **All features \> Project setting**.

5. Under the **configuration reporting** module, complete the following configuration, then click **Save**.

   Parameter description

   
   |Parameter |DescriptionS |
   |---|---|
   |Type |Report types.<br><br>Includes JavaScript errors, request monitoring, static resource monitoring, static resource error monitoring, custom monitoring, site performance, blank screen monitoring, long tasks, and user behavior. |
   |User sampling rate |The default user sampling rate on the WebPro client, that is, the reporting ratio. Example: 0.3 means that 30% of users turn on reporting.<br><br><br>* The default user sampling rate for JavaScript error is`1`。<br><br>* The default user sampling rate for the request monitor is `0.5`.<br><br>* The default user sampling rate for the resources monitor is `0.5`.<br><br>* The default user sampling rate for static resource error monitoring is`1`。<br><br>* The default user sampling rate for custom monitors is`1`。<br><br>* The default user sampling rate for site performance is`1`。<br><br>* The default user sampling rate for blank screen monitoring is`1`。<br><br>* The default user sampling rate for long tasks is `0.01`.<br><br>* The default user sampling rate for user behavior is `0.01`. |
   |Rule\-based sampling |Supports setting the sampling rate and selecting filter criteria.<br><br><br>* If multiple sampling rules are set at the same time, the rule with the higher priority will be matched first.<br><br>* If a reported data item successfully matches the first rule and is selected for sampling, it will not be evaluated against subsequent rules.<br><br>* If the first rule does not match, the rule with the next priority will be matched. And so on.<br><br>* If all rules fail to match, data will be reported by sampling according to the user's sampling rate configuration. |
   


<span id=".SlPplJnor6_ogZrlkIg="></span>
## JavaScript error aggregation

JavaScript error aggregation aggregates reported JavaScript errors. On the JavaScript overview page, in the JavaScript error list, you can view the reported JavaScript errors. The error count metric is calculated based on the JavaScript error aggregation configuration.


* Supports two integration policies: **aggregate by error message** and **aggregate by error type and stack trace**.

* After updating the JavaScript error aggregation configuration, the JavaScript error list may contain two JavaScript errors with exactly the same error message.

* On the JavaScript overview page, subscribing to newly added JavaScript exceptions is supported. Whether a JavaScript exception is considered newly added is also calculated using the JavaScript error aggregation configuration. Therefore, after updating this configuration, a large number of newly added JavaScript error subscription messages may appear.


<span id=".5oWi6aG16Z2iICYg5oWi5Yqg6L29ICYg5oWi6K-35rGC"></span>
## Slow pages & slow loading & slow requests

This configuration allows you to modify the thresholds for slow pages, slow loading, and slow requests.


* Slow page: When the page load time exceeds the set threshold, the page is considered a slow page.

* Slow loading: When the total time for loading static resources exceeds the configured threshold, the resource is classified as a slow\-loading resource.

* Slow request: When the request time exceeds the threshold specified in the setting, the request is considered a slow request.


<span id=".5oCn6IO95oyH5qCH5Z-65YeG57q_"></span>
## Performance metric baseline

The performance metric baseline can indicate performance compliance in the performance metric chart. All performance metrics of the application are displayed on the **site performance overview \> metric overview** page. In the following example charts, the red dashed line represents the corresponding performance metric baseline. Users can also observe the distribution of metric values over the past seven days during configuration.

Compliance rate = number of PIDs meeting baseline requirements within the filtered time period / total number of PIDs. The sample size threshold does not affect the compliance rate calculation.

<span id="34489514"></span>
## Performance score setting

The performance score configuration provides rules for calculating the overall score of Web services on the platform. You can view the performance score in the daily report, and you can view the pageload performance score in the **performance monitor**. Performance score = sum of (score for each metric × its weight). Pageload performance score = each metric score × its weight.

If a particular metric has a significant negative impact on the performance score and cannot be resolved for the time being, you can raise the threshold for that metric to reduce its influence on the performance score. This will allow you to more clearly view how other metrics affect the application.

For example:


* If the blank screen rate is too high and cannot be fixed for the time being, you can increase the threshold.

* If there are many request errors that cannot be resolved temporarily, you can increase the threshold.

* If the application is highly complex and the request takes a long time, you can increase the request timeout.


<span id=".5oql6K2mQUNL"></span>
## Alert ACK

The alert ACK configuration primarily affects alert ACK Actions and supports configuring the effective duration for each ACK. in **alert task**\>You can perform actions on the **alert detail** page.

Click ACK to enter alert ACK status. ACK only suppresses alert notifications, but alert events are still generated and the rule remains in effect.


* Reset ACK: The default suppression period for a single ACK is 24 hours. Within 24 hours after the user confirms the ACK, the ACK can be reset at any time, and the countdown is refreshed.

* Cancel ACK: Exit the alert ACK status. Alert notification has returned to normal.
