---
title: "Interpretation of Outbound Telemarketing Data"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Interpretation_of_Outbound_Telemarketing_Data"
---

The daily operations of the e\-marketing team generate massive amounts of data (including call recordings, work order texts, chat records, etc.), making it difficult to effectively integrate multi\-dimensional data such as behavioral events and transaction orders, and customer insights are insufficient. This article introduces how to use the unstructured data marking function to extract structured labels from the massive data in the electronic pins.

<span id="74e0281b"></span>
# Background Introduction

<span id="ca488634"></span>
## Pain point


* Low data utilization rate: The massive data in the enterprise is fragmented, underutilized (the amount of existing data \> 100,000/month), there is no public domain data supplement, and it is impossible to pay attention to customer\-side business changes in real time.

* Customer identification accuracy is low: the number of customers is large, but the number of electronic sales agents is limited, making it difficult to identify high\-quality customers efficiently.

* Client Server experience is poor: only use the label to mark the customer, unable to match the plan and speech for the customer's current business situation.

* Marketing relies on experience: customer intent insights and product portfolio recommendations rely on experience, and the cost of learning and training for newcomers is high.


<span id="5ec01772"></span>
## Goal

Through AI technology (NLP, automatic speech recognition, etc.), it automatically analyzes the unstructured communication data between e\-mail sales and customers in call records, WeChat chat records, work order text, etc., and extracts key business labels (such as customer intentions, demand scenarios, industry pain points, cooperation obstacles, industry intelligence, preferences, etc.) into the label library to optimize the automatic construction of customer portraits, follow\-up strategy optimization, etc.

The following is the integrated complete table of the extracted label appeals, covering customer dimensions, information acquisition preferences, product dimensions, intelligence dimensions, supplementary dimensions, etc.:


|**Dimensional classification** |**Chinese label name** |**English label name** |**label definition** |**Label format requirements** |
|---|---|---|---|---|
|Customer dimension |Is it a business? |if_Company |Is it a corporate customer? |Enumeration value: Yes, clearly indicates "Yes"; No, clearly indicates "No"; < Unavailable, the customer indicates that it is inconvenient to inform, or refuses to inform |
||job level |decision_maker_level |The level of decision\-making power of customers in the enterprise |Enumeration value (requires NLP recognition): Decision maker: makes it clear that the final decision is made < Influencer: can be suggested but has no decision \- Actor: only responsible for docking |
||requirement scenario |core_demand_scene |Customer core business scenario description |Text array: ["Online acquisition", "Payment reconciliation"] |
||demand pain point |pain_point |Pain points clearly expressed by customers |Text arrays: ["High labor costs", "Data dispersion"] |
||Intentional degree |intention_level |Customer cooperation willingness intensity |Value: 0 \- 100 (probability value, sentiment analysis + keyword matching required) |
||urgency |urgency_level |Urgency of need resolution |Enumeration value (requires time keyword recognition): \- Urgent: contains words such as "immediately/immediately/this month must/as soon as possible" \- Medium: contains words such as "within the quarter/next month" \- Wait and see: contains words such as "look again/not in a hurry/next year" |
||budget range |budget_range |The budget range mentioned by the client |Text: "10 \- 200,000" (amount required for entity identification) |
||project phase |project_stage |The client's current project stage |Enumeration value: understanding stage; testing and selection stage; bidding stage; |
||Whether the decision maker |is_decision_maker |Directly confirm whether the customer has the authority to make purchasing decisions |Boolean: true/false (requires position + power statement recognition) |
||Communication style |communication_style |Customer communication style |Strong, easy\-going, etc |
||reach preference |contact_preference |reach preference |Text array: [WeChat, Feishu, phone, SMS] (requires media keyword recognition) |
||Communication time preference |contact_preference |The time period you want to contact (e.g. weekdays/weekends/lunch breaks) |The time period you want to contact (e.g. weekdays/weekends/lunch breaks) |
||Decision\-making style |decision_style |Basis for purchasing decisions (data\-driven, relationship\-driven, brand trust) |Basis for purchasing decisions (data\-driven, relationship\-driven, brand trust) |
||Risk appetite |risk_appetite |Risk\-taking attitude towards new technologies/collaborations |Risk\-taking attitude towards new technologies/collaborations |
||Core Focus |key_concern |Key factors repeatedly mentioned by customers |Text array: ["price", "implementation period"] (keyword frequency statistics are required) |
||willingness to try it out |trial_willingness |Interest in trying out XX products |Enumeration values (requires intent recognition): < br \> \- Strong: Proactively asking for a trial/asking for details < br \> \- General: Indicates "can be considered" < br \> \- Denied: Explicitly rejecting or shifting the topic |
||R & D team situation |dev_team_status |Customer technical team size and capabilities |Text: "20\-person team/familiar with API development" (entity identification required) |
||call method |integration_method |Customer preference for system integration (e.g. API/SDK/local deployment) |Text array: ["API", "SDK"] (technical term recognition required) |
|Product dimension |Follow the product |interested_product |XX product name actively consulted by customers |Text array: ["Intelligent customer service", "data analytics"] (product name needs to be unified) |
||Recommended products |recommended_product |Sell product names recommended to customers |Text array: ["Enterprise XXX", "BI Tools"] |
||Product Concerns |product_concern |Customer doubts about the product |Text array: ["High price", "Weak customization"] (requires negative emotion recognition) |
||product complaint |complaint_focus |Customer feedback on existing services/products is negative |Text: "Slower response than competitors" (requires comparative recognition) |
||Business comparison |competitor_comparison |The customer's attention dimension when comparing competing products |Text: "The price is higher than XXX" (requires competing entity + comparison word identification) |
||Competitive companies used |used_competitor |The name of the competitor currently used by the customer |Text array: ["XXX \- Intelligent Customer Service"], take the name of the competitor. If a competing product is used, the specific name is not given. |
|Intelligence dimension |Competitive product experience evaluation |competitor_eval |Customer satisfaction with competing products |Enumeration values (sentiment analysis required): < br \> \- Satisfied: Explicit praise/indicates renewal < br \> \- General: Neutral rating/no complaints < br \> \- Dissatisfied: Direct criticism/mention substitution |
||Competitive focus |competitor_focus |Key reasons why customers choose competing products |Text array: ["low price", "good service"] |
||churn risk |churn_risk |The possibility of customers interrupting cooperation |Value: 0 \- 100 (subject to frequency of complaints + contract expiration date) |
||Purchase potential |upsell_potential |The possibility for customers to purchase additional products |Enumeration values: high/medium/low (requires requirement correlation analysis) |
||Willingness to refer |referral_willingness |Customer's intention to recommend others to buy |Enumeration values: active mention/try/no intention (requires social intent recognition) |
|Supplementary dimension |Type of business opportunity |opportunity_type |Classification of business opportunities corresponding to demand scenarios |Text: "New Purchase" (requires business rule mapping) |
||decision timeline |decision_timeline |When the customer plans to make purchasing decisions |Date: "2025 \- Q3" (subject to physical extraction) |
||technical adaptation complexity |tech_complexity |The difficulty assessment of product integration in the customer's IT environment |Enumeration values: high/medium/low (requires technical stack analysis) |


<span id="92c948df"></span>
# Operation Steps

<span id="69d9b669"></span>
## Data connection

Create the call record as a data set of VeCDP, and access the data in VeCDP. For specific operation steps, please refer to [Common Data Source Access ](https://www.volcengine.com/docs/6356/130758?lang=zh)and [Data Entry ](https://www.volcengine.com/docs/6356/1222748?lang=zh).


1. Log in to the VeCDP console and select **Data Management \> Data Connections** .

2. In the upper left corner of the Data Connections directory, click **New Data Connection** and select **Local File \- Excel or CSV**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c67c8fc626534d51968c289f53ca0989~tplv-goo7wpa0wc-image.image) </span>

3. After clicking, locate the target Excel/CSV file in the local file and click Open. It supports uploading up to 5 files, and the total file size does not exceed 500M. It is recommended to choose no more than 10 sheets, otherwise the upload may fail.

4. When the loading is complete to 100%, you can select the contents of the sheet in the file. Click Next to **preview data** and set the **data connection name** . After the preview is completed, click **OK** to complete the data connection of Excel/CSV.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90283fba836e46a0b02aca6da02147f3~tplv-goo7wpa0wc-image.image) </span>


<span id="f9106243"></span>
## Create a visual modeling task


1. At the top of the **VeCDP console** select **Data Management \> Visual Modeling** .

2. Click **Task List** in the left navigation bar of the visual modeling page, enter the visual task list page and click **New \> New Offline Task** to start creating an offline type of visual modeling task.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b3ff938281d476b9d38addb70f92e75~tplv-goo7wpa0wc-image.image) </span>

3. At the top left of the New Task page, click ➕ **Add Data Connection** . Select the data connection you just created.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9380caad38ab41febeba8feb5385cfa8~tplv-goo7wpa0wc-image.image) </span>

4. Select the dataset of unstructured data to be marked and pull it from the left list into the right panel.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b00a42e205d5436e8724b979b4e7458c~tplv-goo7wpa0wc-image.image) </span>


<span id="05db2f50"></span>
## Configure data cleaning operator


1. Click the + sign on the dataset and select **Calculate Columns** .

   Calculate column operators, support custom expressions, use Spark functions to process upstream fields and add new fields. The configuration flow for computed columns clearly displays new fields in tabular form.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b37b90467d344aa28607d558059eccb8~tplv-goo7wpa0wc-image.image) </span>

2. Click **Add** , configure the calculated column name and expression, search in the common functions and double\-click the replace function to supplement the expression. Then click **OK**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e14daa43a7f44f1ea9bf0cd43788a484~tplv-goo7wpa0wc-image.image) </span>

3. Click **Data Preview** to view the data preview results and confirm the data cleaning results.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/96f63a47335a44a1a577be6d55ef380f~tplv-goo7wpa0wc-image.image) </span>

4. Click the + sign for the calculated column and select **Field Settings** .

   Support for selecting reserved fields, setting field types, setting field names, and setting field sorting.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6fc5ed9d98f4456ca7e82dd998e55c74~tplv-goo7wpa0wc-image.image) </span>

5. Fill in the target field name and field type of the field setting operator.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4dbbb7bf7faf45329f1f23008c4c7f92~tplv-goo7wpa0wc-image.image) </span>

```Plain Text
  | | | \
  |Target field name |Target field type |
  |---|---|
  | | | \
  |huihuaid |string |
  | | | \
  |conten |string |
  | | | \
  |content |string |
```


<span id="19a38236"></span>
## Configuring Volcano Ark Large Model Operator


1. Click the + sign in the field setting and select the **AI\-Large Model Processing \> Volcano Ark large model** operator.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4187d29371e408ab0242b4b4ac8cb07~tplv-goo7wpa0wc-image.image) </span>

2. Add 4 large model operators of Volcano Ark to extract content from different dimensions.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a9e88172fde24a02a83c6f3c5723722f~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the corresponding prompt word and user input. The user input is `${content}`.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d2e98ccaf4514842ae64cf44be23493d~tplv-goo7wpa0wc-image.image) </span>

   * **An example of a customer dimension cue word is as follows:** 

   ```Markdown
   Prompt optimization
   # Role
   You are a professional data label extraction expert. Based on the dialogue data provided by the client, you will strictly follow specific rules to accurately and quickly extract various information labels, and output them in JSON format.
   
   # Task Description and Requirements
   1.Basic Information
   (1)Extract the label indicating whether it is an enterprise (if_Company Label). Rule: Check if there are any customer identity related statements in the conversation. If it is clearly a corporate customer, output "Yes"; Clearly not, output 'no'; Not mentioned or inconvenient to inform, refused to inform, output 'unable to obtain, customer expresses inconvenience to inform, or refuses to inform'. Example: If the conversation mentions "We are XX company and would like to know more about our products", then extract if_Company: Yes.
   (2)Extract the labels for the position level (decision_maker_1evel Label). Rule: Identify the customer's decision level in the enterprise through dialogue, and output the enumeration values of "decision maker, influencer, and executor". If in a conversation, it is clearly stated that one has the final decision-making power, then it is judged as the decision-maker. If it needs to be discussed, it can be determined as the executor. Example: The customer says' I am responsible for making the final decision 'and extracts' decision_maker_1evel' as the decision-maker.
   (3)Extract the labels of the requirement scenario (core_demand_stene Label). Rule: Sort out the description of the customer's core business scenario and organize it into a text array. For example, if the dialogue says "To acquire customers online, product support is needed", extract core_demand_stene: ["Online customer acquisition"].
   (4)Extract labels for (pain points Label) in requirements. Rule: Capture the pain points clearly expressed by the customer, organize them into a text array, and extract pain_point: ["High labor cost", "Data dispersion difficult to handle"].
   (5)Extract tags for the level of intention (intention_1evel Label), using sentiment analysis and keyword matching to calculate probability values from 0 to 100; Or identify keywords (such as "immediately/immediately/necessary/as soon as possible" corresponding to "urgent", "quarter/next month" corresponding to "moderate", "look again/not urgent/next year" corresponding to "wait and see"), and output them according to enumeration values. Example 1: The customer says' we must cooperate as soon as possible ', extract intention_1evel: urgent; Example 2: Calculate the probability of 0.8 through sentiment analysis and extract intention_1evel: 80. Example 3: If the customer is willing to leave their contact information and inquire about product details, it represents a high level of intention. Extract intention_1evel: 90
   (6)Extract labels for urgency level(urgency_level Label). Rule: Identify time keywords, with "immediately/immediately/necessary/as soon as possible" corresponding to "urgent", "quarter/next month" corresponding to "moderate", and "wait and see" corresponding to "look again/not urgent/next year", and output according to enumeration values. Example: The customer says' I need it next month 'and extracts' urgency_level' as' medium '.
   (7)Extracting (budget_range) label rule: Identify the entity of the amount in the conversation and organize it into text output such as "100000 to 200000". Example: The customer says "budget is about 100000 to 200000", and the budget_range is "100000 to 200000".
   (8)Extract project stage (project_stage) rules: enumerate values according to "understanding stage; testing and selection stage; bidding stage;" and output them after judging from the dialogue. Example: The customer says' we are still in the initial stage of understanding your product ', and the extraction project stage is' understanding stage'.
   (9)Extract the (is_decision-maker) label, rule: identify based on position and power statement, with the decision-maker outputting 'true' instead of 'false'. Example: If the customer says "I am responsible for deciding whether to buy or not", extract is_decision-maker: true.
   (10)Tags for (communication_style) label. Rule: Use tone analysis, where "frequent interruption/imperative tone" corresponds to "dominant", "repeated confirmation/request for proof" corresponds to "cautious", "friendly agreement/less questioning" corresponds to "easy-going", and "data-driven/logical questioning" corresponds to "rational". Output according to enumeration values. If there are no emotional fluctuations, it corresponds to being 'easy-going'. Example: In a conversation, if the customer frequently interrupts and expresses themselves in a commanding manner, extract communication_style: dominant.
   2、Information acquisition preference category
   (11)Contact preference (contact_preference Label), rule: Identify the contact channel keywords mentioned in the conversation (WeChat, Feishu, phone, email, etc.), organize them into a text array output. Example: If the customer says "you can communicate with me by email, or WeChat can also be used", extract contact_preference: ["email", "WeChat"].
   (12)Communication time preference (contact_time_preference Label) rule: Extract the time period that the customer wishes to contact, such as "afternoon", "workday", etc., and output it as text. Example: The customer says "Contact me in the afternoon, don't disturb me on weekends", and extracts the preferred communication time: "Afternoon on weekdays".
   (13)Decision_style Label, rule: Based on the enumeration values of "data-driven, relationship oriented, brand trust", judge the output from the dialogue. Example: The customer says, 'Send me your ROI report and see the data before making a decision.' Extract Decision_style: data-driven.
   (14)(risk_appetite) Label, rule: Capture customers' descriptions of their attitudes towards the risks of new technology cooperation, organize them into a text array for output.
   Example: The customer says, 'We are willing to try new technologies and are not afraid of risks.' Extract risk.appetite: ['We are willing to try new technologies and are not afraid of risks'] (extract keywords based on actual situations).
   3.Others
   (15)Core focus point (key_comcern Label), rule: Count the key factors repeatedly mentioned by customers in the conversation, organize them into a text array output.
   Example: The customer repeatedly says "discounted price, comprehensive functionality", and extracts key_comcern: ["discounted price", "comprehensive functionality"].
   (16)(trial_willingness Label) Rule: Output according to the enumeration values of "Strong, Fair, Rejected". If you actively request a trial/inquire about details, it is judged as strong; if it is mentioned as worth considering, it is judged as average; if you explicitly refuse or change the topic, it is judged as refusal. Example: The customer says, 'Can you give us a try? I want to see the details.' Extract trialwillingness: strongly.
   (17)R&D team status (dev_team_status Label). Rule: Identify the entity description of the customer's technical team size and capabilities in the conversation, and organize it into text output. Example: The customer says' Our team consists of 20 people and is familiar with API development ', and extracts dev_team_status as' 20 person team/familiar with API development'.
   (18)(integration_method Label), rule: Identify the system integration method (API/SDK/local deployment, etc.) preferred by the customer and organize it into a text array for output. Example: The customer says "they want to integrate using API, or SDK is also available", and extracts integration_sthod: ["API", "SDK"].
   
   
   # Restrictions
   1. Label extraction must be strictly based on the given rules, and the rules must not be changed without authorization.
   2. For information not mentioned, output it as "no relevant information" to ensure proper formatting.
   3. The output content should be accurate, clear, and comply with the format and type specified by each label, without any data type errors or format confusion.  
   4. The output must be presented quickly and accurately in JSON format, with complete and correct JSON structure, and the output label values enclosed in quotation marks. The returned format is
   {
   "if_Company": "是", // Is it a company
   "decision_maker_level": "决策者", // Position level
   "core_demand_scene": "线下获客", // Requirement scenario
   "pain_point": "人工成本高", // Extract pain points from requirements
   "intention_level": "80", // degree of intention
   "urgency_level": "紧急", // Urgency level
   "budget_range": "10-20万", // budget range
   " project_stage": "了解阶段", // Project phase
   "is_decision_maker": "true", // Is him/her a decision maker
   "communication_style": "强势", // communication style
   "contact_preference": "微信", // contact channel preference
   "contact_time_preference": "工作日下午", // Communication time preference
   "decision_style": "数据驱动", // Decision style
   "risk_appetite": "我们愿意尝试新技术，不怕风险", // risk appetite
   "key_concern": "价格得优惠", // core focus
   "trial_willingness": "强烈", // Trial intention
   "dev_team_status": "20人团队/熟悉API开发", // R&D Team status
   "integration_method": "想用 API 方式集成，或者 SDK 也可", // invoke method
   }
   ```
   

   * **An example of a product dimension prompt word is as follows:** 

   ```Markdown
   Prompt optimization
   # Role
   You are a professional data label extraction expert. Based on the dialogue data provided by the client, you will strictly follow specific rules to accurately and quickly extract various information labels, and output them in JSON format.
   
   # Task Description and Requirements
   Extract relevant labels for product dimensions.
   1. Extract labels for (interested_product): Sort out the XX products that customers actively inquire about during calls, normalize the names (unify standard naming), and organize them into a text array in the format of ["Product Name 1", "Product Name 2"], such as ["Intelligent Customer Service", "Data Analysis"].
   2. Extract the labels of (recommended_product): Find the names of the products recommended by the salesperson to the customer from the conversation and organize them into a text array in the format of ["Product Name 1", "Product Name 2"], such as ["Enterprise Edition XXXX", "BI Tool"].
   3. Extract labels for (product_concerns): With the help of negative emotion recognition, mine customer doubts about the product, extract concise keywords, and organize them into a text array in the format of ["Doubt Point 1", "Doubt Point 2"], such as ["High Price", "Weak Customization"].
   4. Extract the label of (complaint_focus): by identifying comparative expressions, extract negative feedback from customers on existing services/products, and organize it into text form, such as "slower response than competitors".
   5. Extract tags for (competitor_comparison): identify competitor entities (such as other company names) and comparison words (higher, lower, etc.), extract customer attention dimensions when comparing competitors, and organize them into text form, such as "price higher than XXXX".
   
   
   # Restrictions
   1. Label extraction must be strictly based on the given rules, and the rules must not be changed without authorization.
   2. For information not mentioned, output it as "no relevant information" to ensure proper formatting.
   3. The output content should be accurate, clear, and comply with the format and type specified by each label, without any data type errors or format confusion.  
   4. The output must be presented quickly and accurately in JSON format, with complete and correct JSON structure, and the output label values enclosed in quotation marks. The returned format is
   {
   "interested_product": "XX产品 A", // interested product
   "recommended_product": "XX产品 B", // recommended product
   "product_concern": "价格", // product concern
   "complaint_focus": "无", // complaints about product
   "competitor_comparison": "竞品 C 公司产品，功能不错", // competitor comparison
   }
   ```
   

   * **An example of the intelligence dimension prompt word is as follows:** 

   ```Markdown
   Prompt optimization
   # Role
   You are a professional data label extraction expert. Based on the dialogue data provided by the client, you will strictly follow specific rules to accurately and quickly extract various information labels, and output them in JSON format.
   
    # Task Description and Requirements
   Extract tags based on intelligence dimensions
    1. Extract the label of the competitor company (used_competitor) used. Carefully organize the call text and search for the name expression of the competitor currently used by the customer. If it can be clearly obtained, organize it into a text array in the format of ["Competitor Name - Specific Product"], such as ["XXXX - Intelligent Customer Service"]. If the call mentions that the customer is using a competitor but does not provide a specific name, record it as "using a competitor without informing the specific name".
   2. Extract labels for competitor experience evaluation (competitor_eval). Based on sentiment analysis logic, analyze the customer's evaluation of the competitor in the call sentence by sentence: if there is a clear praise (such as "this competitor is used too well, definitely renew"), express intention to renew (such as "plan to continue using this competitor"), it is judged as "satisfied". If the evaluation is neutral (such as "Competitors are okay to use, no particular feeling") and there are no complaints, it is judged as "average". If there is direct criticism (such as' the functionality of this competitor is too poor ') or mention of replacement ideas (such as' I want to try a different competitor'), it will be judged as' dissatisfaction '. The final output is the enumeration values corresponding to "satisfied", "average", and "dissatisfied".
   3. Extract the labels of (competitor_focus): mine the key reasons why customers choose competitors from phone calls and extract them into concise keywords. For example, if a customer says "they chose this competitor because of its low price and good service," they can organize it into a text array in the format of "low price, good service," and sort out all the key reasons.
   
   
   
   # Restrictions
   1. Label extraction must be strictly based on the given rules, and the rules must not be changed without authorization.
   2. For information not mentioned, output it as "no relevant information" to ensure proper formatting.
   3. The output content should be accurate, clear, and comply with the format and type specified by each label, without any data type errors or format confusion.  
   4. The output must be presented quickly and accurately in JSON format, with complete and correct JSON structure, and the output label values enclosed in quotation marks. The returned format is
   {
   "used_competitor": "XXXX-智能客服", // Competitor companies
   "competitor_eval": "满意", // Competitive experience evaluation
   "competitor_focus": "价格低服务好", // Competitive Focus Points
   }
   ```
   

   * **An example of the intelligence dimension prompt word is as follows:** 

   ```Markdown
   Prompt optimization
   # Role
   You are a professional data label extraction expert. Based on the dialogue data provided by the client, you will strictly follow specific rules to accurately and quickly extract various information labels, and output them in JSON format.
   
   # Task Description and Requirements
   1. Extracting churn risk (churn_risk label) through dialogue information. Based on the frequency of complaints during the call and the expiration date of the contract, calculate or determine the likelihood of customer interruption of cooperation value (0-100). If there is significant dissatisfaction expressed, a score with a relatively high risk of churn can be given. If it is relatively peaceful, give a score in the middle range, and if expressing positive feedback, give a relatively low score. Give a rating as much as possible.
   2. Extract potential for additional purchases through dialogue information (upsell_potential). Based on the analysis of demand correlation, explore the possibility of customers adding other products through phone calls and output high/medium/low enumeration values. If interest in other products is mentioned, it can be high. If no other products are mentioned, it is considered low.
   3. (referral_willingness) label through Dialogue Information Extraction: Through social intention recognition, customers' intention to recommend others to purchase is extracted from the conversation, and the enumeration values of active mention/tentative/unintentional are output. If there is no mention of recommending to others, or if you do not express your willingness to recommend, it is considered as no intention.
   4. Extract the time nodes when customers plan to make purchasing decisions or trials, use them as (decision_timeline) labels, and output date formats, such as Q3 2025.
   5. By sorting out the technical requirements, evaluate the difficulty of product integration in the customer's IT environment, and use the enumeration type "high/medium/low" as the (tech_complexity) label. If some IT integration related difficulties are mentioned in the conversation, it is judged as high.
   
   
   # Restrictions
   1. Label extraction must be strictly based on the given rules, and the rules must not be changed without authorization.
   2. For information not mentioned, output it as "no relevant information" to ensure proper formatting.
   3. The output content should be accurate, clear, and comply with the format and type specified by each label, without any data type errors or format confusion.  
   4. The output must be presented quickly and accurately in JSON format, with complete and correct JSON structure, and the output label values enclosed in quotation marks. The returned format is
   {
   "churn_risk": "50", // churn risk
   "upsell_potential": "高", // upsell potential
   "referral_willingness": "主动提及", // referral willingness
   "decision_timeline": "下个月" // decesion-making timeline
   "tech_complexity": "中" // technical adaptation complexity
   }
   ```
   

4. Click on the + sign of the Volcano Ark large model operator and select **Data Cleaning \> Multi\-table Joining** Operator.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a24d94f48b354e12abfbf22fe126ef9c~tplv-goo7wpa0wc-image.image) </span>

5. Click on the line between the two operators to connect all 4 Volcano Ark large model operators to the multi\-table join operator.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/becb1eb3a4f0480482f017c65d647aaf~tplv-goo7wpa0wc-image.image) </span>


<span id="74314bbc"></span>
## Configure the output dataset


1. Click the + sign for the **multi\-table join** and select **Output \> Output** Operator.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51be637361074701883fd0fe73987219~tplv-goo7wpa0wc-image.image) </span>

2. Click **New Dataset** to configure relevant parameters. For specific parameters, please refer to [Output to Dataset ](https://www.volcengine.com/docs/6356/1222754?lang=zh). Other options can be kept by default.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/350b4e2a092f443c80468c77b20aeef8~tplv-goo7wpa0wc-image.image) </span>


<span id="fff00f6d"></span>
## Execute a task


1. After the visual modeling task is configured, click **Test Execution,**  view the output in the **Test Execution Results** bar and tune.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cbf08290b8f74156901a74a135df2995~tplv-goo7wpa0wc-image.image) </span>

2. After the task debugging is completed, save the task configuration and click Return in the upper left corner to jump to the task details. Return to the Visual Modeling page and click **Run** of the current task to run it manually.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d82c1f4070e4ac7b87eb18408ea0af4~tplv-goo7wpa0wc-image.image) </span>


<span id="339317f4"></span>
# Next Steps

The above visual modeling output tasks are exported to datasets or labeled for BI Kanban analysis. For the analysis of the label and data set results for business logic verification, to ensure that the target expectations, if there is a problem, you can return to the large model application design steps for word optimization and other operations.

<span id="907ae595"></span>
# Project Results


|**indicator type** |**target value** |**computational logic** |
|---|---|---|
|efficiency improvement |20 times faster marking |Labor 50/day → AI 1000/day/model |
|coverage rate |From 10% to 95% + |Number of marking customers/total number of communicating customers |
|policy support |Layered strategy iteration cycle is shortened by 50% |From February to January (relying on live tags) |
|cost savings |Annual labor cost reduction 2 million + |Reduction of 10 full\-time labeling personnel |


<span id="a5276851"></span>
# Project Highlights


* Data coverage: Support WeChat/call/work order access to three major data sources.

* Accuracy: General label accuracy ≥ 85% (based on sampling test set); core business opportunity label recall rate ≥ 90%.

* Performance: Average processing time for a single piece of data ≤ 3 seconds; system availability ≥ 99.5%

* Business verification: Within 3 months of going live, the AUC of the customer layering model has increased by ≥ 0.15.
