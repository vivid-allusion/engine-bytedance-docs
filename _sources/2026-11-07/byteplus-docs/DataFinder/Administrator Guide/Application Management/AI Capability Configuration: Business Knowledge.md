---
title: "AI Capability Configuration: Business Knowledge"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/AI_Capability_Configuration_Business_Knowledge_"
---

DataFinder Intelligent Analytics Assistant provides you with intelligent Q & A capabilities, allowing you to ask for business knowledge directly in the conversation window of the intelligent assistant. Intelligent Q & A provides you with a default knowledge base, and you can also upload local knowledge to DataFinder as a custom business knowledge base for Intelligent Q & A. This article shows you how to create and manage custom business knowledge.

<span id="cf13292f"></span>
# Create custom business knowledge


1. Log in and enter the DataFinder console, click **Application Management** \> **AI Capability Configuration** \> **Business Knowledge** in the top navigation bar, enter the business knowledge page and click the **Create Business Knowledge** button, and then configure custom business knowledge parameters in the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5b36137550f4076b8125a6c107aa89d~tplv-goo7wpa0wc-image.image) </span>

2. Basic information for configuring custom knowledge.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9807f19a2592406196e4e64b62528019~tplv-goo7wpa0wc-image.image) </span>

   * Set the knowledge domain name and description according to the interface prompts, and select the avatar of the knowledge base.

   * You can also find and add a project member as an administrator of knowledge by entering a project member name in the **Add Administrator** configuration field.

3. Click the **Knowledge** tab at the top of the configuration page to upload and associate knowledge.

   1. Click the **Upload Knowledge** button, upload local knowledge according to the interface prompts, and click **OK** when done.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d63e5ec8114ef496c7d290e48c9851~tplv-goo7wpa0wc-image.image) </span>

      The current supported upload knowledge file formats are: PDF, DOC, DOCX, CSV, TXT and other formats, and a single file cannot exceed 100M.

   2. Click **Associated Knowledge** , select the knowledge file that needs to be associated in the currently created knowledge in the pop\-up window, and when the subsequent intelligent Q & A makes an intelligent reply based on this knowledge, it will query the knowledge associated here and the default knowledge base provided by DataFinder as the analysis basis for the answer.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/351600a42058426586197e6aab6d9efb~tplv-goo7wpa0wc-image.image) </span>

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cc8f658deaaa46ea96dd38061485dfb9~tplv-goo7wpa0wc-image.image) </span>

4. Click the **Conversation Settings** tab at the top of the configuration page to configure the initial question for Smart Q & A.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/946271266f1c492caf74d7c20aaf8b08~tplv-goo7wpa0wc-image.image) </span>

   * You can set the most frequently consulted questions in the current knowledge domain scenario as the initial questions. After setting, when the intelligent assistant is called for intelligent Q & A later, the interface will directly display the initial questions set here to improve the efficiency of intelligent Q & A.

   * Currently, up to three initial questions are supported.

5. After creating the custom knowledge, click the **Publish** button in the upper right corner. After publishing, you can use the created knowledge to answer questions in the Intelligent Analytics Assistant.


<span id="2a850866"></span>
# Use custom business knowledge


* You can find the Smart Assistant button in the left sidebar of any page of the DataFinder console, and click to evoke the Smart Assistant sidebar. You can directly ask for business knowledge in the conversation window of the Smart Assistant.

* You can switch the knowledge base used for business consultation on the page of the intelligent assistant (when selecting a custom knowledge base, the actual knowledge base content range is "Custom Knowledge Base" + "Default Knowledge Base Provided by DataFinder").


<span id="c8e4c25c"></span>
# Edit and delete custom business knowledge

In the business knowledge page:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/59b2dc92ea0e46d1ad20b05c80cefca8~tplv-goo7wpa0wc-image.image) </span>


* Click on the created knowledge to enter the knowledge editing page, where you can make edits to the knowledge, similar to creating a custom business knowledge described above.

* Click the Delete button in the lower right corner of the created knowledge base to delete the created knowledge.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Only the creators and administrators of the knowledge have the authority to edit or delete the knowledge.</div>


* <div data-tips="true" data-tips-type="warning">After deleting it, you will no longer be able to answer questions based on this knowledge in the smart assistant. Please proceed with caution.</div>
