---
title: "Unstructured Data Processing Operators Configuration"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Unstructured_Data_Processing_Operators_Configuration"
---

Unstructured data processing operators are functional modules for processing unstructured data (such as text, images, audio, etc.). For example, the REST API operator can convert audio data into text, and the Volcano Ark large model operator will call the large model of the OpenAPI protocol on the platform for intelligent marking. This article introduces how to configure common operators for unstructured data processing.

<span id="2e07da36"></span>
# Explain

After adding a data connection, you need to add an unstructured data processing operator to process the data. VeCDP supports the following unstructured data processing operators:


* **REST API 2.0 call** : call external plug\-ins (ASR/OCR, etc.), use the output data of the upstream node as the imported parameter of the API, and query the data for data completion.

* **Volcano Ark large model** : docking Volcano Engine large model service, through custom model configuration, generation strategy and role person, to achieve unstructured data analysis.


<span id="9b347048"></span>
# Prerequisite


* [Data Preparation](https://docs.byteplus.com/docs/dataagent/Data_Preparation)

* [Task Creation](https://docs.byteplus.com/docs/dataagent/Task_Creation_)


<span id="5908b07f"></span>
# REST API operator

If your unstructured dataset contains audio data that has not been converted to text, you need to call the ASR capability through the REST API operator to convert it to text. The current REST API operator feature is turned off by default, so if you need to use it, you need to contact the Volcano Engine account manager to manually enable the REST API operator. For detailed usage of this operator, see [Rest API 2.0](https://docs.byteplus.com/docs/dataagent/Rest_API_2_0).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When preparing data, it is currently recommended that you convert the audio & video file to text first and then access the VeCDP dataset. It is not recommended that you directly access the audio & video file directly to VeCDP and then use the data processing operator to operate. See the specific operation <a href="https://docs.byteplus.com/docs/dataagent/Data_Preparation">Data Preparation</a>.</div>



1. Click on the left **operator** , drop down and select **Special Color Zone Operator \> REST API 2.0 Call** , and pull it into the right panel...

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3c4657d6f6bc43219610dab1bb7f7c6d~tplv-goo7wpa0wc-image.image) </span>

2. Configure ASR task parameters. For a detailed description of parameter configuration, see [REST API 2.0 ](https://www.volcengine.com/docs/6356/1277545?lang=zh).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c5754627544849a3bfee064fda49be28~tplv-goo7wpa0wc-image.image) </span>

3. Click **Data Preview** to preview the processing results.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24bd79736a2240c9b51a976f193803cb~tplv-goo7wpa0wc-image.image) </span>


<span id="8b3306a8"></span>
# **Volcano Ark Large Model Operator**

After introducing the dataset, you can introduce large model operators downstream of the dataset to intelligently label the connected data. For detailed use of this operator, please refer to the [Volcano Ark Large Model ](https://www.volcengine.com/docs/6356/1852857?lang=zh).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, only the Volcano Ark large model operator is supported. Connect to your Ark large model platform through the operator, and call the large model on the platform that supports the OpenAPI protocol for intelligent marking.</div>



1. Click on the left operator, drop down and select **Featured Area Operator \> Volcano Ark Large Model** , and pull it into the right panel.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/565b50d83dcd49c1ae64fab6823a2ff4~tplv-goo7wpa0wc-image.image) </span>

2. Click on the Ark big model operator that has been dragged into the task, click the "Customize Volcano Ark Model" button at the bottom of the task window, configure the access point of the Ark and the API key, and see the [Volcano Ark Large Model ](https://www.volcengine.com/docs/6356/1852857?lang=zh)for detailed parameter configuration instructions.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/915bde748186407e9dd95bb935f14422~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |explain |
   |---|---|
   |Inference access point |Configure the inference access point for your Ark large model platform, the general format is ep\-xxxxxxxxxx\-yyyy, please refer to the [Volcano Ark documentation ](https://www.volcengine.com/docs/82379/1099522)for the operation of the inference access point. |
   |API Key |Configure the API Key for your Ark big model OpenAPI call, the general format is xxxxxxxx\-yyyy\-xxxx\-yyyy\-xxxxxxxxxxxx, refer to the [Volcano Ark official website documentation ](https://www.volcengine.com/docs/82379/1263279)for the way to get it. |
   |Generative randomness |Temperature: Increasing the temperature will make the output of the model more diverse and innovative, while reducing the temperature will make the output content more compliant with the instruction requirements but less diverse. It is recommended not to adjust it at the same time as "Top p". |
   |Top P |Top p is the cumulative probability: When the model generates the output, it selects the words with the highest probability until the total probability of these words accumulates to the top p value. This allows the model to choose only these high\-probability words, thus controlling the diversity of the output. It is recommended not to adjust at the same time as "generating randomness". |
   

3. Configure the prompt word associated with the reply logic.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6de4585119c24ad391a55204b0f10069~tplv-goo7wpa0wc-image.image) </span>

   It needs to include the following four parts:

   * Role definition: such as tag extraction expert.

   * Skill description: such as what label to extract.

   * Output format: as required by JSON format.

   * Other limitations: such as focusing on extraction tasks without divergence.

      The following is an example for reference only:

   ```Markdown
   # Role
   You are a precise and efficient chatbot for bank consumer loan customer service, 
   capable of quickly and accurately extracting corresponding tags from customer service 
   chat records, helping banks to gain a deeper understanding of customer needs and provide 
   more personalized services.
   
   ## Skills
   ### Skill 1：Analyze chat content and extract tags
   1. Carefully study customer service chat records to accurately understand the customer's expression intentions.
   2. Based on the customer's statement, determine the label to which their loan demand belongs：
       - Immediate processing: The customer clearly stated that they need to apply for a consumer loan immediately.
       - Recently considered：The customer has revealed plans to apply for a consumer loan in the near future.
       - No demand：The customer clearly expressed that there is currently no need to apply for a consumer loan.
   3. Based on the customer's statement, determine the label to which their (customerType) belongs：
       - Personal：Personal user.
       - Enterprise: Enterprise users.
       - Unknown: Unable to clearly determine customer type.
   4. Based on the customer's statement, determine the label to which their (focus) belongs：
       - Interest rate: Customers mainly inquire or discuss about loan interest rates.
       - Limit: The customer emphasized the situation related to the loan limit.
       - Repayment method: The customer shows interest in the repayment method.
       - Approval process: Customers are concerned about loan approval processes and related issues.
       - Other: The content that customers are concerned about does not belong to the clear categories mentioned above.
   5. Based on the customer's statement, determine the label to which their (loanUsage) belongs：
       - Daily consumption: The customer stated that the loan is mainly used for daily consumption.
       - Education expenditure: The client emphasizes that the loan is used for education related expenses.
       - Medical expenses: The customer mentioned that the loan is used for medical purposes.
       - Other uses: The loan purpose mentioned by the customer does not belong to the above category.
       - Not mentioned: The customer did not mention any information related to the purpose of the loan.
   6. Freely extract other valuable tags from chat records, such as customer preferences for loan terms, special requirements, etc. (output null if not available).
   
   Output content in JSON format, as shown in the following example：
   
   {
       "demand": "Recently considered",
       "customerType": "Personal",
       "focus": "limit",
       "loanUsage": "daily expenses",
       "otherValuableTags": null
   }
   
   If there is no matching label, null can be output.
   
   ## Restrictions
   -Only analyze customer service chat content, extract exact tags, and do not perform any other unrelated operations.
   -Strictly follow the established label classification for judgment, and do not create new label categories on your own.
   -It is essential to ensure the accuracy and objectivity of the analysis results.
   -The freely extracted tags must be truly valuable and relevant to customer needs or bank consumer loans.
   ```
   

4. Configure template variables with user input. After selecting the field column for unstructured data in "Upstream Fields" of "Template Variables", configure the rules for the variable in "User Input".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf988f6aa4884cdbb99fc6cb7798f403~tplv-goo7wpa0wc-image.image) </span>

   * Upstream field: Select the input field that needs to be labeled as the output of the large model. Use ${field name} to refer to the data in the upstream field, and use < ID \> to identify the input content type. For example, `${context} < text >`is used to refer to the data of the upstream content column and is of text type. The following logos are currently supported:

      
      |Type |logo |
      |---|---|
      |Text |`<text>` |
      |Picture |`<image>` |
      |Audio |`<audio>` |
      |Video |`<video>` |
      |Do not fill in the logo |The system default is `< text >` |
      

      After selecting an upstream field, ${field name} is used to refer to the data of the upstream field, for example, ${conversation content} is used to refer to the data of the upstream field "conversation content" column, for example:

      * When the upstream data set is text\-based outbound call conversation data and WeCom session data, the text data loaded upstream can be selected, that is, the conversation content column.

      * The upstream data set is the outbound call conversation data of the audio class. When processing with ASR, the processed text data, that is, the processed conversation content column, can be selected.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If the upstream field name is the same as the system variable, the value of the upstream field will be overwritten. Therefore, you need to avoid using fields with the same name as system variables.      </div>
      

      * User input: After selecting an upstream field, the selected upstream field is automatically used as a variable for user input. You can add examples of user input to debug the effect of large model extraction when different inputs are used. Input format: ${conversation content | example: xxxx}.

5. Click "Test Execution" at the bottom of the page, and the system will extract the label according to the field name entered by the user and give an example result.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e880589f2c46482189185f3a491c8a93~tplv-goo7wpa0wc-image.image) </span>

   You can set the field settings for the desired label according to the example.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/105ca5d0a3bd4339acdc10f8dc270ffe~tplv-goo7wpa0wc-image.image" width="2938px" />   </div>
   


<span id="15dbce95"></span>
# Next step

See [Processing Result Output Configuration](https://docs.byteplus.com/docs/dataagent/Processing_Result_Output_Configuration).
