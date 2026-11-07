---
title: "Callback URLs"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Callback_URL"
---

When configuring a notification policy, if notification messages need to be received via Webhook, you need to create a callback URL. This topic describes how to create and manage a callback URL.

<span id="dNaHmWMk"></span>
## Background

The egress IP addresses used by different products to send messages via the general callback URL are as follows:


|Cloud service |Region |Egress IP address |
|---|---|---|
|Cloud Monitor |Chinese mainland |`101.126.49.16/28`, `101.126.49.32/28`, `221.194.189.0/24`, `101.126.49.32`, `101.126.49.33`, `101.126.49.34` |
||Regions outside the Chinese mainland |`101.47.0.0/24 `, `145.223.191.128/26`, `145.223.191.0/25`, `145.223.191.192/26` |
|Cloud product event |Chinese mainland |`101.126.49.16/28`, `101.126.49.32/28`, `221.194.189.0/24`, `101.126.49.32`, `101.126.49.33`, `101.126.49.34` |
||Regions outside the Chinese mainland |`101.47.0.0/24 `, `145.223.191.128/26`, `145.223.191.0/25`, `145.223.191.192/26` |
|Vital Managed Service for Prometheus |Chinese mainland |`101.126.49.32/28`、`101.126.49.16/28`、`118.145.64.64/28`、`118.145.64.80/28`、`14.103.32.192/28`、`14.103.32.208/28` |
||Regions outside the Chinese mainland |`145.223.191.128/26`、`145.223.191.0/25`、`145.223.191.192/26` |
|Server\-side Monitoring |Chinese mainland |`180.184.79.11`, `180.184.141.182`, `118.145.68.136`, `101.47.76.223`, `101.47.47.14`, `163.7.12.169` |
||Regions outside the Chinese mainland |`101.47.76.223`, `101.47.47.14`, `163.7.12.169` |


<span id="ljuCQGth"></span>
## Limits

Currently, you can create up to 1,000 callback URLs.

<span id="6SAulheB"></span>
## Create a callback URL


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe).

2. In the left navigation pane, select "**Alert Center \-\> Notification configuration**" to go to the "Notification configuration" page.

3. On the **Notification object** tab, select **Callback address** to enter the callback address management page.

4. Click **Create callback address** and configure the relevant parameters as needed.

   
   |Parameter |Description |
   |---|---|
   |Callback address name |Specify a name for the callback URL. The name serves as a unique identifier for the callback URL. Duplicate names are not allowed. |
   |Channel |Select the channel included in the current callback URL and configure key information such as the callback URL and Secret.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The Feishu Secret, DingTalk Secret, custom Token, and custom Header must be consistent with the original configuration. Otherwise, the connection will fail. For example, if signature verification is enabled when you configure the Feishu custom bot, you need to enter the Feishu Secret here.</div><br> |
   ||**Lark swarm robot**: You need to configure the Feishu callback URL and Feishu Secret. For instructions on how to obtain the values and more details, see [Configuring Feishu bots](https://docs.byteplus.com/en/docs/Observability_Platform/Configuring_Feishu_bots). |
   ||**Lark application robot**: You need to complete Feishu user authentication and authorization, and select a group that has the "BytePlus Observability Alerting Bot" added. For authorization methods and more detailed instructions, see [Configuring Feishu application bots](https://docs.byteplus.com/en/docs/Observability_Platform/Configuring_Feishu_application_bots).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The system does not automatically detect which groups have the Feishu application bot added. Make sure that you select a group that has the Feishu application bot added. Otherwise, alert notifications may not be received as expected.</div><br> |
   ||**WeCom**: You need to configure the WeCom callback URL. You can also configure the "@user" mention. For instructions on how to obtain the values and more details, see [Configuring WeCom bots](https://docs.byteplus.com/en/docs/Observability_Platform/Configuring_WeCom_bots).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">"@user" is configured using WeCom account IDs. Multiple users can be configured.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The "@user" setting in the callback URL is a persistent mention. These users will be @mentioned in every message.</div><br> |
   ||**DingTalk**: You need to configure the DingTalk callback URL and DingTalk Secret. You can also configure "@user" and "@phone number" mentions. For instructions on how to obtain the values and more details, see [Configuring DingTalk bots](https://docs.byteplus.com/en/docs/Observability_Platform/Configuring_DingTalk_bots).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">"@user" is configured using DingTalk account IDs. Multiple users can be configured.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The "@user" and "@phone number" settings in the callback URL are persistent mentions. These users will be @mentioned in every message.</div><br> |
   ||**Slack**: You need to configure the Slack callback URL. For instructions on how to obtain the value, see the [official documentation](https://api.slack.com/messaging/webhooks). |
   ||**General callback address**: You need to configure a custom callback URL, custom Token, and custom Header as needed. For the egress IP addresses used to send messages via the general callback URL, see the description in the [Background](https://docs.byteplus.com/en/docs/Observability_Platform/Callback_URL) section. |
   

5. After you configure the parameters, click **Connectivity testing** in the lower\-left corner. Once the connection is verified, click **OK** in the lower\-right corner to finish the configuration.


<span id="OyzSFP59"></span>
## Managing callback URLs

Click a button in the "Actions" column to the right of the target callback URL to perform the corresponding operation. The currently supported management operations are as follows:


|Actions |Description |
|---|---|
|Edit |Edit the configuration information of an existing callback URL. |
|Delete |Delete a callback URL that is no longer needed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If a callback URL is already associated with notification policies, deleting the callback URL will also disassociate notification policies.</div><br> |
