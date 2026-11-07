---
title: "Configure a custom response rule"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Configure_a_custom_response_rule"
---

To provide tailored, safe responses when your LLM application detects specific risks, you can use the custom response repository. This guide provides step\-by\-step instructions on how to configure custom response rules in the LLM Application Firewall, helping you improve response efficiency and ensure a secure user experience.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, custom response rules are only available for <strong>Enterprise edition instances</strong>.</div>


<span id="d9c5fc6c"></span>
## Usage scenarios


* **Customized response output**: You can configure dedicated response repositories based on different risk categories. When user input or generated content triggers the corresponding risk, the LLM Application Firewall outputs a customized response from the response repository, meeting security protection requirements in various scenarios. You can retrieve the response content via the API to send to users.

* **Improve response efficiency and stability**: The response repository can directly match and output predefined responses, avoiding issues such as response delays, unstable content, or excessive token consumption caused by relying on an LLM for generation, which enables rapid responses.


<span id="82ac46f3"></span>
## Notifications


* You can configure up to 100 response rules.

* Custom responses have a higher priority than model answers from the LLM Application Firewall.

* If multiple response rules are triggered, the LLM Application Firewall will randomly return the content from one of the corresponding responses.


<span id="a5f0226b"></span>
## Steps


1. Log in to the [LLM Application Firewall console](https://console.volcengine.com/omni-shield/llm-shield/).

2. Select the region where the instance is located in the top bar.

3. In the left navigation, select **Protection \> Custom response list**.

4. Click **Add response rule** .

5. Configure the answer rule parameters.

   
   |**Configuration items** |**Note** |**Example value** |
   |---|---|---|
   |Rule name |Name of the response rule.<br><br>Naming rules:<br><br><br>* Must start with a letter or digit.<br><br>* Letters, digits, periods (.), underscores (_), and hyphens (\-) are allowed.<br><br>* Length must be 1–128 characters. |Non\-compliant stock recommendation |
   |Description |Enter the usage scenario or other remarks for this auto\-response rule to facilitate understanding and management.<br><br>Supports up to 255 characters. |Returns the specified answer when a violation related to stock recommendations is detected. |
   |Detection category |Associate with the corresponding detection category. |General topic control |
   |Response content |Enter a predefined response. When the detected content matches the relevant detection category, the LLM Application Firewall will return this predefined response. |Hello, I am unable to provide advice related to this topic. |
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf88997a4f5547b2806c469e9b5d1b54~tplv-goo7wpa0wc-image.image) </span>

6. Click **Confirm**.


<span id="edbc2024"></span>
## Subsequent operations

You can filter events with the action `Secure reply` on the protection log page to view the execution status of related response rules.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad24a284b583493c907965681acfb977~tplv-goo7wpa0wc-image.image) </span>
