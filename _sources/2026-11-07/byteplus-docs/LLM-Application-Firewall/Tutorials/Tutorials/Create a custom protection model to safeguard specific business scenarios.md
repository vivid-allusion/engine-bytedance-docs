---
title: "Create a custom protection model to safeguard specific business scenarios"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Create_a_custom_protection_model_to_safeguard_specific_business_scenarios"
---

To enhance security for your specific business needs, LLM Application Firewall allows you to create custom protection models. This guide provides step\-by\-step instructions on how to train, test, and deploy an exclusive protection model using your own sample data, ensuring it is tailored to your actual business scenarios.

<span id="5d77a4e1"></span>
## Scenario description

Suppose your business is a financial AI customer service assistant. Its main function is to answer users' common questions related to finance and securities applications, and to guide users toward rational investment, preventing non\-compliant Q&A (such as promising returns, recommending stocks in violation of regulations, and more). You can create a model specifically for detecting such illegal financial Q&A to improve the detection rate of related content.

The following steps describe operations related to this scenario.

<span id="47a0fd49"></span>
## Prerequisites

You have purchased an LLM Application Firewall **annual/monthly enterprise edition instance**.

<span id="e4b3c8d8"></span>
## Step 1 Create a detection category

Detection categories are used to identify the label type of content hits, helping to distinguish different content categories within the same rule. LLM Application Firewall provides some built\-in detection categories, which can be used to associate rules related to LLM protection. To create a custom protection model, you must first create a custom detection category.


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield/region:llm-shield+ap-southeast-1/).

2. Select the region where the instance is located in the top bar.

3. In the left menu bar, select **Protection** ** \> ** **Custom protection**.

4. Select the **Detection category** and click **Add detection category**.

5. Enter the category name and description.

   *  ** Category name ** : `Financial_Inquiry_Detection`. It is recommended to use a name that accurately describes and summarizes the issue.

   * **Description**: Used to identify non\-compliant Q&A content in financial scenarios, such as guaranteed returns or stock recommendations.

6. Click **Confirm**.


<span id="75c52743"></span>
## Step 2 Create a protection model

After creating the detection category, you can proceed to configure the model. Because the model needs to be trained based on sufficient sample content, you must prepare the corresponding sample set in advance.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div>


<div data-tips="true" data-tips-type="warning">After the model is created, it will automatically be queued for training. This process is expected to take 1–2 hours and cannot be canceled once started. To avoid resource waste, please ensure that you configure the model information correctly when creating it.</div>



1. In the left menu bar, select **Custom model** tab and click  ** Add model ** .

2. Fill in the basic information for the model.

   *  ** Model name ** : `Financial_Inquiry_Detection`. The name can be consistent with the detection category, or you can choose a custom name that accurately summarizes the core scenario targeted by the protection model.

   *  ** Scenario description ** : `Used to detect Q&A content for a financial customer service assistant to ensure it answers common questions about finance and securities applications, guides users toward rational investment, and prevents non-compliant Q&A, for example, promising returns, recommending stocks in violation of regulations, and more`.

3. Click **Download template**.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/37588e1b0b984ebaaa9eaa64954924d8) </span>

4. Open the template and fill in the training sample content as required.

   * Title: The theme of the sample content. It can be consistent with the detection category name (`Financial_Inquiry_Detection`), or you can choose a custom name that accurately summarizes the core theme of the sample content, such as recommending stocks in violation of regulations.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">Note      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">You can train a model with sample content from multiple different topics, with up to 10 sample topics supported per model.      </div>
      

   * IsWhite: Whether it is a positive sample.

      * TRUE: Positive sample. The model will determine it as compliant content.

      * FALSE: Negative sample. The model will determine it as non\-compliant content.

   * Content: The specific content of the sample.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">Caution      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Double quotes (”) cannot be parsed.      </div>
      

   The following is a sample for reference:

   
   |Sample type |Title |IsWhite |Content |
   |---|---|---|---|
   |Positive sample |Financial_Inquiry_Detection |TRUE |How to diversify investment risk? |
   |Negative sample |Financial_Inquiry_Detection |FALSE |Recommend a stock that is guaranteed to rise. |
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">\*Caution   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The effectiveness of the model depends on the quality and quantity of the samples you provide. To ensure the accuracy and effectiveness of the protection model, your sample set should meet the following criteria:   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Close to real scenarios</strong>: Samples should originate from your actual business data and cover various typical questions and edge cases.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Balanced positive and negative samples</strong>: Each category requires at least 20 positive samples (compliant content) and 20 negative samples (non\-compliant content).   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Positive samples are more important than negative samples</strong>: To reduce false positives, it is recommended that the number of high\-quality, diverse positive samples (normal business conversations) exceed that of negative samples.   </div>
   

5. Upload the configured training set to the console.

   The platform will automatically parse the relevant data and determine whether the training set you uploaded meets the requirements. Please adjust the training set according to the parsing results to ensure it meets the standards for model training.

6. After parsing is complete, associate the sample content with the detection category and fill in the relevant description.

   * **Title**: The theme of the sample content is automatically extracted by the platform.

   * **Detection category**: Select  the category you have created in **Step 1**(`Financial_Inquiry_Detection`).

   * **Description**: Questions or answers involving illegal fundraising, money laundering, financial fraud, fraudulent business schemes, and other illegal financial activities.

7. Click **Confirm**.


<span id="9392d2cc"></span>
## Step 3 Train the model (automatically triggered)

After the model is created, it will automatically enter the training queue. The training process is expected to take 1 to 2 hours and cannot be canceled once started. Please wait patiently.

After the model training is complete, it will transition to the  ** Not deployed **  status.

<span id="87638dd3"></span>
## Step 4 Deploy the model

After the model training is complete, you need to deploy the model to the LLM Application Firewall service for subsequent testing and usage.


1. In the custom model list, locate the created model.

2. Click **Deploy** in the Actions column and confirm. The LLM Application Firewall will automatically begin deploying your custom model.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/95e7eb5376df46958af490fefa744809) </span>

   After the model deployment is complete, it will transition to the **Pending publication** status.


<span id="a542519f"></span>
## Step 5 Test the model performance

Before the model goes live, it is recommended to test the protection performance to verify whether the model can accurately identify the target risks and ensure that normal business operations are not adversely affected. You can perform performance validation in the following two ways:


* Online testing: Suitable for scenarios requiring small\-batch, rapid validation. You can quickly create test content and obtain validation results.

* Canary testing: Simulates real online traffic for testing, providing a more comprehensive assessment of the model's performance in actual environments.


<span id="460cf93a"></span>
### Online testing

Online testing refers to directly entering the content to be checked in the console, allowing the deployed model to determine compliance. This method enables rapid retrieval of detection results.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div>



* <div data-tips="true" data-tips-type="warning">A maximum of 100 tasks can exist simultaneously, including both executed and unexecuted tasks.</div>


* <div data-tips="true" data-tips-type="warning">Each task can contain up to 100 test items.</div>


* <div data-tips="true" data-tips-type="warning">Each test item can contain up to 4096 bytes.</div>


1. In the custom model list, locate the created model.

2. Click  ** Test & Publish **  in the Actions column.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/2fff3cf0306f4ad89eb3e0f432b8b4f1) </span>

3. Select **Online testing** and click **OK**.

4. Select the model and enter the content to be tested.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/0da4df73b6b14657bf2460e4f78831c0) </span>

5. Click **Run**.

6. Click **View results** and refresh the webpage to check the result.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/e0dcbde4342f4d5fa13112925d439132) </span>


<span id="339d3e84"></span>
### Canary testing

Canary testing configures protection rules consistent with those used in production, associates detection categories with specific protected assets, and utilizes real online traffic to verify the model's actual performance.


1. In the custom model list, locate the created model.

2. Click  ** Test & Publish **  in the Actions column.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/2fff3cf0306f4ad89eb3e0f432b8b4f1) </span>

3. Select **Canary testing** and click **OK**.

4. Configure rule parameters.

   * **Rule name**: Enter the corresponding name to distinguish different rules.

   * **Asset**: Select the assets to be used for protection performance testing. It is recommended to use **test assets**.

   * **Effective mode**: Check **Take effect on both input and output**.

   * **Detection category**: Select **`Test category`**` > `**`Financial_Inquiry_Detection`**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If your model has not been deployed, you cannot select the corresponding detection category when adding rules.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/3d858142bfb4468c943f123d0f5ba8e6) </span>

   * **Action**: Configure as **Observe**.

5. Click **OK**.

6. After actual data requests are made online, filter the attack logs by the test detection category to check for unexpected hits (false positives) or misses (false negatives).

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/66ff89b0a56347a1923b580780971967) </span>

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Both of these methods can help you test the model's effectiveness. If the test results do not meet expectations, you need to adjust the sample set content and recreate the protection model; if the results meet expectations, you can directly publish the model.   </div>
   

<span id="e8027392"></span>
## Step 6 Publish the model

After confirming that the model's performance meets expectations, you can publish the model. Only after publishing will the detection categories associated with the model take effect in the protection rules.


1. In the custom model list, select the model to be published.

2. Click  ** Test & Publish **  in the Actions column.

3. Select **Publish directly** and click **OK**.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/9db6efd311524636aee16fb160abf58f) </span>

   After publishing is complete, the model transitions to the **Published** status.


<span id="7fe9b1b3"></span>
## Step 7 Configure custom rules

Rules are used to associate detection capabilities with actual protected assets, so you need to create a rule to associate the `Illegal financial Q&A` category with the target asset.


1. Select the  ** Custom detection rule **  tab and click **Add rule**.

2. Configure the relevant rule parameters.

   * **Rule name**: Enter the corresponding name to distinguish different rules.

   * **Asset**: Select the assets that you want to protect.

   * **Detection category**: Select **`Official category`**` > Illegal financial Q&A`.

   * **Action**: Configure as **Block**.

3. Click **Confirm**.


After your custom rule takes effect, the system will detect illegal financial Q&A on the associated assets according to the configured rule. If any violations are found, the system will block the request in accordance with the `Block` action. It is recommended to regularly review the protection logs to understand rule execution and identify any anomalies.

<span id="4705d6a7"></span>
## FAQs about custom models

<span id="9884e4be"></span>
### How to replace existing model capabilities?

The LLM Application Firewall supports seamless replacement of the current model without changing existing rule configurations, such as asset associations and detection categories. To update or replace sample content, create a new model, associate it with the original detection category, and use test assets for canary testing. Once the test results meet expectations, directly publish the model to complete the switch. The main steps are as follows:


1. **Create**: Create a new protection model.

   1. Upload a new sample set.

   2. Associate the original detection category with the new sample content.

2. **Deploy**: After the model is automatically trained, deploy the model.

3. **Test**: After deployment is complete, use test assets for canary testing to verify the effectiveness of the new model.

4. **Publish**: After confirming that the model meets your expectations, publish it.

5. **Decommission the original model**: Unpublish the original model to ensure your protected assets are safeguarded by the new model.


<span id="5d3a03f5"></span>
### How to expand existing model capabilities

To add new detection capabilities based on existing detection categories (for example, adding the `IllegalStockRecommendation` category to the `PromisedReturns` category), refer to the creation process, prepare relevant sample data, and deploy a new model.

<span id="c447a1fc"></span>
### How to conduct canary testing?

Before fully applying custom model capabilities to the production environment, it is crucial to conduct small\-scale canary testing. The recommended steps for canary testing are as follows:


1. **Create test assets**: Create a test asset to verify the effectiveness of the model's detection and rule configurations.

2. **Enable observation mode**: Before publishing the custom model, associate the test asset with the detection category you are testing and configure the action as "Observe".

3. **Collect and analyze logs**: After running for a period of time (for example, 1–3 days), carefully review all matched requests in the "attack logs." Pay special attention to those "false positive" logs that you believe are part of normal business operations.

4. **Policy tuning**:

   * If false positives are present, analyze the causes. This may be due to overly broad sample content or the need for more detailed allowlist samples.

   * If false negatives occur (known attacks are not detected), first confirm that all relevant rules are enabled, then further verify whether the blocklist sample content is sufficiently comprehensive.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/db8d9ed6692b4e04ba8322ac17b750c0) </span>

5. **Switch to block/secure reply mode**: When the false positive rate drops to an acceptable level, change the execution action and gradually expand the scope of assets affected by the policy until full coverage is achieved.
