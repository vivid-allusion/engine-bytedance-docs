---
title: "Access log delivery to TOS"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Obtaining-access-logs"
---

This article introduces how to deliver access logs from Layer 7 (HTTP/HTTPS) listeners to Torch Object Storage (TOS).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This feature does not apply to HTTP/HTTPS requests on Layer 4 TCP listeners.</div>


<span id=".5byA5ZCv6K6_6Zeu5pel5b-X"></span>
## Enable the access log feature

<span id="kfJAfldR"></span>
### Prerequisites


* Ensure you have enabled Torch Object Storage (TOS) and Torch Log Service (TLS).

* When enabling access logs for the first instance under an account, ensure the associated role is authorized for the CLB service.

* An HTTP listener or HTTPS listener has been created for CLB. If not created, see [Creating an HTTP listener](https://docs.byteplus.com/en/docs/clb/Creating-an-HTTP-listener) or [Creating an HTTPS listener](https://docs.byteplus.com/en/docs/clb/Creating-an-HTTPS-listener).


<span id="0OIkzSNz"></span>
### Procedures


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the project and region.

3. Click the target CLB instance name.

4. On the Overview tab, click Configure Access Log Delivery to TOS.

5. If this is the first time My account enables the access log feature, follow these steps:

   1. On the automatically redirected Cross\-service access request page, click Authorization.

   2. On the Overview tab of the source instance details page, click Configure Access Log Delivery to TOS again.

6. Turn on the Enable Access Log switch, and select an existing bucket or create a new one.

7. Click **Configure** to complete the action.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After enabling access log, wait about 5 minutes for the first log file to upload to the bucket before you can view it.</div>


* <div data-tips="true" data-tips-type="tip">CLB organizes access logs into files at fixed intervals (currently default is 5 minutes, adjustment not supported) and uploads them to your specified bucket. If no access occurs during the fixed interval, no access log file will be generated.</div>



<span id=".5p-l55yL5pel5b-X5paH5Lu2"></span>
## View log files


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the project and region.

3. Click the target CLB instance name.

4. On the Overview tab, click Bucket Name.

5. In the left\-side navigation pane, click File List.

6. Click **CLBAccessLogs/ \> ** ***YYYY*** **/ \> ** ***MM*** **/ \> ** ***DD*** **/** .

   > *YYYY*, *MM*, and *DD* represent directories named by year, month, and day, e.g., CLBAccessLogs/ \> 2021/ \> 8/ \> 17/.   
   

7. Click Download on the right side of the target file. After downloading, unzip it to view the contents.


<span id=".5YWz6Zet6K6_6Zeu5pel5b-X"></span>
## Disable the access log feature


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click the target CLB instance name.

4. On the Overview tab, click Configure Access Log Delivery to TOS.

5. Turn off the Enable Access Log switch and click OK to complete the actions.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [EnableAccessLog](https://docs.byteplus.com/en/docs/clb/EnableAccessLog)

* [DisableAccessLog](https://docs.byteplus.com/en/docs/clb/DisableAccessLog)


&nbsp;
