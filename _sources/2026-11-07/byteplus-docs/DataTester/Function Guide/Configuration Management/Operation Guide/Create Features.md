---
title: "Create Features"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Create-Features"
---

<span id="一、功能简介"></span>
# Introduction to functions

If there are new features/policies that need to be changed frequently, they can be created as a feature for dynamic configuration, interface management, and updates.

Example: For example, product coupon combing, APP login method, these functions or policies can be updated on the interface by creating a Feature configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c6f7227bd8eb44589b8b75b7a9300199~tplv-goo7wpa0wc-image.image) </span>

<span id="二、如何使用"></span>
# How to use


* **Operation entrance:**  Feature list, click "+ Create Feature".

* To create a Feature, you need to fill in the following information: basic information, applicable APP, custom variables, setting variants, publishing audience

* After the feature is created or changed, it needs to be published before it will take effect online. If you need to publish it, please refer to it [Publishing Features](https://docs.byteplus.com/docs/DataTester/Publishing-Features).


**1. Fill in the basic information**

That is, the name, key and other basic description information of the Feature, which is designed to convey what function or strategy the Feature represents

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f0269168234944cdbaf6bd0cda8645be~tplv-goo7wpa0wc-image.image) </span>


* **Key name:**  Key is the core key value of the feature, which will be embedded in the code after filling it out. Specification: The key value is globally unique, supports English characters, numbers, and underscores, with a maximum of 200 characters. Once created, modification and editing are not allowed. Example: app_login_type.

* **Feature name:**  It is recommended to take the name related to the policy, so that others can quickly get the corresponding policy online. Specification: The name is globally unique, supports Chinese and English characters, numbers, and underscores, with a maximum of 100 characters (no special symbols can be included). Example: APP login method.

* **Feature Description:**  A description of a feature. Specification: Support Chinese and English characters, numbers, underscores, the longest no more than 2048 characters, example: This is the APP login feature.

* **Owners:**  The default creator is Owner, and others can be added as Owners to facilitate collaborative operation.

* **Upload image:**  You can click on the image location to upload Feature image or page screenshot, which is convenient for quickly identifying the difference of Feature.

* **Labels:**  You can customize labels, mainly used for classification and search queries, to facilitate feature management, such as user performance optimization strategies can be unified with "performance optimization" labels; support adding multiple labels. It is recommended to select existing tags or add new tags for easy management (up to 10 are supported, each within 20 characters).


**2. Set the variant**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e38928ec07904c36a29daf2e30e1f47d~tplv-goo7wpa0wc-image.image) </span>


* Variant is the value of the Feature (value)

* Type: support boolean, string, number and json four types (json type supports multi\-level nesting)

* Variant value:

   * Boolean: contains two variants True and False by default, and a description can be added

   * String: string format

   * Number: Support integer ten, decimal five

   * JSON: The JSON type supports multi\-layer nesting, please fill in according to the JSON specification

* You can create ≥ 1 variant, and fill in the corresponding parameter values and descriptions according to the type of variant value

* Example: If Feature is APP login method, the variant can be 1: QQ login, 2: WeChat login, 3: Douyin login


**3. Publish audience**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e82599fee284061be1e0f650ed70436~tplv-goo7wpa0wc-image.image) </span>


* The publishing audience sets the effective rules for the Feature, that is, what rules will take effect according to the final delivery, including: which APP will take effect, and which variant will take effect

* Audience rules: If you need to set different conditions to publish different variants, you can set them in the audience rules; they will take effect according to the top\-down logic, and users who miss the rule will take effect. Final default rules

   * Custom Audience Rules:

      * Filter conditions: Multiple filter conditions can be added to audience rules, and the relationship between multiple conditions is "and"

         * Note: If the existing filter conditions do not meet the requirements, you can enter the filter conditions management to customize the filter conditions

      * Release range: You can choose the release range "a variant, multiple variants, and no parameter value" (where multiple variants refer to multiple variants that can be randomly released in proportion). After selecting a variant or variant, you can set the flow ratio.

      * Add audience rules: You can add multiple sets of audience rules, each with a relationship of "or", and judge from top to bottom. For example, when a request hits the first custom rule, there is no need to judge subsequent rules

   * Default Final Rule: Users who miss the "Audience Whitelist" and "Custom Audience Rules" will automatically publish the final rule.

      * Select one of the variants: For example, if there are 3 variants, the default final rule can be one of variant 1, variant 2, or variant 3.

      * Parameter values are not issued: Variant values are not issued, effective local default values.
