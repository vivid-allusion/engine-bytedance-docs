---
title: "Platform setting"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Platform_setting"
---

This document introduces the parameters that can be configured in the platform parameter configuration.

<span id=".5o6l5pS257uE566h55CG"></span>
## receiver group management

Configure members by group to allow members to receive schedule report subscriptions, dashboard subscriptions, and alerts.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Make sure you have already marked the email address of the APMPlus client as trusted; otherwise, subscription, schedule report, or alert emails may be blocked or sent to the spam folder.</div>



* <div data-tips="true" data-tips-type="warning">Domestic email address: apmplus@cnmail.apmplus.volces.com</div>


* <div data-tips="true" data-tips-type="warning">Overseas email address: apmplus@rfmail.apmplus.volces.com</div>


1. On the **receiver group management** page, click **create receiver group**.

2. In the **Create receive group** dialog box, after completing the configuration, click **Confirm**.

   Configuration description:

   
   |**Parameter** |**DescriptionS** |
   |---|---|
   |Name |Customize the name of this receiving group. This name is used to identify this receiving group. |
   |Email |Enter the email address that will receive subscriptions. |
   

3. Verify email

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the receiving group is created, email verification is required. Only verified email addresses can properly receive messages from APMPlus.   </div>
   

   1. Click **Verify** after the recipient group mailbox. The platform will send a verification email to this email address. Please check your email to complete the verification.

   2. View the email content in your mailbox, then verify it yourself.


<span id=".5qCH562-566h55CG"></span>
## tag management

Custom tags can be configured in key\-value format. Configured tags can be applied to issues for filtering and categorizing.


1. On the **tag management** page, click **create module**.

2. In the **create module** dialog box, after completing the configuration, click **confirm**.

   Configuration description:

   
   |**Parameter** |**DescriptionS** |
   |---|---|
   |Module name |A custom module name is used to identify the module. |
   |Tag name |Custom tag name for filtering and categorizing issues. |
   


<span id=".U0RL5LiK5oql6YWN572u"></span>
## SDK setting

Switches and the sampling rates of each field can be configured by feature module, enabling on\-demand Monitoring to help save and control customer costs. For details, refer to [SDK setting](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration).

<span id=".5bmz5Y-w5Y-C5pWw6YWN572u"></span>
## platform parameter configuration

Used for setting parameters and thresholds, with default values preset, and can be specifically adjusted according to the actual business situation.


|**Configuration module** |**Parameter** |**Default value** |
|---|---|---|
|crash analytic |Crash alert ACK time |24 hours |
||Crash protection alert ACK time |24 hours |
|error analytic |Error alert ACK time |24 hours |
|lag analytic |The lag alert ACK time |24 hours |
|event analytic |Event alert ACK time |24 hours |
|traffic monitor |Traffic monitor alert ACK time |24 hours |
|disk monitor |Disk monitor alert ACK time |24 hours |
|battery analytic |Battery alert ACK time |24 hours |
|CPU monitor |CPU monitor alert acknowledgment time |24 hours |
|startup analytic |Slow start threshold |3 milliseconds |
||Do you want to set a maximum startup time? |Yes |
|page experience |Slow page threshold |100,000 milliseconds |
|Request error |Slow query threshold |3000 milliseconds |
|Monitoring pages |Page monitoring alert ACK time |24 hours |
|Slow pages |Slow page threshold |6000 milliseconds |
|Slow request |Slow request threshold |3000 milliseconds |
|Performance metric baseline |FP |Less than 1000 milliseconds is considered excellent.<br><br>Greater than 2500 milliseconds is considered poor. |
||FCP |Less than 2000 milliseconds is considered excellent.<br><br>Greater than 4000 milliseconds is considered poor. |
||LCP |Less than 2500 milliseconds is considered excellent.<br><br>Durations greater than 4000 milliseconds are considered poor. |
||TTI |Less than 3800 milliseconds is considered excellent<br><br>Values greater than 7300 milliseconds are considered poor. |
||INP |Less than 200 milliseconds is considered excellent.<br><br>Greater than 500 milliseconds is considered poor. |
||CLS |Less than 0.1 milliseconds is considered excellent<br><br>Greater than 0.25 milliseconds is considered poor. |
||FMP |Less than 2000 milliseconds is considered excellent.<br><br>Greater than 4000 milliseconds is considered poor. |
||LOAD |Less than 2000 milliseconds is considered excellent.<br><br>Greater than 4000 milliseconds is considered poor. |
|Alert ACK |Effective duration of alert ACK |24 hours |
|memory optimization |A single large object definition |Greater than or equal to 1000 KB |
||Definition of class large objects |The number of items is greater than or equal to 50, and the total memory usage is greater than or equal to 10,000 KB. |
|network analytic |Slow request threshold |2000 milliseconds |
||Whether to set a time limit for network requests |No |
||Request time limit value |6000 milliseconds |
|MetricKit |MetricKit alert ACK time |24 hours |


<span id=".572R57uc6K-35rGC6K6-572u"></span>
## request setting


* List of own service domain names

   Domain names other than those belonging to the service itself will be identified as third\-party services. If no setting is specified, the default is a third\-party service.

* Setting the collection scope for domain name data in network Monitoring

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Request filtering only supports configuring one of the collection modes.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The network sampling rate in the SDK setting is a prerequisite; data collection based on the request filtering configuration will only occur when a device matches the sampling criteria.   </div>
   

   * Full collection:

      * If you select full collection, all URLs are collected.

   * Allowlist:

      * The collection policy first performs string matching on the URL. If the string matching does not succeed, regular expression matching is performed. If a match is found, the URL is collected.

      * Only URLs under domains or IPs in the allowlist will be collected; other URLs will not be collected.

      * You can add multiple domain names or IP addresses, but please add only one at a time.

   * Blocklist:

      * The collection policy first performs string matching on the URL. If string matching does not succeed, regular expression matching is performed. If neither match is successful, the URL will be collected.

      * URLs under domains or IPs in the blocklist will not be collected; all other URLs will be collected.

      * Please add one domain name or IP address at a time. All URLs under that domain or IP will be excluded from collection.
