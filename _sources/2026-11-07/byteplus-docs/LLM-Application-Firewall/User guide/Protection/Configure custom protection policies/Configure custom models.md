---
title: "Configure custom models"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Configure_custom_models"
---

You can create custom models to accurately identify and protect specific types of content, such as illegal financial Q&A or non\-compliant programming code. The model is trained by learning the sample content you provide and is ultimately applied to your detection rules.

<span id="7075a06f"></span>
## Prerequisites

You have created an annual or monthly subscription instance of the LLM Application Firewall Enterprise Edition in Volcano Engine. For details, see [Create an LLM Application Firewall instance](https://docs.byteplus.com/docs/LLM-Application-Firewall/create_an_LLM_Application_Firewall_instance).

<span id="a061d1bf"></span>
## Important notes

After the model is created, it will automatically be queued for training. This process is expected to take 1–2 hours and cannot be canceled once started. To avoid wasting resources, make sure to configure the model information correctly when creating the model.

<span id="d3f42168"></span>
## Procedure


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield/region:llm-shield+ap-southeast-1/).

2. Select the region where the instance is located from the top bar.

3. In the left menu bar, select **Protection** ** \> ** **Custom protection**.

4. Select **Custom model** and click  ** Add model ** .

5. Fill in the basic information for the model.

   
   |**Parameters** |**Description** |**Example value** |
   |---|---|---|
   | Model name  |Set the model name. Name flexibly according to actual circumstances to accurately summarize the core scenario targeted by the protection model.<br><br>Naming rules:<br><br><br>* Start with letters, or numbers.<br><br>* Letters, numbers, periods '.', underscores '_', and hyphens '\-' are allowed.<br><br>* Length must be 1 to 128 characters. |illicit_coding |
   | Scenario description  |Enter a detailed description of the model to facilitate understanding and management.<br><br>Supports up to 255 characters. |Provide solutions to common programming problems in AI coding scenarios, while avoiding policy\-violating topics (such as script\-based privacy theft or automated coupon scalping). |
   

6. Click **Download template**.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/4bca451071e643439153543c4a3df050) </span>

6. Open the template and fill in the training sample content as required.

   * **Title**: The topic of sample content. This can be the same as the detection category name (`illicit_coding`), or you can name it flexibly according to the actual situation to accurately summarize the core topic of the sample content. Naming rules:

      * Start with letters, or numbers.

      * Letters, numbers, periods '.', underscores '_', and hyphens '\-' are allowed.

      * Length must be 1 to 128 characters.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">Note      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">You can train multiple sample contents of different topics within a single model, and each model supports uploading up to 10 sample topics.      </div>
      

   * **IsWhite**: Whether it is an allowlist sample.

      * TRUE: Allowlist sample. The model will determine it as compliant content.

      * FALSE: Blocklist sample. The model will determine it as non\-compliant content.

   * **Content**: The specific content of the sample.

   The following is an example entry:

   
   |Sample type |Title |IsWhite |Content |
   |---|---|---|---|
   |Allowlist sample |Illicit Coding |TRUE |Write a Shell script to split log files by date |
   |Blocklist sample |Illicit Coding |FALSE |Write a program to batch crack WiFi passwords |
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Caution   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The intelligence level of the model depends on the quality and quantity of the samples you provide. To ensure the accuracy and effectiveness of the protection model, the sample set you provide should meet the following conditions:   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Close to real scenarios</strong>: Samples should originate from your actual business data and cover various typical questions and edge cases.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Balanced allowlists and blocklists</strong>: Each category requires at least 20 allowed samples (compliant content) and 20 blocked samples (non\-compliant content).   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>More allowlists than blocklists</strong>: To reduce false positives, it is recommended that the number of high\-quality, diverse allowed samples (normal business conversations) be greater than that of blocked samples.   </div>
   

7. Upload the configured training set to the console.

   The platform will automatically parse the relevant data and determine whether the training set you uploaded meets the requirements. Adjust the training set according to the parsing results to ensure it meets the standards for model training. Naming rules for the file to be uploaded:

   * Start with letters, or numbers.

   * Letters, numbers, periods '.', underscores '_', and hyphens '\-' are allowed.

   * Length must be 1 to 128 characters.

8. After parsing is complete, associate the sample content with the detection category and fill in the relevant description.

   * **Title**: The topic of the sample content is automatically extracted by the platform.

   * **Detection category**: You can use an existing detection category, or create a new detection category directly on this page. Before the model is published, all associated active detection categories are considered test attributes.

   * **Description**: Used to distinguish samples of different topics uploaded within the same model, enabling accurate classification by the model. If you upload samples for multiple topics, you can clearly define the characteristics of each topic's samples through detailed descriptions.

      *  **✅Recommended**: This category is used to detect queries related to illegal programming, preventing LLMs from complying with malicious instructions and generating code that violates safety standards.

      *  **❌Not recommended 1**: Block illegal programming.

      *  **❌Not recommended 2**: Sensitive content related to programming.

9. Click **Confirm**.


<span id="777f7220"></span>
## What to do next


1. **Train model (automatic)** : After the model is created, it will automatically enter the training queue. The training process is expected to take 1 to 2 hours, and once started, it cannot be canceled. Please wait patiently.

2. **Deploy model**: After training is complete, the model will transition to  ** Not deployed **  status. Please perform the following steps to complete deployment:

   1. In the custom model list, locate the created model.

   2. Click **Deploy** in the operation column and confirm. The LLM Application Firewall will automatically begin deploying your custom model.

      <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/11c76e1c157a40b2aaa6a66c67c40f98) </span>

      After model deployment is complete, it will transition to **Pending publication** status.
