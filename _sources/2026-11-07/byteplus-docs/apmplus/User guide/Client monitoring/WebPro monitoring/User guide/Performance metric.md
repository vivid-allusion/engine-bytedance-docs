---
title: "Performance metric"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/performance_metric"
---

After registering a performance metric on the performance metric management page, you can view the compliance rate of the performance metric, as well as detailed information such as the performance metric trend chart, distribution, and Bounce Rate, on the site performance overview page.

<span id=".5pON5L2c5q2l6aqk"></span>
## Operation Procedure


1. Log in to the [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client).

2. Click **Webpro Monitoring** under the target application.

3. In the upper left corner of the console, select **All features \> performance metric**.

4. On the **performance metric management** page, click **Register performance metric**.

5. In the **register performance metric** dialog box, complete the following configuration, and then click **confirm**.

   Parameter descriptions are as shown in the following table:

   
   |**Parameter** |**DescriptionS** |
   |---|---|
   |key |Key for custom reporting. Only lowercase letters are supported. |
   |Name |A custom performance metric name is used to identify the performance metric. |
   |Description |Enter the meaning of the current metric. |
   |Baseline |Customize the good and bad baselines. |
   |Calculate bounce rate |If actions such as page unload are triggered before instantaneous metrics occur, these metrics are considered a bounce and should be included in the Bounce Rate calculation.<br><br><br>* Turn off: bounce rate is not calculated<br><br>* Enable bounce rate |
   |Display time units |The unified time unit for performance metrics is ms. For performance metrics that do not measure time, the time unit may be omitted.<br><br><br>* Turn off time units<br><br>* Show time units |
