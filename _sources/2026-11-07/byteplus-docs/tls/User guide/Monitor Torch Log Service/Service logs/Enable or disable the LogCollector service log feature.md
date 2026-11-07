---
title: "Enable or disable the LogCollector service log feature"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/enable_or_disable_the_service_log_feature"
---

For LogCollector, you can enable or disable the service log feature as needed. For other features, the service log feature is enabled by default and cannot be manually enabled or disabled. This topic describes how to enable or disable the service log feature for LogCollector.

<span id=".5byA5ZCvLWxvZ2NvbGxlY3Rvci3mnI3liqHml6Xlv5c="></span>
## Enable the service log feature for LogCollector

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Only LogCollector 1.0.9 and later support the service log feature. For other earlier versions, refer to <a href="https://docs.byteplus.com/docs/tls/upgrade_logcollector_on_a_host">Upgrade LogCollector on a host</a> to upgrade LogCollector, then manually enable the service log feature.</div>


* <div data-tips="true" data-tips-type="tip">Torch Log Service (TLS) only records service logs generated after LogCollector is enabled.</div>



To enable the service log feature:


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Resource management** \> **Host group**.

3. On the **Host group** **management** page, find the target host group, then click **Edit** in the **Actions** column.

4. Toggle the LogCollector service log switch to enable the feature.

5. Click **OK**.


<span id=".5YWz6Zet5pyN5Yqh5pel5b-X"></span>
## Disable the service log feature

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After the service log feature is disabled, expired log data is automatically deleted from the project of the service logs.</div>


To disable the service log feature:


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Resource management** \> **Host group**.

3. On the **Host group** **management** page, find the target host group, then click **Edit** in the **Actions** column.

4. Toggle the LogCollector service log switch off.

5. Click **OK**.
