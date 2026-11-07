---
title: "Configure resource exhaustion mitigation policies"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Configure_resource_exhaustion_mitigation_policies"
---

After configuring the compute consumption attack strategy, the LLM Application Firewall will automatically identify malicious compute consumption targeting LLM services and execute corresponding protective actions to help improve the stability of the service. This article describes how to configure the computational resource exhaustion attack strategy.

<span id="c51bb06d"></span>
## Background information

Although prompts may appear harmless, they can consume significant computational resources from a large model, potentially disrupting your service. For example, unauthorized users may input excessive content into the large model, request excessive output from it, or cause the large model to run a task at high frequency and speed for an extended period. In these scenarios, your LLM service may fail to respond to normal requests, while the LLM Application Firewall can identify these potential malicious consumption attempts, and log or intercept these requests.

<span id="3be3c284"></span>
## Prerequisites

You have connected the websites requiring protection to the LLM Application Firewall. For integration instructions, see [Introduction to assets integration](https://docs.byteplus.com/docs/LLM-Application-Firewall/introduction_to_assets_integration).

<span id="b09f2fac"></span>
## Steps


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield/).

2. In the top bar, select the region to which the instance belongs.

3. In the left navigation, select **Protection \> LLM protection \> Resource exhaustion mitigation**.

4. Enable the policy.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/3a2219f2ebbf48b3a4e68b851b19c337) </span>

5. Click **Add rule**, and configure the rule information.

   
   |Parameters |Note |Example value |
   |---|---|---|
   |Rule name |Enter the name of the protection policy.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Must start with letters or digits.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Only letters, digits, periods, underscores, and hyphens are allowed.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Length should be between 1 and 128 characters.</div><br> |rule1 |
   |Asset |Select the assets or paths to match. After selecting an asset, all paths configured under that asset will be included in the matching scope. |asset1 |
   |Trigger threshold |Supports configuring character limits for model input and output. You can use protection logs to optimize threshold configurations, enabling more accurate detection and prevention of computational resource consumption attacks.<br><br><br>* Valid threshold range: 1–30,000<br><br>* Conditional relationship: Different thresholds can be set separately for model input and output,<br><br>   * If a logical OR is applied to the two thresholds, the rule is triggered if either threshold is met.<br><br>   * When both conditions are combined using AND logic, the rule is triggered only if both thresholds are met. |Model input 2,000 characters or model output 10,000 characters |
   |Perform action |Action taken when a request meets the trigger threshold.<br><br><br>* Observe: Allow requests to pass through if the threshold is reached.<br><br>* Block: Block requests when the threshold is reached. If the asset is configured with a custom block response strategy, the system will respond to the user according to the configured content.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">All requests that trigger the protection policy are recorded in the attack details.</div><br> |Block |
   |Protection level |The detection sensitivity of the LLM Application Firewall varies based on the protection level.<br><br><br>* The available levels are `loose`, `normal`, and `strict`.<br><br>* The stricter the level, the broader the scope of risk coverage; that is, even low\-risk requests will be filtered.<br><br>* You can optimize protection level settings by using protection logs. For example, if a large number of false positives occur in `Normal` mode, you can downgrade to `Loose`. |Normal |
   |Rule switch |Enable or disable the current rule. |Enable |
   

6. Click **OK**.


<span id="d219ea32"></span>
## Configuration effects

Suppose you have configured a resource exhaustion mitigation rule for the asset. The information is as follows:


|Parameters |Value |
|---|---|
|Rule ID |rule\-d34ecr68pa51a3t7\*\*\*\* |
|Trigger threshold |The model input threshold is `2,000` characters, the model output threshold is `10,000` characters, and the conditional relationship is `OR` |
|Protection level |Normal |
|Perform action |Block |



* Protection result: The LLM Application Firewall automatically blocks the request when it detects that the user's prompt exceeds 2,000 characters or the model's output exceeds 10,000 characters.

* Log query: You can query the corresponding log information on the protection log page by filtering rule IDs.
