---
title: "Scaling rule FAQ"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Scaling-policy-FAQs"
---

<span id=".5Ly457yp57uE5Lit5Y-v5Lul5ZCv55So5aSa5Liq5Ly457yp6KeE5YiZ5ZCX77yf"></span>
## Can multiple scaling rules be enabled for a scaling group?

Multiple scaling rules can be enabled simultaneously for a scaling group. However, scaling rules compete with one another. When multiple adjustments are triggered simultaneously, only the one that preempts execution will be performed.

<span id=".5Ly457yp6KeE5YiZ55qE5Ya35Y205pe26Ze05ZKM5Ly457yp57uE55qE5Ya35Y205pe26Ze05pyJ5LuA5LmI5Yy65Yir77yf"></span>
## What is the difference between the cooldown time of a scaling rule and that of a scaling group?


* If you configure cooldown time for both the scaling group and the scaling rule, Auto Scaling will prioritize the cooldown time of the scaling rule.

* If your scaling rule has no configured cooldown time, the Auto Scaling service will use the scaling group's cooldown time. The scaling group's cooldown time is required.


For more information, see [Cooldown time](https://docs.byteplus.com/en/docs/as/Cooldown-period).

<span id=".5aaC5L2V6I635Y-W5Ly457yp57uT5p6c77yf"></span>
## How do I obtain scaling results?

You can obtain scaling results by using either of the following methods:


* [Scaling log](https://docs.byteplus.com/en/docs/as/Viewing-scaling-activities): The Auto Scaling service records the results of scaling activities for each scaling group, including the conditions that triggered scaling, adjustment types, start/stop time, and execution results. This provides a channel for event recording and review.

* [Scaling notification](https://docs.byteplus.com/en/docs/as/Notification-channels): The Auto Scaling service sends scaling activity notifications to you via multiple channels such as internal messages, email, SMS, and alert callbacks. This helps you promptly track changes to your scaling groups.
