---
title: "Configure model abuse prevention policies"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Configure_model_abuse_prevention_policies"
---

To protect your Large Language Model (LLM) applications from malicious prompts that can cause hallucinations or harmful responses, you can configure model abuse prevention policies. This guide provides step\-by\-step instructions on how to add new policies and modify existing ones for your assets within the LLM Application Firewall console.

<span id="ed24e957"></span>
## Limitations

LLM Application Firewall currently provides multimodal detection capabilities and supports detection of text, image, and document content. 


* To use image detection capabilities, the following prerequisites are required:

   * Instance type: Prepaid Enterprise Edition instances or pay\-as\-you\-go instances

   * Image size:  Up to 10 MB

   * Image format: JPG, JPEG, PNG, WEBP, BMP, or static GIF

* To use document detection capabilities, the following prerequisites are required:

   * Instance type: Prepaid enterprise edition instances

   * Image size:  Up to 5 MB

   * Image format: TXT, DOC, DOCX, XLSX, XLS, or PDF.


<span id="d1703395"></span>
## Prerequisites

You have already connected the websites requiring protection to the LLM Application Firewall. For integration\-related operations, see [Introduction to assets integration](https://docs.byteplus.com/docs/LLM-Application-Firewall/introduction_to_assets_integration).

<span id="c69fc7d4"></span>
## Add model abuse prevention policy


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield/).

2. From the top bar, select the instance's region.

3. In the left navigation, select **Protection \> LLM protection \> Model abuse prevention**.

4. Enable the policy.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/da9ba6be090a4129849de67e425df25a) </span>

5. Click **Add rule**, then configure rule information.

   
   |Parameters |Description |Example value |
   |---|---|---|
   |Rule name |Enter the name of the protection policy.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Must start with letters or digits.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Only letters, digits, periods(.), underscores(_), and hyphens are allowed.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Length should be between 1 and 128 characters.</div><br> |rule1 |
   |Asset |Select the domain name or path to match. After selecting the domain name, all paths configured under that domain name will be included in the matching scope.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">Assets integrated via the SDK do not support path\-based matching.</div><br> |www.volcwaf001.com |
   |Content type |Set the content types to be detected. Detection is currently supported for text, image, and document content.<br><br><br>* All types: Detects all content types available for the current instance type.<br><br>* Specific types: Select text,  image, or document as needed.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Notice</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If your asset is integrated via the SDK, text, image, and document content can be detected in both the input and output directions.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If your asset is integrated via traffic or model mode,</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">In the input direction, text, image, and document content can be detected.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">In the output direction, only text content can be detected.</div><br> | |
   |Effective method |* **Checked**: To perform the same type of validation on both the input and output of the LLM, simply select **Take effect on both input and output**, then configure a unified validation category.<br><br>* **Unchecked**: To detect only model input or model output, or to perform different types of detection on input or output content, uncheck and then configure the detection categories separately. |Checked |
   |Detection category |Select the detection categories to apply. |Violence |
   |Action |Specifies the action to take when content matching a detection category is found.<br><br><br>* Observe: Allow requests to pass through if the threshold is reached.<br><br>* Block: Block requests when the threshold is reached. If the asset has a custom block response, the system will use it to respond to the user.<br><br>* Secure reply: Replaces the LLM's original response with a safe answer to ensure the final reply is compliant.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Secure reply is only applicable to assets integrated through SDK.</div><br><br><br>* <div data-tips="true" data-tips-type="default">All requests that trigger a protection policy are recorded in the protection logs.</div><br> |Observe |
   |Protection level |LLM Application Firewall implements detection with different levels of leniency based on the protection level.<br><br><br>* Supports matching rules according to `Loose`, `Normal`, and `Strict` levels.<br><br>* A stricter level provides broader risk coverage by filtering requests that may have a lower risk score.<br><br>* You can optimize the protection level configuration by referring to protection logs. For example, if there are many false positives in `Normal` mode, you can downgrade to `Loose`. |Normal |
   |Rule switch |Enable or disable the current rule. |Enable |
   

6. Click **OK**.


<span id="e487b81f"></span>
## Modify default model abuse prevention policy

When you connect your asset to the LLM Application Firewall, the platform has already created a default model abuse prevention policy. You can directly modify the policy, for example, by changing the rule name, detection category, or action.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div>


<div data-tips="true" data-tips-type="warning">The scope of assets affected by the default policy cannot be modified; it applies only to the assets associated during the initial configuration.</div>



1. Log in to [the LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield/).

2. Select the instance's region in the top bar.

3. In the left navigation, select **Protection \> LLM protection \> Model abuse prevention**.

4. Click the **Edit** button for the default rule.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">\*Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The default rule naming format is <code><asset name>Default</code>, for example, <code>bot_Default</code>.   </div>
   

5. Modify parameters such as the rule name, detection category, and action.

6. Click **OK**.
