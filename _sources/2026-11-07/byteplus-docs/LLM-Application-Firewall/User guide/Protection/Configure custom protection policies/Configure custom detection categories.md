---
title: "Configure custom detection categories"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Configure_custom_detection_categories"
---

Detection categories are used to identify the tag types triggered by content, helping to distinguish different content categories within the same rule. The LLM Application Firewall has preconfigured some detection categories, which can be directly used to associate protection rules. To create a custom protection model, you must first create a custom detection category. You can associate models, assets, and rules through custom detection categories to achieve more precise protection policy configuration.

<span id="b9d34d60"></span>
## Caution


* The name of a custom detection category must not duplicate any existing category.

* You can create up to 1,000 custom detection categories.

* Due to log storage and display requirements, deleted detection categories will still count against the quota.


<span id="144cc307"></span>
## Steps


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield/region:llm-shield+ap-southeast-1/).

2. Select the region of the instance in the top navigation bar.

3. In the left menu bar, select **Protection** ** \> ** **Custom protection**.

4. Select **Detection category** and click **Add detection category**.

5. Enter the category name and description.

   
   |**Parameter** |**Description** |**Example value** |
   |---|---|---|
   | Category name  |Set the name of the detection category. It is recommended to use a name that accurately describes and summarizes the category.<br><br>Naming rules:<br><br><br>* Must not duplicate any existing category.<br><br>* Must start with letters, or numbers.<br><br>* Only letters, numbers, periods '.', underscores '_', and hyphens '\-' are allowed.<br><br>* Length must be 1 to 128 characters. |illicit_coding |
   |Description |Enter a detailed description for this category to facilitate understanding and management.<br><br>Supports up to 255 characters. |This category is used to detect queries related to illegal programming, preventing LLMs from complying with malicious instructions and generating code that violates safety standards. |
   

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/f467ad8decdd4627b3716cf4d1793b48) </span>

6. Click **Confirm**.

   After completing the operation, you will see the newly created category in the detection category list.
