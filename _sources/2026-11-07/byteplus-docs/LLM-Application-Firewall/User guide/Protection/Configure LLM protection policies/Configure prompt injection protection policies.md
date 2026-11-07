---
title: "Configure prompt injection protection policies"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Configure_prompt_injection_protection_policies"
---

To protect your Large Language Model (LLM) from prompt injection attacks, you can configure protection policies using the LLM Application Firewall. This guide provides step\-by\-step instructions for adding new policies and modifying the default policy, ensuring your model operates securely without compromising the user experience.

<span id="d92e5f82"></span>
## What is a prompt attack?

Prompt injection is an attack where an attacker inserts harmful content into a prompt to achieve their objectives. This harmful content includes requests for large models to modify their own parameters, controlling the model to modify or delete underlying system services, and inducing it to output or leak sensitive information such as model parameters and system data.

<span id="84318656"></span>
## Important note

When you add an asset to the LLM Application Firewall, the platform automatically creates a default prompt injection protection policy, which can be modified. To add a new prompt word protection policy for assets, ensure that the detection category tags associated with different policies are not duplicated.

<span id="f99a4fac"></span>
## Prerequisites

You have connected the websites requiring protection to the LLM Application Firewall. For integration\-related operations, see [Introduction to assets integration](https://docs.byteplus.com/docs/LLM-Application-Firewall/introduction_to_assets_integration).

<span id="bf4a504a"></span>
## Add prompt injection protection policy


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield/).

2. Select the instance's region in the top bar.

3. In the left navigation, select **Protection \> LLM protection \> Prompt injection protection**.

4. Enable the policy.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/e75be1293c754b12b2ead62cf371118e) </span>

5. Click **Add rule** to configure rule information.

   
   |Parameters |Description |Example value |
   |---|---|---|
   |Rule name |Enter the name of the protection policy.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Must start with a letter or a digit.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Only letters, digits, periods, underscores, and hyphens are allowed.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Length should be between 1 and 128 characters.</div><br> |rule1 |
   |Asset |Select the assets or paths to match. After selecting an asset, all paths configured under that asset will be included in the matching scope. |asset1 |
   |Detection classification |After detecting and classifying a threat, the LLM Application Firewall performs the configured action based on the wordlist for that classification.<br><br> |Role\-playing |
   |Action |When the firewall detects content in a specified category, it performs the configured action.<br><br><br>* Observe: Allow requests to pass through if the threshold is reached.<br><br>* Block: Block requests when the threshold is reached. If the asset is configured with a custom block response strategy, the system will respond to the user according to the configured content.<br><br>* Secure reply: Replaces the model's original response to the user with a predefined answer to ensure the reply is compliant and safe.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">All requests that trigger the protection policy will be recorded in the attack details.</div><br> |Intercept |
   |Rule switch |Enable or disable the current rule. |Enable |
   

6. Click **OK**.


<span id="0db7eb63"></span>
## Modify default prompt injection protection policy

When you connect an asset to the LLM Application Firewall, the platform automatically creates a default prompt injection protection policy. You can modify this policy directly, for example, by changing the rule name, detection category, or action.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div>


<div data-tips="true" data-tips-type="warning">The scope of assets to which the default policy applies cannot be modified. It only applies to assets associated during the initial configuration.</div>



1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield/).

2. In the top bar, select the region of the instance.

3. Select **Protection \> LLM protection \> Prompt injection protection** in the left navigation.

4. Click **Edit** for the default rule.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The default rule naming format is <code><asset name>Default</code>, for example, <code>bot_Default</code>.   </div>
   

5. Modify rule name, detection category, execution action, and other parameters.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">\*Caution   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When checking category associations, ensure that the category is not yet associated with other protection policies for the selected asset.   </div>
   

6. Click **OK**.


<span id="cf70a6b0"></span>
## Configuration effects

Assume you have configured a prompt injection protection rule for the asset. The information is as follows:


|Parameters |Value |
|---|---|
|Rule ID |rule\-d34ecr68pa51a3t7\*\*\*\* |
|Detection classification |Role\-playing, Prompt\-stealing |
|Action |Block |



* Protection result: The LLM Application Firewall has detected prompt injection risks in the user's prompt, including role\-playing and prompt\-stealing, and will automatically block this request.

* Log query: You can query the corresponding log information on the protection log page by filtering by rule ID.
