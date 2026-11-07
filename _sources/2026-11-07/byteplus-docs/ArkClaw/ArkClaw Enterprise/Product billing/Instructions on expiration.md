---
title: "Instructions on expiration"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Instructions_on_expiration_"
---

After the  of a subscription seat expires, the platform offers a retention period. During this period, you can renew it based on your need for continuous use. If you do not perform any operations during the resource retention period, the resources related to the seat  are forcibly released after the period ends. This operation is irrecoverable. This topic describes the impacts on the  of subscription seats when they expire, as well as the methods of handling resources after expiration.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The viewing path described in this topic applies to workspaces of the seat management type. If your workspace is of the instance management type, the expiration dates of each instance are independent of each other. Please view the expiration time of each instance in the instance list, and renew instances that are about to expire <a href="https://docs.byteplus.com/en/docs/ArkClaw/Renew_unsubscribe_or_delete_a_Claw_instance">individually</a> as needed.</div>


<span id="75FQM1Vc"></span>
## Expiration rules

When your ArkClaw expires, it stops after 12 hours, and its **associated resources are retained for 7 days (168 hours)** . If you do not renew it within this period, the system automatically deletes your data.

An expired Coding Plan package becomes unavailable and is no longer renewable **12 hours** after expiration. To continue using the service, you need to purchase additional [Coding Plan](https://docs.byteplus.com/en/docs/ModelArk/2276791#rules) seats.


> * For the first combined purchase of Coding Plan, the validity period aligns with that of ArkClaw and expires simultaneously with ArkClaw.

> * For Coding Plan purchased during a [seat change](https://docs.byteplus.com/en/docs/ArkClaw/Modify_seat), the expiration time is determined by the validity period selected on the seat change page.

> * The Coding Plan or Agent Plan separately purchased expires based on the validity period selected on the ModelArk seat purchase page.


<span id="0GLYbsbm"></span>
## Instructions on release after expiration


|Item |Description |
|---|---|
|Expiration time |23:59:59 on the expiration day. |
|Shutdown time |12 hours after expiration.<br><br>After your ArkClaw instance stops, its status will change to **Stopped**. |
|Release time |7 days (168 hours) after expiration.<br><br><br>* Data: **Retained for 7 days** and automatically cleared after timeout.<br><br>* ArkClaw: Automatically deleted after 7 days. |


<span id="Kt7TkVzk"></span>
## Resource status after expiration

The following figure shows the resource status at different stages after expiration.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Based on the <a href="https://console.byteplus.com/message/setting">notification method</a> you specify, the platform sends notifications via SMS, email, or internal message 7 days before, on the day of, and 24 hours after your ArkClaw expires. These notifications inform you about impending expirations, resource suspensions, and resource releases. Please monitor these notifications closely.</div>


* <div data-tips="true" data-tips-type="default">For orders without <a href="https://docs.byteplus.com/en/docs/ArkClaw/Renewal_description?lang=en">auto\-renewal</a> enabled, starting from the 7th day before seat expiration, notifications about upcoming resource expiration, service suspension upon expiration, and resource reclamation will be displayed in the console. Pay attention to these notifications.</div>


* <div data-tips="true" data-tips-type="default">If all orders in the space trigger the reclamation mechanism, all resources (including templates, images, skills, knowledge, cloud disks, and user information) in that space will be permanently deleted and cannot be recovered.</div>



<span id="FgCwKxDu"></span>
## View expiration time

You can view the subscription seat expiration time to plan renewals and prevent service interruptions when subscription seats stop upon expiration.


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise). 

2. In the left navigation pane, click "Resource Configuration" \> "Seats".

3. Click the “Seat overview” tab, and view the seat expiration time in the **Claw seat** section.

   > You can also click "ModelArk Plan details" to view the Coding Plan expiration time, status, and other information in the ModelArk Plan section.
