---
title: "Project setting"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/project_setting_minipro"
---

Project settings consolidate multiple basic configurations, including reporting configuration, JavaScript error aggregation, slow pages, slow start, slow requests, performance metric baseline, performance score, and alert ACK. By modifying project parameters, you can obtain monitoring data that is better suited to your business needs.

<span id=".5LiK5oql6YWN572u"></span>
## Reporting configuration

After the mini program integrates the SDK, the SDK uses both the configuration set in the integration code and the configuration delivered by the platform when reporting data. After completing the reporting configuration, updating the SDK's reporting configuration eliminates the need to update the SDK configuration, release the update online, and perform a series of other cumbersome steps.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After the configuration is reported, it will take effect within 5 to 15 minutes after saving the configuration.</div>


<span id="e7ab47b0"></span>
### Modify the SDK setting


1. Log in to the [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client).

2. On the top navigation bar, select the target region.

3. In the left\-side menu, select **Client Monitoring**, then click the target application name, and then click **Mini Program Pro Monitoring** under the target application.

4. In the upper left corner of the console, select **All features \> Project setting**.

5. Under the **reporting configuration** module, complete the following configuration, and then click **Save**.

   Parameter description

   
   |**Parameter** |**DescriptionS** |
   |---|---|
   |Type |The report type.<br><br>Includes basic configuration, JavaScript error, request monitor, custom monitor, performance monitor, and setData. |
   |User sampling rate |The default user sampling rate for Mini Pro Monitoring, that is, the reporting ratio. For example, 0.3 means that 30% of users turn on reporting.<br><br><br>* The default user sampling rate for JavaScript errors is`1`。<br><br>* The default user sampling rate for the request monitor is`1`。<br><br>* Default user sampling rate for custom monitor is`1`。<br><br>* The default user sampling rate for the performance monitor is`1`。<br><br>* The default user sampling rate for setData is `0.01`. |
   |Rule\-based sampling |Supports setting the sampling rate and selecting filter criteria.<br><br><br>* If multiple sampling rules are set at the same time, the rule with the higher priority will be matched first.<br><br>* If a reported data entry successfully matches the first rule and is selected for sampling, it will not be evaluated against the next rule.<br><br>* If the first rule fails to match, the next rule in order of priority will be matched. And so on.<br><br>* If all rules fail to match and sampling cannot be triggered, reporting cannot occur. |
   


<span id="78955ead"></span>
### Configuration of allowlist customers


1. Log in to the [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client).

2. On the top navigation bar, select the target region.

3. In the left\-side menu, select **Client Monitoring**. Next, click the target application name. Then, under the target application, click **Mini Program Pro Monitoring**.

4. In the upper left corner of the console, select **All features \> Project setting**.

5. Under the **Reporting configuration** module, click **Basic configuration**.

6. In the **allowlist user** text box, enter the userId. The corresponding user will be able to report all types of data, ensuring they are included in the allowlist.


<span id=".5oWi6aG16Z2iJuaFouWQr-WKqCbmhaLor7fmsYI="></span>
## Slow pages & slow start & slow request

The configuration allows you to modify the thresholds for slow pages, slow loading, and slow requests.


* Slow page: When the total page navigation time exceeds the threshold specified in the settings, the page is classified as a slow page.

* Slow start: When the total load time for the first screen exceeds the set threshold, it is considered a slow start.

* Slow request: A request is considered a slow request when its request time exceeds the threshold specified in the setting.


<span id=".5oCn6IO95oyH5qCH5Z-65YeG57q_"></span>
## Performance metric baseline

The performance analysis baseline can reflect performance compliance in the performance metric chart.


* On the **performance monitor** page, all application performance metrics are displayed. In the chart, the red dashed line represents the corresponding metric baseline.

* Users can also observe the distribution of metric values for the past seven days during the configuration process, and can also observe this in the **performance monitor**.\-**Start time distribution** and **performance monitoring**\-View the distribution of metric values on the **Page load time distribution** page.


<span id=".6KGo546w5YiG6K6-572u"></span>
## Performance score setting

The performance score configuration defines the rules used by the platform to calculate the overall score for mini programs. You can view the performance score in the daily report, and you can view the pageload performance score in the **performance monitor**. Performance score = sum of (score for each metric × its weight). Pageload performance score = the sum of each metric's score multiplied by its weight.

If a particular metric has a significant negative impact on the performance score and cannot be resolved for the time being, you can increase the threshold for that metric to reduce its influence on the performance score. This allows you to more clearly view how other metrics affect the application.

For example:


* If the JavaScript error rate is too high and cannot be fixed for now, you can increase the threshold.

* If there are many request errors and they cannot be fixed for now, you can increase the threshold.

* If the application is highly complex and requests take a long time, you can increase the allowed request time.


<span id=".5oql6K2mQUNL"></span>
## Alert ACK

The alert ACK configuration primarily affects alert ACK Actions and supports configuring the effective duration for each ACK. In the Actions column under **alert management**, you can perform actions on alert details.

Click ACK to enter alert ACK status. ACK only suppresses alert notifications; however, alert events are still generated, and the rule remains in effect.


* Reset ACK: The default blocking duration for a single ACK is 24 hours. Within the 24\-hour period after the user confirms the ACK, the ACK can be reset at any time, and the countdown will restart.

* Cancel ACK: Exit the alert ACK status. Alert notification has returned to normal.
