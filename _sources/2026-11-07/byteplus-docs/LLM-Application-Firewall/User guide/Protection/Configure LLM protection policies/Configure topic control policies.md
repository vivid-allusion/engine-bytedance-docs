---
title: "Configure topic control policies"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Configure_topic_control_policies"
---

To prevent your LLM from being misused to generate non\-compliant or reputation\-damaging content, you can configure Topic Control rules. Topic Control is an intelligent protection feature for the LLM Application Firewall that learns from your examples to intercept sensitive inputs in real time. This guide provides step\-by\-step instructions on how to create and apply these rules, using a financial business scenario as a practical example.

<span id="01b0beaa"></span>
## Important notes


* An access path can be associated with only one topic control rule.

* A maximum of 9 topics can be added under each topic control rule.

* To ensure the effectiveness of model detection, please provide clear topic descriptions and sample content whenever possible. For example:

   
   |Parameter |Configuration example |
   |---|---|
   |Topic description |`Request recommendations for specific stocks, funds, or other products` |
   |Black sample |`Please recommend three stocks that will reach the daily price limit tomorrow.` |
   |Placeholder sample |`Is it appropriate to invest parents' retirement funds in bank wealth management products?` |
   


<span id="1d6392c6"></span>
## Prerequisites

You have connected the websites you want to protect to the LLM Application Firewall. For integration\-related operations, see [Introduction to assets integration](https://docs.byteplus.com/docs/LLM-Application-Firewall/introduction_to_assets_integration).

<span id="d29e6974"></span>
## Steps


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield/).

2. Select the instance's region from the top bar.

3. In the left navigation, select **Protection \> LLM Protection \> Topic Control**.

4. Enable the policy.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/030a197321f64248ba82c6768ae7be41) </span>

5. Click **Add rule**.

   
   |Parameter |Description |Example value |
   |---|---|---|
   |Rule name |The rule name, which is used to distinguish between different topic control rules.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Must start with a letter or a digit.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Only letters, digits, periods, underscores, and hyphens are allowed.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Length should be between 1 and 128 characters.</div><br> |Topic1 |
   |Description |Provides supplementary explanations for the topic control rule. |Topic control for financial scenarios. |
   |Asset |Select the assets or paths to match. After selecting an asset, all paths configured under that asset will be included in the matching scope. |asset1 |
   |Topic name |A custom name for a controlled topic, used to distinguish it from other topics.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Starts with letters, or digits.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Letters, digits, period '.', underscore '_', and hyphen '\-' are allowed.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Length must be between 1 and 128 characters.</div><br> |Product recommendations |
   |Topic description |Provides an additional description for the current topic and helps the LLM understand the meaning of the current topic.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">Length must be between 1 and 255 characters.</div><br> |Request recommendations for specific stocks, funds, or other financial products. |
   |Sensitive words |* This configuration is optional. It can be used as a keyword for the current rule, making it easier for the large model to match the relevant detection content.<br><br>* You can enter multiple sensitive words. Press the Enter key to confirm and enter the next sensitive word. |Individual stock recommendations, fund recommendations, and product recommendations |
   |Blocked sample |Specifies common high\-risk inputs for this scenario that you want the LLM Application Firewall to block. These intercepted samples are used to train the model, enabling it to match more relevant inputs.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Up to 10 blocklist samples can be entered for each topic.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Each sample supports up to 50 characters.</div><br> |Which fund should a beginner buy? |
   |Allowed sample |Specifies common, risk\-free inputs for this scenario that the LLM Application Firewall should permit. These samples are used to train the model to recognize safe inputs, improving its matching accuracy.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can enter up to 10 allowlist samples for each topic.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Each sample supports up to 50 characters.</div><br> |Which types of investment products are more suitable for beginners? |
   |Effective scope |Specify whether the topic applies to the user's input prompt or the model's response. |Applies to prompt |
   |Action |The action to take when a request matches this topic rule.<br><br><br>* Observe: Allow requests to pass through if the threshold is reached.<br><br>* Block: Block requests when the threshold is reached. If the asset is configured with a custom block response strategy, the system will respond to the user according to the configured content.<br><br>* Secure reply: Replace the original large model's responses to users with trained answers to ensure that replies are compliant and legal.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">All requests that trigger the protection policy are recorded in the attack details.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If you are concerned that topic control rules may intercept legitimate user requests, we recommend setting the rule action to <code>Observe</code> initially. In this mode, the LLM Application Firewall does not block requests that match the rules; it only records attack logs. You can analyze the attack details to review which requests matched the rule. After confirming that the rule is working as expected, adjust the action to <code>Block</code>.</div><br> |Block |
   |Topic control switch |Enable or disable the current rule. |Enable |
   

6. Click **OK**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Caution   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After configuration is complete, you need to wait approximately 10 minutes for the topic control rules to take effect. This is because the LLM Application Firewall requires time to train on the configured topic content to generate accurate detection models.   </div>
   

<span id="0cbb0def"></span>
## Frequently asked questions

<span id="2acc2d5b"></span>
### What is the difference between topic control and custom watch list?


* The custom watch list uses regular expression\-based content matching and only hits a rule and triggers a protective action when a keyword from the watch list is detected in the input or when the input exactly matches a rule in the watch list.

* Topic control uses intelligent matching based on topic descriptions and topic samples to detect diverse topic content, more accurately identify and block non\-compliant content, and prevent model abuse.


<span id="ba613662"></span>
### Will configuring topic control policies affect normal user requests?

If you are concerned that topic control strategies may affect legitimate user requests, follow these recommendations:


1. When configuring a rule, set the action to `Observe`. In this case, the LLM Application Firewall will not intercept matched requests, but it will record attack logs.

2. Refer to [View details of attack events](https://docs.byteplus.com/docs/LLM-Application-Firewall/View_details_of_attack_events) to analyze the detection results and confirm whether the related events in the attack log match the characteristics of an attack.

3. Adjust the action to `Block` after confirming that the attack event meets expectations.
