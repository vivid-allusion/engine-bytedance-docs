---
title: "Configure sensitive data disclosure prevention policies"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Configure_sensitive_data_disclosure_prevention_policies"
---

The protection policy for sensitive data disclosure prevention is based on a robust sensitive data detection mechanism that identifies personal data in input and output content in real time and intercepts it according to preset policies. Ensure that users' personal identity information, contact details, and other sensitive data are not leaked or misused when using large model services, protecting users' privacy and security.

<span id="c0d4cd9b"></span>
## Important notes

When you connect assets to the LLM Application Firewall, the platform automatically creates a  sensitive data  policy, which can be modified. To add a sensitive data disclosure prevention policy for an asset, ensure that the detection category tags associated with different policies are not duplicated.

<span id="73edc202"></span>
## Prerequisites

You have connected the assets requiring protection to the LLM Application Firewall platform. For more information, see [Introduction to assets integration](https://docs.byteplus.com/docs/LLM-Application-Firewall/introduction_to_assets_integration).

<span id="c2a99d62"></span>
## Add sensitive data disclosure prevention policy


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield/).

2. Select the instance's region from the top bar.

3. In the left navigation, select **Protection \> LLM protection \> Sensitive data disclosure prevention**.

4. Enable the policy.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/d94230ac921c482ebc6def1e07c67501) </span>

5. Click **Add Rule** to configure the rule details.

   
   |Parameters |Description |Example value |
   |---|---|---|
   |Rule name |Enter the name of the protection policy.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Must start with a letter or a digit.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Only letters, digits, periods, underscores, and hyphens are allowed.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Length should be between 1 and 128 characters.</div><br> |rule1 |
   |Assets |Select the assets or paths to match. After selecting an asset, all paths configured under that asset will be included in the matching scope. |asset1 |
   |Effective mode |* **Selected**: To perform the same type of detection on the input and output of the large model, simply select **Synchronize input and output detection**, and then configure a unified detection category.<br><br>* **Not selected**: To detect only model input or model output, or to perform different detections on input and output, clear this option and configure the detection categories separately. |Select |
   |Applicable countries/regions |Select your target countries or regions to apply sensitive data disclosure prevention policies. |Singapore |
   |Detection categories |Filter the label categories that need to be detected.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div><br><br><br><div data-tips="true" data-tips-type="warning">Ensure that this detection category is not already used by another protection policy for the selected asset.</div><br> |ID number, bank card number |
   |Perform action |Specifies the action to perform when content in the corresponding category is detected.<br><br><br>* Observe: Allow requests to pass through if the threshold is reached.<br><br>* Block: Block requests when the threshold is reached. If the asset is configured with a custom block response strategy, the system will respond to the user according to the configured content.<br><br>* Secure reply: Replace the original large model's responses to users with trained answers to ensure that replies are compliant and legal.<br><br>* Data masking: The corresponding content will be returned to the user in a masked format (for example, the phone number `13911111111` will be displayed as `***********`).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">All requests that trigger the protection policy are recorded in the protection logs.</div><br> |Data masking |
   |Rule switch |Enable or disable the current rule. |Enable |
   

6. Click **OK**.


<span id="0b49274e"></span>
## Modify the default sensitive data disclosure prevention policy

When you connect an asset to the LLM Application Firewall, a default sensitive data protection policy is automatically created for it. You can modify this default rule's parameters, such as the rule name, detection categories, and the action to perform, but you cannot modify the scope of its affected assets. This default rule only applies to assets associated at the time of onboarding.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div>


<div data-tips="true" data-tips-type="warning">The scope of assets to which the default policy applies cannot be modified; it only applies to the assets associated during the initial configuration.</div>



1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield/).

2. In the top bar, select the region of the instance.

3. From the left navigation, select **Protection \> LLM protection \> sensitive data disclosure prevention**.

4. Click the Edit button for the default rule.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">\*Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The default rule naming format is <code><asset name>Default</code>, for example, <code>bot_Default</code>.   </div>
   

5. Modify parameters such as rule name, detection category, execution action, and more.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">\*Caution   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When classifying for association detection, ensure that this category is not currently associated with other protection policies for the selected asset.   </div>
   

6. Click **OK**.


<span id="52f57546"></span>
## Configuration effects

Suppose you have configured a sensitive data disclosure prevention rule for an asset. with the following configuration:


|Parameters |Value |
|---|---|
|Rule ID |rule\-d34ice68pa51a3t7\*\*\*\* |
|Detection category |Phone number |
|Perform action |Data masking |



* Protection result: When the LLM Application Firewall detects a phone number in the response, it returns the response with the phone number masked.

* Log query: You can find the corresponding logs on the  page by filtering by the rule ID.


&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;
