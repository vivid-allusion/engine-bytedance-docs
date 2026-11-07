---
title: "Using TOS Agent"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Using-TOS-Agent"
---

This topic primarily covers the layout of the chat interface and how to use TOS Agent.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">TOS Agent is currently in closed beta. Please contact your account manager for access.</div>


<span id="DyBymqOs"></span>
## Prerequisites


1. Make sure that you have created a BytePlus account and completed real name verification. For more information, see [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/Account/sign-up-and-verify-byteplus-account?redirect=1).

2. Make sure that you have activated TOS for your account or Identity and Access Management (IAM) users. For more information, see [Activate TOS](https://docs.byteplus.com/en/docs/tos/docs-quick-start_1).


<span id="l4QKolCa"></span>
## Using TOS Agent


1. Log in to [the TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **TOS Agent** to access the chat interface.

3. Type your request into the chat box at the bottom of the page, or select a scenario card under the chat box.


The TOS Agent interface has three parts:


* **Sidebar on the left**: This area provides options to **create new conversations**, select a **region** and **bucket**, and view **task history**.

* **Chat box in the center**: This is where you interact with TOS Agent by entering your requests. You can use @ in the chat box to temporarily reference a bucket or a flow rule. This tells the agent which bucket or rule the operation applies to.

* **Workspace on the right**: This is the collaborative area between the agent and the console. It is not displayed by default. It only appears when you submit a request involving the creation of a bucket or upload of objects. At that point, **a form will appear that needs to be filled out**.


<span id="k9amUgJf"></span>
## Examples


<Tabs>
<Tab zoneid="C7feUA1geA" title="General conversations">
<TabTitle>General conversations</TabTitle>

You can chat with TOS Agent using natural language. When replying, the agent shows you its entire thought and execution process so that you can monitor the processing status in real time.


</Tab>
<Tab zoneid="ynGpaloNzh" title="Access anomaly diagnosis">
<TabTitle>Access anomaly diagnosis</TabTitle>

If you are unable to access TOS resources as usual, the agent will identify the cause of the issue, such as an expired signature or denied permission, and provide clear instructions on how to resolve it. For sensitive operations, such as configuration changes, the agent requires your confirmation before executing them.


</Tab>
<Tab zoneid="peLYHP4sxN" title="Creating buckets">
<TabTitle>Creating buckets</TabTitle>

You can describe your bucket creation requirements using natural language. The agent will convert the request into a structured set of parameters and open a form for you to review and complete. Then, the agent will submit the request to complete the creation process. If the operation fails due to insufficient permissions or other reasons, the agent will display a specific error message and allow you to retry or cancel the operation.


</Tab>
<Tab zoneid="cCgo34kZsM" title="Data analytics">
<TabTitle>Data analytics</TabTitle>

TOS Agent can act as your data analysis assistant. It supports queries about bucket resource usage, such as storage status, bandwidth, throttling, and overall assessment. This helps you understand your resource usage.


</Tab>
<Tab zoneid="UdzMRclWo7" title="Multimodal retrieval">
<TabTitle>Multimodal retrieval</TabTitle>

Enter your retrieval requirements in the chat box. The agent will display each result as a large image or video preview in a pop\-up window. Zooming and downloading are supported.


</Tab>
</Tabs>


<span id="NAGMYHwn"></span>
###
