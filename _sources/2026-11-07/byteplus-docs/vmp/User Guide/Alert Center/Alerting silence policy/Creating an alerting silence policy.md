---
title: "Creating an alerting silence policy"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/create-alerting-silence-rule"
---

The alert silence policy is used to silence specified alerts. When some alerts cannot be resolved, you can configure an alert silence policy to silence the notifications of the corresponding alerts. This topic describes how to configure an alert silence policy.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The new Alert Center is available. It provides comprehensive upgrades and optimizations for features such as notification policies, notification templates, aggregation policies, and suppression policies. We recommend configuring suppression policies in the new <a href="https://console.byteplus.com/observe/alert/silence">Alert Center</a>.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

VMP has been activated.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

Up to 1,000 alert silence rules can be created within a root user and its Identity and Access Management (IAM) users.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5omL5Yqo6YWN572u"></span>
### Manual configuration


1. Log in to [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target region.

3. On the left navigation bar, click **Alert center \> Alerting silence policy**. On the page that appears, click **Create silence policy** and configure the policy.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_555c5395fcb48683f2e5c012a03df6d4.png) </span>


|Parameter |Descriptions |
|---|---|
|Policy Name |Specify the name of the alert silence policy.<br><br><br>* It is a string and can contain Chinese characters, uppercase and lowercase letters, digits, underscores (`_`), and hyphens (`-`).<br><br>* It cannot start with a digit, underscore (`_`), hyphen (`-`), or any other special character.<br><br>* It must be 1 to 128 characters in length. |
|Description |Specify the description of the alert silence policy. The description must be 1 to 128 characters in length. |
|Silence machers |Use the labels included in the alerts to match the alerts that you want to silence. Example: `job:kubernetes-etcd`. You can configure multiple label groups. Each label group can contain multiple labels.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The logical <strong>OR</strong> relationship applies between label groups. The logical <strong>AND</strong> relationship applies between labels within a label group.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">In addition to the labels in alert events, the <code>__alerting_rule_id</code> label (alert rule ID) is also supported. You can use this label to search for the target alert rule.</div><br> |
|Silence time |Configure the effective time period of the alert silence policy. Valid values:<br><br><br>* **Always**: The alert silence policy always takes effect.<br><br>* **Periodic**: The alert silence policy only takes effect within a specified time period on each day. Click **Start time** and **End time** to specify the effective time periods of the alert silence policy on each day. You can specify up to 3 time periods.<br><br>* **Custom**: The alert silence policy takes effect during the specified time periods on specified dates. Click **Start date** and **End date** to specify the effective time periods of the alert silence policy. You can configure up to 3 time periods. |



4. Click **Create** to complete the configuration.


<span id=".6YCa6L-H5ZGK6K2m6YCa55-l6YWN572u"></span>
### Configuration through alert notification

When you receive alert notifications in Feishu, you can create an alert silence rule by using the notifications.


1. When you receive a Feishu alert notification, click the silence button at the bottom of the notification.

2. Then, you are redirected to the VMP console. The system automatically creates a silence policy and fills in the parameters.

3. You need to modify the **Silence matchers** and **Silence time** parameters based on your business requirements. Then, click **OK** to complete the configuration.
