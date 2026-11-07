---
title: "Custom protection description"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Introduction_to_custom_protection"
---

Large Model Application Firewall provides rich preset protection capabilities that cover general security scenarios. For dedicated risks, industry terms, internal materials, or specific violation patterns in your enterprise business, you can also use custom protection capabilities for fine\-grained control.

The core logic of custom protection is: first create a **detection category**, then create a custom capability and associate it with the category, and finally associate the detection category with effective assets and execution actions through **custom detection rules**. Custom protection capabilities take effect on target assets only after these three steps are completed.

Custom protection currently includes the following capabilities:


* **Custom watch list**: Identifies specified text content through exact match, keyword match, or regular expression match. It is suitable for whitelists, blocklists, industry terms, fixed risk expressions, and other scenarios.

* **Custom model**: Trains a dedicated protection model based on the positive and negative samples you provide. It is suitable for complex semantics, vertical industry risks, and business scenarios that are difficult to cover with general policies.


<span id="30fa0723"></span>
## Key concepts

&nbsp;


|**Concept** |**Description** |
|---|---|
|Detection category |The organization and association unit for custom protection. Custom watch lists and custom models all need to be associated with detection categories. Subsequent rules control the effective scope through detection categories. |
|Custom capability |Refers to a custom watch list or custom model, and is used to define "what needs to be identified". |
|Custom detection rule |Used to define "which assets it takes effect on" and "how to handle hits". You need to select assets, detection categories, and execution actions in the rule. |
|Execution action |The handling method taken after a detection category is hit, such as allow, block, safe response, or observe. |
|Effective asset |The target asset bound to a custom detection rule. Only assets bound to the rule apply the corresponding custom protection capabilities. |


<span id="b82dd5be"></span>
## Capability selection

Different custom capabilities are suitable for different problems. Select the appropriate capability based on your detection objective.

&nbsp;


|**Custom capability** |**Applicable scenario** |**Configuration method** |**Effective method** |
|---|---|---|---|
|Custom watch list |Identifies fixed words, industry terms, whitelist content, blocklist content, and text in specific formats |Configure entries, keyword combinations, or regular expressions, and associate them with detection categories |Takes effect after you select detection categories and assets through custom detection rules |
|Custom model |Identifies complex semantic risks, vertical business violation content, and expressions that are difficult to identify with general policies |Upload positive and negative samples to train the model, and associate sample topics with detection categories |After the model is published, it takes effect after you select detection categories and assets through custom detection rules |


<span id="3155df10"></span>
## Scenario examples


* **Financial compliance word control**: For example, if an enterprise wants to block non\-compliant marketing expressions such as "principal guaranteed" and "zero risk", it can create a custom watch list and associate it with the detection category `FinancialCompliance`. Then it can create custom detection rules for related assets and set the execution action to **block** or **observe**.

* **Vertical business model protection**: For example, if an enterprise wants to identify complex semantic risks such as illegal financial Q&A and non\-compliant code generation, it can create a custom model based on real business samples, associate sample topics with detection categories, and make the model take effect on target assets through custom detection rules after the model is published.


<span id="ff2e1850"></span>
## Process description

You can use the following process to make custom protection capabilities take effect on specified assets:

<span id="0aa39bd9"></span>
### Step 1: Create a detection category

Create a detection category for carrying custom capabilities, such as `FinancialCompliance` or `CodeSecurity`.

<span id="c298ee80"></span>
### Step 2: Create a custom capability

Create a custom watch list or custom model based on your business objective, and associate it with the corresponding detection category.


* When creating a custom watch list, configure entries, keyword combinations, or regular expressions, and associate them with a detection category.

* When creating a custom model, upload positive and negative samples, associate detection categories, and complete training, testing, and publishing.


<span id="2fc4f812"></span>
### Step 3: Create a custom detection rule


1. Select the target assets on which the custom detection rule will take effect.

2. Select a detection category associated with a custom capability.

3. Configure the execution action, such as **allow**, **block**, **safe response**, or **observe**.


<span id="837ccb1b"></span>
### Step 4: Verify the result


1. Send test content to the target asset through the SDK or actual business link.

2. Test content that should hit and should not hit separately.

3. Check whether the detection results are classified into the expected category.

4. Check whether the system executed the expected action.


<span id="b464ce99"></span>
## Related documents


* [Configure custom detection categories](https://docs.byteplus.com/docs/LLM-Application-Firewall/Configure_custom_detection_categories)

* [Configure custom models](https://docs.byteplus.com/configure-custom-model)

* [Test protection capabilities online](https://docs.byteplus.com/docs/LLM-Application-Firewall/Create_online_test_tasks)

* [Configure custom detection policies](https://docs.byteplus.com/docs/LLM-Application-Firewall/Configure_custom_detection_policies)

* [Configure custom watch lists](https://docs.byteplus.com/docs/LLM-Application-Firewall/Configure_custom_watch_lists)

* [Create a custom protection model to protect specific business](https://docs.byteplus.com/docs/LLM-Application-Firewall/Create_a_custom_protection_model_to_safeguard_specific_business_scenarios)
