---
title: "Notification content overview"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/notification_content_overview"
---

When configuring alarm policies in Log Service, notification content can include not only plain text strings but also custom content designed using content syntax, functions, and variables, delivering more detailed and clear alarm information in the notifications.

<span id=".5Yqf6IO95qaC6L-w"></span>
## Feature overview

The notification content of Log Service alarm notifications supports the following syntax features:


* [Content variables](https://docs.byteplus.com/docs/tls/content_variables): When configuring alarm notification content, you can add variables in addition to fixed text strings. Log Service automatically replaces variables in the notification content with their actual values when sending alarm notifications based on the alarm policy. For example, for the content variable `{{ AccountID }}`, Log Service replaces it with the BytePlus account ID associated with the current alarm policy.

* [Content syntax](https://docs.byteplus.com/docs/tls/content_syntax): Log Service provides built\-in content syntax in the alarm feature, supporting customized design and formatting of notification content and style to meet diverse notification customization needs.

* [Content functions](https://docs.byteplus.com/docs/tls/content_functions): Variable functions handle special character escaping, string truncation, and other processing on content variables, and special content filtering can be done through filters.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The alarm notification content in Log Service also supports customization through advanced functions and filters. For related business scenarios, you can contact technical support through the ticket system for more information.</div>
