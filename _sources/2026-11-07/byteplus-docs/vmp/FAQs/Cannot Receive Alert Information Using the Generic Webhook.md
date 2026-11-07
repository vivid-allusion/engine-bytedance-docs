---
title: "Cannot Receive Alert Information Using the Generic Webhook"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Cannot_Receive_Alert_Information_Using_the_Generic_Webhook"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue Description

A user configured an alert contact and used the Generic Webhook to receive alert information. Among them, the Webhook address is the Webhook address of the WeCom alert robot. After configuration, it was found that alert information could not be correctly received via WeCom.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause Analysis

This is because the generic webhook format provided by VMP is incompatible with WeCom. The alert information sent by Vital Managed Service for Prometheus in the Generic Webhook format cannot be parsed by WeCom, resulting in failure to correctly receive alert information.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the details of the Generic Webhook format, please refer to <a href="https://docs.byteplus.com/en/docs/vmp/general-webhook-format">Generic Webhook Format Description</a>.</div>


<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution

The solution to this issue is as follows:


1. If you want to receive alert information through the generic webhook, make sure that the receiving endpoint can parse the generic webhook format.

2. If you want to receive alert information through Feishu, DingTalk, WeCom, or other tools, please refer to the following document:

   * [Receiving alert information through the the Feishu bot](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-Lark)

   * [Receiving alert information through the Feishu application bot](https://docs.byteplus.com/en/docs/vmp/Receiving_alerting_notifications_through_Lark_application_robot)

   * [Receiving alert information by DingTalk](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-DingTalk)

   * [Receiving alert information by WeCom](https://docs.byteplus.com/en/docs/vmp/Receiving_alerting_notifications_through_Wecom)
