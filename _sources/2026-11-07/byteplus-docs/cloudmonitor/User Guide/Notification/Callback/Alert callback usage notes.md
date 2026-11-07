---
title: "Alert callback usage notes"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Webhook-instructions"
---

In a Cloud Monitor alert policy, you can specify an alert callback URL. This topic describes the usage notes for the callback URL and the parameters included in POST requests sent by the Cloud Monitor alert callback API.

<span id="aafb90ed"></span>
## Background

When you create an alert policy, you can specify an alert contact group or an alert callback URL to receive alert notifications in the Alert way section on the Create alert policy page. The following figure provides an example. For the steps of creating alert policies, see [Creating alert policies](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy). 

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you have created an alert policy for which no alert callback URL is specified, you can edit the existing alert policy to add an alert callback URL. For specific operations, refer to <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Modifying-an-alarm-strategy">Modifying an alert policy</a>.</div>


If you have created an alert policy for which an alert callback URL is specified, when the monitored cloud service triggers the alert policy, Cloud Monitor will send an alert notification to the members in the specified contact group. In addition, Cloud Monitor will invoke the alert callback API to initiate a `POST` request to the specified URL. The request will carry the request body of the alert notification (`application/json`).

The webhook callback can be retried up to three times, with each attempt timing out after 8 seconds. The client may determine that the request timed out and trigger a retry even though the server has already received the request. As a result, repeated callbacks occur. You can check the uniqueness of the request based on the value of `x-volc-trace-id ` in the request header because retry requests carry the same value of `x-volc-trace-id`.

<span id="a1cce06c"></span>
## Limits on the alert callback URL

The alert callback URL can receive alert notifications only if the following conditions are met:


* Cloud Monitor can directly access the URL. Therefore, the URL must be accessible over the public network.

* The URL must only contain English characters (half\-width characters), and cannot start or end with meaningless spaces or line breaks.

* The URL must be in the following format:

   ```Plain
   schema://host/path#query-param
   ```
   

   In the URL:

   * `schema`: the request protocol. Both HTTP and HTTPS are supported.

      Cloud Monitor does not automatically add a protocol to the alert callback URL. Therefore, you must manually add a protocol when you specify the URL.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Cloud Monitor supports both HTTP and HTTPS. If the URL cannot be resolved due to an invalid protocol, Cloud Monitor cannot trigger alert callbacks.      </div>
      

   * `host/path`: the request domain name and route, which are used to receive alert notifications.

   * `query-param`: the request parameters

      Cloud Monitor does not modify the content of the request parameters but encodes the request parameters. Therefore, the callback receiver needs to decode the data in the URL to obtain valid parameter data.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Cloud Monitor does not recommend using query parameters, and it does not add any query parameters.      </div>
      

   Sample URL:

   ```Plain
   http://example.com/open-apis/bot/v2/hook/131ad***
   ```
   


<span id="ad0b7184"></span>
## Related document


* To view the request content of a metric alert callback for cloud services, refer to [Request content of a metric alert callback](https://docs.byteplus.com/en/docs/cloudmonitor/request-content-of-metric-alarm-callback).

* To view the request content of an event alert callback for cloud services, refer to [Request content of an event alert callback](https://docs.byteplus.com/en/docs/cloudmonitor/Content-of-a-webhook-request-of-the-event-type).


&nbsp;
