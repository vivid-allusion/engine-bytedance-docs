---
title: "Configure custom detection rules"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Configure_custom_detection_policies"
---

Custom detection rules are used to associate detection categories with assets and actions. They define which assets a custom watch list, custom model takes effect on, and how to handle content after a hit. A custom capability takes effect on target assets only after you associate it with a detection category and configure custom detection rules.

This topic describes how to create, verify, and manage custom detection rules.

<span id="use-cases"></span>
## Use cases

You can configure custom detection rules in the following scenarios:


* Apply a custom watch list to specified assets to allow allowlist content, or observe or block blocklist content.

* Associate a deployed custom model with test assets to verify model detection results in grayscale.

* Apply a published custom model to production assets to identify risky content in specific business scenarios.


<span id="prerequisites"></span>
## Prerequisites


* The businesses that need protection have been connected to the LLM Application Firewall. Connection methods and supported detection directions may vary by asset. For more information, see [Introduction to assets integration](https://docs.byteplus.com/docs/LLM-Application-Firewall/introduction_to_assets_integration).

* Detection categories have been created, and the custom capabilities that need to be used have been associated with the categories:

   * When using a custom model, deploy the model before grayscale testing. Publish the model before production launch.

   * When using a custom watch list, complete the corresponding configuration and enable the rule switch.

* The assets, content types, detection directions, and actions after content hits have been defined.


For related configurations, see [Configure custom detection categories](https://docs.byteplus.com/docs/LLM-Application-Firewall/Configure_custom_detection_categories), [Configure custom models](https://docs.byteplus.com/docs/LLM-Application-Firewall/Configure_custom_models), [Configure custom watch lists](https://docs.byteplus.com/docs/LLM-Application-Firewall/Configure_custom_watch_lists).

<span id="configuration-description"></span>
## Configuration description

<span id="actions"></span>
### Actions

&nbsp;


|Action |Description |
|---|---|
|Allow |The content continues to flow after it hits the rule. This applies to content that is explicitly allowed to pass, such as a custom watch list allowlist. |
|Block |The request is blocked after the content hits the rule. If a custom block response policy is configured for the asset, users receive the configured response content. |
|Safe response |Replace the original LLM response with secure and compliant content. Safe response applies only to assets connected through SDKs. |
|Observe |Record hits without blocking requests. This applies to rule grayscale, effect evaluation, and false positive troubleshooting. |


When a request hits multiple custom detection rules associated with the same asset, the system executes them in the order of `Allow > Block > Security reply > Observe`. Custom allow rules have the highest priority. If a request does not hit a custom allow rule but hits a custom block rule, the request is blocked. For the complete decision logic when other protection policies are also hit, see [Introduction to protection policies](https://docs.byteplus.com/docs/LLM-Application-Firewall/introduction_to_protection_policy).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div>


<div data-tips="true" data-tips-type="warning">Allow rules override the actions of other protection policies. Before you configure allow rules, strictly limit the assets, content types, and detection categories, and fully verify the impact scope.</div>


<span id="effective-conditions"></span>
### Effective conditions

A rule participates in detection only when all of the following conditions are met:


1. The global **Custom detection rules** switch at the top of the page is enabled.

2. The **Rule switch** of the current rule is enabled.

3. The request passes through an asset associated with the rule.

4. The request content type is within the scope configured for the rule.

5. The corresponding model input or model output detection category is configured for the request direction.

6. The custom capability associated with the detection category is available. When using a custom model, the model corresponding to the test category must be deployed, and the model corresponding to the official category must be published.


For example, if a rule is bound only to asset A, the content type is set to **Text**, and only the **Model output** category is configured, the rule does not detect asset B, document content, or model input content.

<span id="procedure"></span>
## Procedure


1. Log on to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield).

2. In the top navigation bar, select the region to which the instance belongs.

3. In the left navigation pane, choose **Protection \> Custom protection \> Custom detection rule**.

4. Enable the **Custom detection rule** switch at the top of the page. The rule list supports querying rules by rule name or rule ID, and displays the assets, content types, detection categories, actions, and enabled status associated with each rule.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/28a6f7d36d4c46469df886ff8f750254~tplv-goo7wpa0wc-topic.webp) </span>

5. Click **Add rule**.

6. Configure the basic information and effective conditions of the rule.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72953537de974551a5812cdfbfca4ba5~tplv-goo7wpa0wc-topic.webp) </span>

&nbsp;

   
   |Configuration item |Description |
   |---|---|
   |Rule name |Enter a name used to distinguish the rule. We recommend that the name reflect the business, detection direction, and action. |
   |Asset |Select the assets that the rule needs to protect. For grayscale testing, we recommend selecting test assets. For production launch, select actual business assets. |
   |Content type |Select **All types**, or select **Specific types** and then select **Text** and **Document** as needed. |
   |Effective method |If model input and model output need to use the same detection category, select **Synchronize input and output detection**, and then configure a unified detection category. If you only detect one direction, or if input and output need to use different detection categories, do not select this option, and configure **Model input** and **Model output** separately. Configure at least one of input and output. |
   |Detection category |Select a category associated with a custom watch list, custom model. For custom model grayscale testing, select **Test category**. When the model is published and used for production assets, select **Official category**.<br><br><br>* **Test category**: Used for grayscale testing before a custom model is published. Select the test category corresponding to the deployed model.<br><br>* **Official category**: Used for officially published models and production assets. Select the official category corresponding to the published model.<br><br>* **Model input**: Detects content sent to the model.<br><br>* **Model output**: Detects content generated by the model. |
   |Action |Set the handling method after content hits the category. For more information, see [Actions](https://docs.byteplus.com/en/docs/313/90815#actions). |
   |Rule switch |After it is enabled, the rule enters the enabled state after being saved. After it is disabled, only the configuration is saved, and the rule does not participate in detection. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you select multiple assets, make sure that these assets support the content types and detection directions set in the rule.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The same asset can be associated with multiple rules. Before configuration, we recommend checking existing rules to avoid action conflicts.   </div>
   

7. After confirming that the configuration is correct, click **OK**.


<span id="verify-rule"></span>
## Verify the rule effect

After a rule is created, we recommend verifying it in a small scope before using it for production business.


1. When testing a custom model in grayscale, select **Test asset**, **Test category**, and the **Observe** action.

2. Prepare the following test samples:

   * Positive samples that should hit the category.

   * Normal samples that should not hit.

3. Submit content to the asset associated with the rule through an SDK, online testing, or the actual business link for inspection. For bidirectional detection rules, verify model input and model output separately.

4. In the detection results or protection logs, confirm whether the hit category, action, and business performance meet expectations.

5. Adjust the custom capability or rule based on false positives and false negatives. After the model detection effect meets expectations, publish the model and create or adjust the rule, and select **Official category** and production assets.

6. You can continue to use the **Observe** action during the initial production launch. After you confirm stability, adjust the action to **Block** or **Safe response** based on risk requirements.


For online verification methods, see [Test protection capabilities online](https://docs.byteplus.com/docs/LLM-Application-Firewall/Configure_custom_detection_policies).

<span id="manage-rules"></span>
## Manage rules

In the custom detection rule list, you can perform the following operations:


* **Query**: Search for rules by rule name, rule ID, or advanced filter conditions.

* **View**: Expand a rule row to view rule details.

* **Edit**: Modify the assets, content types, detection categories, actions, or switches of a rule.

* **Enable or disable**: Use the rule switch to control whether the rule participates in detection. Disabling a rule does not delete its configuration.

* **Delete**: Delete rules that are no longer used. After deletion, the rule no longer takes effect on associated assets.


<span id="faq"></span>
## FAQ

<span id="rule-not-effective"></span>
### Why does the rule not take effect after creation?

Check the following configurations in sequence:


1. Whether both the custom detection rules global switch and the current rule switch are enabled.

2. Whether the request passes through an asset associated with the rule.

3. Whether the request content type and detection direction are within the rule scope.

4. Whether the correct detection category is selected for model input or model output.

5. Whether the detection category is associated with an enabled custom watch list, custom model.

6. Whether the custom model is in the correct phase: grayscale testing uses the test category of a deployed model, and production protection uses the official category of a published model.

7. Whether the same asset hits another custom rule with a higher priority.


<span id="single-direction"></span>
### Can I detect only model input or model output?

Yes. Do not select **Synchronize input and output detection**. Select a category only for the direction that needs detection. Configure at least one of model input and model output.

<span id="unexpected-action"></span>
### Why is the final action inconsistent with the current rule configuration?

The same request may hit multiple rules. Check all custom detection rules and other protection policies associated with the asset, and determine the final action based on the priority in [Actions](https://docs.byteplus.com/en/docs/313/90815#actions).

<span id="confirm-change"></span>
### How do I confirm the result after modifying or disabling a rule?

Return to the rule list to confirm that the status has been updated, and then use test samples to verify the actual effect. When production rules are significantly adjusted, we recommend verifying them first on test assets or within a small traffic scope.

<span id="related-docs"></span>
## Related documents


* [Custom protection description](https://docs.byteplus.com/docs/LLM-Application-Firewall/Introduction_to_custom_protection)

* [Configure custom detection categories](https://docs.byteplus.com/docs/LLM-Application-Firewall/Configure_custom_detection_categories)

* [Configure custom models](https://docs.byteplus.com/configure-custom-model)

* [Test protection capabilities online](https://docs.byteplus.com/docs/LLM-Application-Firewall/Create_online_test_tasks)

* [Configure custom watch lists](https://docs.byteplus.com/docs/LLM-Application-Firewall/Configure_custom_watch_lists)
