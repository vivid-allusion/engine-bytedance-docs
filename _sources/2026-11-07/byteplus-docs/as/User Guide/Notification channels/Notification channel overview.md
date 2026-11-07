---
title: "Notification channel overview"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Overview_of_notification_channels"
---

The Auto Scaling service supports notifications about scaling operations via internal messages. This way, you can promptly learn about changes in a scaling group.

<span id=".6YCa55-l5rig6YGT57G75Z6L"></span>
## Notification channel type

A scaling group supports two types of notification channels: event notification and message notification.


|Channel type |Introduction |Related cloud product |Procedure |
|---|---|---|---|
|Message notification |Scaling activity results are notified via internal messages, SMS, or email. You need to manually manage related events after receiving a message. |[Message Center](https://docs.byteplus.com/en/docs/message_center/What-Is-Message-Center) |1. [Configuring message reception channels](https://docs.byteplus.com/en/docs/as/Managing_message_notifications#.6YWN572u5raI5oGv5o6l5pS2)<br><br>2. [Creating message notifications](https://docs.byteplus.com/en/docs/as/Managing_message_notifications#.5Yib5bu65raI5oGv6YCa55-l) |


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* Each scaling group only supports creating  and one message notification.
