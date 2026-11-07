---
title: "Setting Webhook"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Setting_Webhook"
---

Webhook is used to provide A2A\-protocol\-based external access to ArkClaw, establishing a linked call channel between ArkClaw and enterprises' internal business systems. Once this feature is enabled, the system automatically generates an Endpoint URL and an API Key. These credentials can be used to integrate internal IM, OA, CRM, and other business systems, and also allow A2A clients to actively call the current ArkClaw instance.

This feature is intended for **in\-depth use by technical developers** with certain interface integration and debugging capabilities.

<span id="VvBzBIMQ"></span>
## Prerequisites


* Contact your administrator to confirm that the A2A endpoint capability is enabled in the global workspace configuration.

* Shared Claw only allows its **administrator** to use this feature.


<span id="T6zxRtZZ"></span>
## Applicable scenarios


* **Enable Webhook**

   The system will enable A2A\-protocol\-based external access. Once Webhook is enabled, the system automatically generates an **Endpoint URL** and an **API Key**, which can be used to integrate enterprises' internal systems, or for A2A clients to actively call the current ArkClaw instance.

* **Disable Webhook (default)** 

   The system will disable A2A\-protocol\-based external calls. Once Webhook is disabled, the generated Endpoint URL and API Key will become invalid, and relevant enterprise systems or A2A clients cannot call the current ArkClaw instance via these access credentials.


<span id="4TLmhDVp"></span>
## Procedure


1. Open a browser, enter the ArkClaw login link in the address bar, and press the "Enter" key.

2. Switch to the target ArkClaw page and click the details icon in the upper\-right corner.

3. Click the "Settings" tab.

4. Enable or disable Webhook as needed.

   * **Enable**: Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_29943bc13a6d60ac7f74a0580b856fa8.png) </span> icon to enable Webhook.

   * **Disable**: Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ec7388db125645f4674fdc5d7f1c8ee1.png) </span> icon to disable Webhook.


<span id="7K7ux20B"></span>
## Related operation

After enabling Webhook, you can copy endpoint information, obtain integration code, or perform other operations on the current page, which will be used for interface integration between business systems and ArkClaw Enterprise.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Keep the endpoint information and integration code confidential. Do not disclose or forward them to external parties to avoid security risks to your account and platform resources.</div>


<span id="ZnmWEax3"></span>
### Obtain endpoint

The private endpoint is suitable for system calls in private network environments, and the public endpoint is suitable for integrating business systems that can be accessed via public networks. On the right of the endpoint, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e696989f17935e7872baf0611cdf92ff.png) </span> icon to obtain the corresponding information.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For public network API calls, see <a href="https://docs.volcengine.com/docs/87732/2565932?lang=zh">ArkClaw A2A API integration: basic calls</a> or <a href="https://docs.volcengine.com/docs/87732/2563047?lang=zh">ArkClaw A2A API integration: session\-based multi\-turn conversations</a>.</div>


<span id="JgljCyS8"></span>
### Copy the integration code


1. Click the "Click to view" button.

2. Select the "python" or "CURL" tab to view the sample code for the corresponding language or call method.

3. Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e696989f17935e7872baf0611cdf92ff.png) </span> icon to copy the integration code under the current tab and paste it into a business system, server\-side script, or debugging tool. Then, edit the request parameters, authentication information, and business data as needed to enable integration and calls between ArkClaw and existing business workflows.


<span id="hnefhynV"></span>
### Configure business tags

A tag is a key\-value pair used to identify ArkClaw. Tags help you categorize ArkClaw with similar attributes based on different dimensions, such as purpose, owner, or environment.


1. On the right of the business tag, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ea479ab9d0af139ed9d8e00cdf3a024d.png) </span>.

2. In the business tag pop\-up window, associate tags with or dissociate tags from ArkClaw as needed.

   * **Associate tags**:

      1. Click the "Add tag" button.

      2. From the drop\-down list, select the key\-value pair of the tag to be added.

         <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="3">warning         </div>
         

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="3">You can select only tags preconfigured by the administrator. Custom tags created by employees are not supported.         </div>
         

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="3">Each ArkClaw can be associated with up to 20 tags.         </div>
         

      3. Click the "Confirm" button to complete the operation.

   * **Disassociate tags**:

      1. On the right of an existing tag, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_82b6c404d7ab7b58a5a99165a0727444.png) </span>.

      2. Click the "Confirm" button to complete the operation.
