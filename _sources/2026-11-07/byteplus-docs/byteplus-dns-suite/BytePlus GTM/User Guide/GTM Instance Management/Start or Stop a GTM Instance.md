---
title: "Start or Stop a GTM Instance"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/U5nvpy"
---

This document describes how to start or stop a GTM instance in BytePlus Cloud Scheduling (GTM).

<span id="enable-gtm-instance-scheduling"></span>
## Start a GTM instance

After you start a GTM instance, BytePlus GTM deploys DNS records to the authoritative DNS server of BytePlus GTM based on the rules of that GTM instance. At the same time, BytePlus GTM enables health checks for that GTM instance. You can view the actual DNS records deployed by BytePlus GTM through the operation logs. See [View Operation Logs](https://docs.byteplus.com/docs/byteplus-dns-suite/View_Operation_Logs).

<span id="prerequisites"></span>
### Prerequisites

Your GTM instance can be started only when it meets the following conditions:


* If the enabled policy type for your GTM instance is **basic routing**, the GTM instance must at least include a rule configured with the **default** ISP line. See [Create a Rule](https://docs.byteplus.com/docs/byteplus-dns-suite/snlUdP).

* If the enabled policy type for your GTM instance is **intelligent routing**, you need to set traffic targets for your policy. See [Set Traffic Targets for Intelligent Policy](https://docs.byteplus.com/docs/byteplus-dns-suite/c7KpPz).

    &nbsp;


<span id="steps"></span>
### Steps

Follow these steps to start a GTM instance.


1. Find the GTM instance you configured on the [Instance management page](https://console.byteplus.com/dns-suite/gtm/instances).

2. In the **Actions** column, click **Start**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If there is no <strong>Start</strong> button in the <strong>Actions</strong> column, it means your GTM instance does not meet the prerequisites for being started. You need to check your GTM instance configuration.   </div>
   

3. Click **OK** in the pop\-up window.


After BytePlus GTM deploys DNS records to the authoritative DNS server again, the DNS records in the authoritative DNS server will be updated. However, recursive DNS servers will not request DNS records from authoritative DNS server until the cached DNS records expire. The cache expiration time of DNS records is the TTL you set when creating the GTM instance.

<span id="disable-gtm-instance-scheduling"></span>
## Stop a GTM instance

After a GTM instance in the **Enabled** state is stopped, BytePlus GTM no longer deploys DNS records to the authoritative DNS server of BytePlus GTM. The GTM instance will stop health checks and will not initiate failover. However, DNS records that have already been deployed to the authoritative DNS server will not be deleted. Therefore, the authoritative DNS server of BytePlus GTM will still respond to DNS queries from users according to the rules that have been deployed.

If you need to delete DNS records deployed to the authoritative DNS server, you can [delete the GTM instance](https://docs.byteplus.com/docs/byteplus-dns-suite/umyKsn).

<span id="operation-steps"></span>
### Steps

Follow these steps to stop a GTM instance.


1. Find the GTM instance you created on the [Instance management page](https://console.byteplus.com/dns-suite/gtm/instances).

2. In the **Actions** column, click **Stop**.

3. Click **OK** in the pop\-up window.
