---
title: "Reference for Callback Details"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75124"
---

<span id="introduction"></span>
## Introduction

After enabling the message notification service, your server will receive POST requests from the RTC server containing event details.

You can read this document to understand the callback details.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div>


<div data-tips="true" data-tips-type="default">The URL for receiving callbacks must start with a domain name.</div>


<div data-tips="true" data-tips-type="default">If you choose a HTTPS URL to receive callbacks, you must ensure the SSL certificate for this domain is valid.</div>


<span id="callback-parameters"></span>
## Callback parameters

<span id="body"></span>
### Body


|Parameter |Type |Example |Description |
|---|---|---|---|
|EventType |String |`RecordStarted` |The event type. |
|EventData |String |/ |The event parameters. |
|EventTime |String |`1970-07-01T 00:00:00.000000000 Z` |The UTC when the event occurs.<br><br>Use RFC 3339 format. In the RFC 3339 format, dates and times are represented in the following format: YYYY\-MM\-DDTHH: MM:SSZ, where T is the separator between the date and time, and Z indicates the time is in Coordinated Universal Time (UTC). |
|EventId |String |/ |The event ID, which can be used to deduplicate event callbacks. |
|AppId |String |`Your_AppId` |Your App ID. |
|Version |String |`2020-12-01` |The API version to use. |
|Signature |String |/ |The event callback signature. |
|BusinessId |String |/ |The Business identifier for your audio & video app. |
|Nonce |String |/ |A 4\-digit random number used for the signature. |


> Note:

> See [EventType Reference](https://docs.byteplus.com/docs/byteplus-rtc/docs-75125) for details on the `EventType` and `EventData` parameters.
