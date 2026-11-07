---
title: "Limit"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Limits"
---

This topic describes some limits during the use of Vital Managed Service for Prometheus (VMP).

<span id=".5Z-656GA6ZmQ5Yi2"></span>
## Basic limit


|Limit |Quota |Limit Exceeding Solution |
|---|---|---|
|The maximum number of workspaces per region |Standard Edition workspace: 100<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To view the quota details in different regions, go to the <a href="https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=vmp">quota center</a>.</div><br> |To increase the quota, go to the [quota center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=vmp) to apply. |
|The maximum number of groups configured in a workspace |20 | |
|The maximum number of labels per metric |30 |Automatically discard |
|The maximum length of the label name for a metric |256 bytes |Automatically discard |
|The maximum length of the label value for a metric |2,048 bytes |Automatically discard |
|When the number of newly aggregated metrics exceeds 2,000, it cannot be greater than 16 times the number of original metrics. |\- |Return a limit exceeding error. |
|Each sample must have a metric name. |\- |Automatically discard |
|The minimum query interval of recording rules |5 seconds |\- |
|The maximum number of rules configured in a recording rule group |20 |\- |
|The maximum size of a recording rule file |1 MB |\- |


<span id=".5oyH5qCH5YaZ5YWl6ZmQ5Yi2"></span>
## Metric write limit


|Limit |Quota |Limit Exceeding Solution |
|---|---|---|
|The timestamp carried during the writing of a metric |1 hour |Automatically discard |
|The maximum size of a written request data packet |32 MiB |Return a limit exceeding error. |


<span id=".5oyH5qCH5p-l6K-i6ZmQ5Yi2"></span>
## Metric query limit


|Limit |Quota |Limit Exceeding Solution |
|---|---|---|
|The maximum query time range |31 days |\- |
|Single query timeout |30 seconds |\- |
|The maximum size of a single query result |512 MiB |\- |
|The time interval after which metrics can be queried after collection. |30 seconds |\- |
|The number of samples of a time series in each query result |10,000 |Return a limit exceeding error. |
|The number of queried original samples for each time series |5,000,000 per time series |Return a limit exceeding error. |
|The total number of queried original samples |300,000,000 |Return a limit exceeding error. |
|The maximum length of a query statement |128 KB |Return a limit exceeding error. |


<span id=".5ZGK6K2m5Lit5b-D"></span>
## Alerting center limit


|Limit |Quota |Limit Exceeding Solution |
|---|---|---|
|Alert storage duration |7 days |Delete upon expiration. |
|Number of contacts containing phone numbers (per root account per region) |30<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The number of contacts without phone numbers is not limited.</div><br> |\- |
|Number of contacts containing phone numbers (per root account per region) |20 times/day |Wait until 0:00 when the quota is refreshed each day. |
|The number of times that the phone number of a contact can be modified |3 times |Delete the contact and create a new contact. |
|Alerting rule |500 |The creation failed. |
|Contact |100 |The creation failed. |
|Contact group |100 |The creation failed. |
|Alerting notification policy |20 |The creation failed. |
|Notification template |100 |The creation failed. |
|Alerting aggregation policy |5 |The creation failed. |
|Alerting silence policy |1,000 |The creation failed. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Minute\-level and day\-level frequency limits take effect at the same time. If any level of limit is exceeded, messages will fail to be sent.</div>


* <div data-tips="true" data-tips-type="tip">The minute\-level and day\-level frequency limits take effect starting from the receipt of the first message.</div>



<span id="kv52UJek"></span>
## Alerting notification limit


|**Limit** |**Limit Description** |
|---|---|
|Phone number |* A phone number can receive up to 300 phone calls per day.<br><br>* A phone number can receive up to 1 phone call and 3 text messages per minute.<br><br>* A root user and its Identity and Access Management (IAM) users can receive up to 300 **phone** calls per hour and up to 100 phone calls per minute. |
|Text message |* A phone number can receive up to 300 text message notifications per day.<br><br>* A phone number can receive up to 1 phone call notification and 3 text message notifications per minute.<br><br>* A root user and its IAM users can receive up to 300 **text message** notifications per hour and up to 100 text message notifications per minute. |
|Email |* An email address can receive up to 100 email notifications per minute.<br><br>* An account can receive up to 100 email notifications per minute. |


<span id=".6LWE5rqQ5raI6ICX"></span>
## Resource consumption limit


|Limit |Quota |Limit Exceeding Solution |
|---|---|---|
|The duration of resource consumption statistics |6 months |Delete upon expiration. |
