---
title: "Label Mining for Conversation Content in the Securities Industry"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Label_Mining_for_Conversation_Content_in_the_Securities_Industry"
---

Conversation content refers to all the information records generated when users and objects (such as customer service, intelligent assistants, and other users) interact through language or text, and is the core carrier that carries communication intentions, needs, and feedback. The core of mining the value of conversational content is to transform unstructured conversational data into structured business insights, and extract value from multi\-dimensional content based on structured data. This article shows you how to use conversation insights to analyze the conversation content of an AI conversation assistant and generate the required labels.

<span id="a60c29a4"></span>
# Background Introduction

A securities company has launched an AI stock market assistant for customer service, hoping to extract effective label information through the analysis of conversation content, identify the marketable value of customers, and improve customer satisfaction. But at present, the amount of conversation content data is huge, and it is time\-consuming and easy to miss to guess the marketable value of customers based on experience or manually analyze customers based on user portraits.

<span id="7833afe5"></span>
## Project Objectives

When a customer has a conversation with the AI stock market assistant, the system needs to analyze the conversation content and output it into three labels:


1. Consultation intention: Identify what financial knowledge the client wants to know (e.g. asking about fund returns, stock trends, new policies and regulations, etc.).

2. Operation intention: Determine what business the customer wants to do (such as changing passwords, setting fixed investments, checking positions, etc.).

3. Customer emotions: perceive the customer's current mood (happy/calm/dissatisfied).


<span id="2f946a3d"></span>
# Operation Steps

<span id="e2df8379"></span>
## Step 1: Prepare label content and conversation samples

You need to prepare the content, structure, and session\-ready format of the tags.


1. Confirm that the label content to be output includes: label name, label value, and label definition. The label value definition can be simple or complex, and keywords do not have to be written. It is necessary to ensure that the label value definition can be accurately identified when used as a large model cue word.

   Examples are as follows:

   
   |**label classification** |**label name** |**describe** |**label value** |**Label value definition** |
   |---|---|---|---|---|
   |intent tag |Consultation intent |Identify the customer's consultation intentions related to product revenue, market analysis, policy interpretation, etc. expressed in the conversation |product revenue |Clients ask about the returns, historical performance, or expected returns of a particular investment product. For example, the following keywords appear: yield, return, profit, income situation, XXXX... (supplement according to the specific situation) |
   ||||market analysis |Clients inquire about market conditions, trend analysis, sector performance, or macroeconomic conditions. For example, the following keywords appear: stock index, growth enterprises market index, financial sector, XXXX... (supplement according to specific circumstances) |
   ||||Policy interpretation |Clients inquire about the interpretation and impact of financial policies, regulations, taxation policies, or other relevant policies. For example, the following keywords appear: Securities Supervision Commission announcement, exchange rules, tax regulations, policy interpretation, regulatory policies, XXXX... (supplement according to specific circumstances) |
   ||||Market interpretation |Clients inquire about the interpretation of specific market conditions, trend analysis, or professional opinions. For example, the following keywords appear: market interpretation, market analysis, market trend, market forecast, XXXX... (supplement according to the specific situation) |
   ||action intent |Identify whether the customer has the intention of business operations in the conversation, such as position adjustment, fixed investment setting, threat and risk assessment, etc |Position analysis |Clients may consult or seek advice on adjusting their existing investment portfolios. For example, the following keywords appear: position analysis, position adjustment, position management, XXXX... (supplement according to the specific situation) |
   ||||fixed investment setting |Clients consult or operate the setting, modification or cancellation of regular fixed investment. For example, the following keywords appear: fixed investment, fixed quota, fixed investment, automatic investment, fixed investment plan, XXXX... (supplement according to the specific situation) |
   ||||threat and risk assessment |Clients ask about investment threat and risk assessment, product risk rating or personal risk tolerance. For example, the following keywords appear: product risk level, customer risk level, threat and risk assessment, XXXX... (supplement according to the specific situation) |
   |mood tag |customer sentiment |Identify the current mood of the customer in the conversation as positive, neutral, and negative. |forward |The positive emotions expressed by customers such as satisfaction, joy, expectation, and gratitude. For example, the following keywords appear:<br><br>Profit, money, income, rise, daily limit, surge, surge, satisfaction, XXXX... (supplement according to the specific situation) |
   ||||neutral |Neutral emotions such as calm, objectivity, and inquiry expressed by customers. For example, the following keywords appear:<br><br>Understand, want to know, ask, consult, inquire, how, how, XXXX... (supplement according to the specific situation) |
   ||||Negative |The customer's tone and attitude are poor, expressing dissatisfaction with the service/product/income; for example, the following keywords appear: loss, loss, loss, drop, drop limit, plunge, crash, XXXX... (supplement according to the specific situation). |
   

2. Confirm the session sample data.

   It is recommended that you prepare the session sample in the standard format, which is as follows:

   
   |**session date** |**session id** |**session type** |**session start time** |**session end time** |**user id** |**user name** |**Agent ID** |**Agent name** |**conversation content** |
   |---|---|---|---|---|---|---|---|---|---|
   |20250520 |test2 |1V1 private chat |2025/5/20 12:40 |2025/5/20 12:48 |2 |Mr. Liu 18888888888 |1061XXXX5 |Far ahead \- newcomer XX |2024\-08\-20 18:07: 07_ customer (Mr. Liu 18888888888) _ change the transaction password<br><br>; 2024\-08\-20 18:07: 47_ Customer service (far ahead \- newcomer XX) _ Hello, under normal circumstances, after opening an account, the transaction passwords of the ordinary account and the credit account are the same. When modifying or resetting the transaction password, the transaction password of the ordinary account and the credit account will be modified at the same time. |
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If your session data cannot be used directly, you can use visual modeling to convert it into a format dataset available to VeCDP, see details <a href="https://docs.byteplus.com/docs/dataagent/Label_Mining_for_Conversation_Content_in_the_Securities_Industry#00815bad">1. Visual modeling</a>.   </div>
   

<span id="9bab9703"></span>
## Step 2: Session data access


1. Log in to the VeCDP console and select **Data Management \> Data Connections** .

2. In the upper left corner of the Data Connections directory, click **New Data Connection** and select **Local File \- Excel or CSV** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c67c8fc626534d51968c289f53ca0989~tplv-goo7wpa0wc-image.image) </span>

3. After clicking, locate the target Excel/CSV file in the local file and click Open.

4. When the loading is complete to 100%, you can select the contents of the sheet in the file. Click Next to **preview data** and set the **data connection name** . After the preview is completed, click **OK** to complete the data connection of Excel/CSV.


<span id="4d5e8ea4"></span>
## Step 3: Create a new session file

<span id="00815bad"></span>
### 1. Visual modeling

It is necessary to process the messages in the session data into a standard session (ie, a conversation) through visual modeling.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0773e6e8670c489695cdda2e2280f973~tplv-goo7wpa0wc-image.image) </span>

<span id="3b5eaf85"></span>
#### 1.1 Data access


1. Select **Data Management \> Visual Modeling** in the top navigation bar of the VeCDP console. Select the **task list** in the left list and click **New \> New Offline Task** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b3ff938281d476b9d38addb70f92e75~tplv-goo7wpa0wc-image.image) </span>

2. At the top left of the New Task page, click ➕ **Add Data Connection**. Select the data connection you just created.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/981e0921e89d4fe48be5c0f26149e7f7~tplv-goo7wpa0wc-image.image) </span>

3. Select one of the data connections and pull it from the left list into the right panel. (Example: Select "Session File" and pull it to the right.)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2afd8c0f63e244c8bab9e1aa725eb1e1~tplv-goo7wpa0wc-image.image) </span>

4. Click on the dataset to configure the relevant information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6b6fde5b23d48ea8346c303c213d487~tplv-goo7wpa0wc-image.image) </span>


<span id="4fcd031d"></span>
#### 1.2 Data cleaning


1. Click the + sign on the right side of the dataset and click **Calculate Column** .

   Calculate column operators, support custom expressions, use Spark functions to process upstream fields and add new fields. The configuration flow for computed columns clearly displays new fields in tabular form.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0dfcbc8c35e0494cb3c9f6291528d165~tplv-goo7wpa0wc-image.image) </span>

2. Click **Add** to configure the calculated column names and expressions. Then click **OK**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c251e40580a44de5acf3669fbcda2f53~tplv-goo7wpa0wc-image.image) </span>

   
   |parameter |example |
   |---|---|
   |calculated column name |unique Session ID |
   |field type |automatic |
   |edit expression |`CONCAT ('user id', '_', 'session id')` |
   

3. Click **Data Preview** to view the data preview results and confirm the data results.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3505a0b6d66b42efbc558abf44fd16ea~tplv-goo7wpa0wc-image.image) </span>

4. Click the + sign to the right of the calculated column and click the **calculated column**. Add another calculated column, as shown above.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73896f0ec4f7440a82b0e9eae559a8cf~tplv-goo7wpa0wc-image.image) </span>

   
   |parameter |calculated column name |calculated column name |edit expression |
   |---|---|---|---|
   |Name 1 |single\-line conversation content |string |```Markdown```<br>```concat_ws(```<br>```  '_',```<br>```  array(```<br>```    `时间`,```<br>```    CASE WHEN `角色` = 'user' THEN '客户 (刘先生 18888888888)' ELSE '客服 (测试客服)' END,```<br>```    `内容````<br>```  )```<br>```)```<br> |
   |Name 2 |Sort time |automatic |```Markdown```<br>```CASE```<br>```  WHEN `角色` = 'ai' THEN```<br>```    CAST(FROM_UNIXTIME(UNIX_TIMESTAMP(`时间`, 'yyyy-MM-dd HH:mm:ss') + 1) AS TIMESTAMP)```<br>```  ELSE```<br>```    CAST(`时间` AS TIMESTAMP)```<br>```END```<br> |
   |Name 3 |Session ID string |automatic |```Markdown```<br>```cast(`会话id` as string)```<br> |
   

5. Click the + sign to the right of the calculated column and click **Data Cleaning \> Free Sorting.** 

   Free sorting operator: Select a sorting field to sort all the data or some combination of dimensions, and you can choose to intercept the data of the previous K value according to the sorting. K is the order number of the interception. If you take the top 100 according to the score, 100 is the K value. Group sorting function is equivalent to the process of setting partition and sorting by window function. Details can be found in [Free Sorting](https://www.volcengine.com/docs/6356/1222749?lang=zh#_2-12-%E8%87%AA%E7%94%B1%E6%8E%92%E5%BA%8F).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d1352157bda4a32b90b9bb19281c122~tplv-goo7wpa0wc-image.image) </span>

6. Configure the parameters of the free sort operator and click **Data Preview** to view the results.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a65b613832ac45bda0ef85c308c21119~tplv-goo7wpa0wc-image.image) </span>

   
   |parameter |example |
   |---|---|
   |sort by |group sort |
   |group field |Session Id |
   |sort field |Sort time |
   |rule |ascending order |
   |sort only |close |
   |K value before interception |1000 |
   

7. Click the + sign to the right of the free sort operator, click **Data Cleaning \> Aggregation,**  and configure the parameters of the aggregation operator by dragging in fields, and then click **Data Preview** to view the results.

   Aggregation: Aggregation of detailed data by grouping.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b791631a1ae44adfa32aef198203ae54~tplv-goo7wpa0wc-image.image) </span>

   
   |parameter |example |
   |---|---|
   |group |Unique Session ID |
   |polymerization |* Min: time<br><br>* Max: time<br><br>* collect_list: within a single\-line session<br><br>* Max: user id |
   |sort field |/ |
   |collation |ascending order |
   

8. Click the + sign to the right of the aggregation operator and click **Calculate Column.**  Configure the parameters of the **calculated column** and click **Data** Preview to view the results.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62aedda4a8be4a628478dd1fdb9cb0fd~tplv-goo7wpa0wc-image.image) </span>

   
   |parameter |calculated column name |calculated column name |edit expression |
   |---|---|---|---|
   |Name 1 |user name |automatic |```Markdown```<br>```'刘先生 18888888888'```<br> |
   |Name 2 |Agent ID |automatic |```Markdown```<br>```lpad(cast(abs(hash(`唯一会话iID`)) % 100000000 AS string), 8, '0')```<br> |
   |Name 3 |Agent name |string |```Markdown```<br>```'测试客服'```<br> |
   |Name 4 |session type |automatic |```Markdown```<br>```'1v1私聊'```<br> |
   |Name 5 |User _ID_STR |automatic |```Markdown```<br>```upper(```<br>```  translate(```<br>```    lower(substring(md5(`唯一会话iID`), 1, 9)),```<br>```    '0123456789abcdef',```<br>```    'ABCDEFGHIJKLMNOP'```<br>```  )```<br>```)```<br> |
   |Name 6 |start time |automatic |```Markdown```<br>````min_时间````<br> |
   |Name 7 |end time |automatic |```Markdown```<br>````max_时间````<br> |
   |Name 8 |session duration |automatic |```Markdown```<br>```2```<br> |
   

9. Click the + sign to the right of the calculated column and click the **calculated column.**  Configure the parameters of the **calculated column** and click **Data** Preview to view the results.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b0e0534bcc24ec8b2250bddf35b13a8~tplv-goo7wpa0wc-image.image) </span>

   
   |parameter |calculated column name |calculated column name |edit expression |
   |---|---|---|---|
   |Name 1 |conversation summary |automatic |```Markdown```<br>```regexp_replace(```<br>```    regexp_replace(```<br>```        regexp_replace(```<br>```            concat_ws("", `collect_list_单行会话内容`),```<br>```            '"',```<br>```            ''```<br>```        ),```<br>```        '<[^>]*>',```<br>```        ''```<br>```    ),```<br>```    '[\r\n]+',```<br>```    ''```<br>```)```<br> |
   


<span id="e1f64ba7"></span>
#### 1.3 Configuring large model operators (optional)

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This step can be omitted if you use the Session Insights task to extract tags. See the specific operation <a href="https://docs.byteplus.com/docs/dataagent/Label_Mining_for_Conversation_Content_in_the_Securities_Industry#916eb372">Step 4: Create a new session insight task</a>.</div>



1. Click the + sign on the right side of the calculation column, and click the **featured area operator \> Volcano Ark large model**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b80cbf6b043a42e4b56ea23c389a356d~tplv-goo7wpa0wc-image.image) </span>

2. Configure hints and user input for the large model operator, see [Volcano Ark Large Model ](https://www.volcengine.com/docs/7139/1829075)for details.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/228e236ad52a463aaf0dc776d86f70f5~tplv-goo7wpa0wc-image.image) </span>

   An example of a cue word is as follows:

   ```Markdown
   # Role
   
   You are a professional intelligent customer service conversation annotation assistant that can accurately and efficiently analyze the conversation content between customers and intelligent agents, and accurately label the conversation based on a predefined tagging system. For any input conversation content, you must quickly and accurately return annotated results in JSON format.
   
   ## Skills
   
   ###Skill 1: Consultation Intent Recognition
   1. Carefully analyze the conversation content and identify the consulting intentions expressed by the client, including product returns, market analysis, policy interpretation, market analysis, stock analysis, financial allocation, basic knowledge, etc.
   2. For vague or complex expressions, determine the main consulting intention through context analysis and keyword recognition.
   
   ###Skill 2: Recognition of Operational Intent
   1. Analyze the conversation content to identify whether the client has expressed their intention for business operations, such as position analysis, fixed investment settings, risk assessment, trading operations, account opening, account closing, other account management, etc.
   2. Accurately determine the type of operational intention based on the customer's statements, questions, and requests.
   
   ###Skill 3: Emotional State Recognition
   1. Determine whether the customer's emotional state is positive, neutral, or negative based on their language, tone, and expression.
   2. Taking into account the overall context and context of the conversation, determine the customer's main emotional tendencies.
   
   ## Label system
   
   ### Consultation intention
   Possible values:
   -Product returns: Customers inquire about the returns, historical performance, or expected returns of specific investment products
   -Market analysis: Customers inquire about market conditions, trend analysis, sector performance, or macroeconomic conditions
   -Policy interpretation: Customers inquire about the explanation and impact of financial policies, regulatory regulations, tax policies, or other related policies
   -Market interpretation: Customers inquire about the interpretation, trend analysis, or professional opinions of specific market trends
   -Stock analysis: Customers inquire about the analysis, evaluation, or investment advice of specific stocks
   -Financial configuration: Customers inquire about personal financial planning, asset allocation advice, or long-term investment strategies
   -Basic knowledge: Customers inquire about financial fundamentals, product tools, etc
   -Other: Those that do not belong to the above categories can be classified as other
   
   ### Operation intention
   Possible values:
   -Position analysis: Customers consult or seek advice on adjusting their existing investment portfolio
   -Fixed investment setting: Customers consult or operate the setting, modification, or cancellation of regular fixed investments
   -Risk assessment: Customers inquire about investment risk assessment, product risk level, or personal risk tolerance
   -Trading operations: Customer inquiries or trading operations such as buying, selling, converting, etc
   -Account opening: Customer inquiries or operations regarding the process and requirements for opening and registering a new account
   -Account cancellation: Customer inquiries or operations for account cancellation, deletion, etc
   -Account management: Account management matters such as customer inquiries or operational modifications
   -Others: Those that do not belong to the above intentions belong to others.
   
   ###Customer emotions
   Possible values:
   -Positive: Positive emotions such as satisfaction, happiness, anticipation, and gratitude expressed by customers
   -Neutral: The neutral emotions expressed by customers, such as calmness, objectivity, and inquiry
   -Negative: The customer's tone and attitude are poor, and they express dissatisfaction with the service/product/revenue
   
   ## Output format
   - Output results in JSON format
   For instance:
   {
    "Consultation intention":<Product Returns, Market Analysis, Policy Interpretation, Market Analysis, Stock Analysis, Financial Allocation, Basic Knowledge, Other)>,
    "Operational intention":<Position Analysis, Fixed Investment Setting, Risk Assessment, Trading Operations, Account Opening, Account Closing, Other Account Management, Other>,
    "Customer Emotions":<Positive, Neutral, Negative>
   }
   
   For any input conversation content, you must return the annotation result in the following JSON format:
   
   
   ## Restrictions
   
   1. Only handle dialogue content related to financial investment services and refuse to handle other unrelated content.
   2. Strictly output the results in the given JSON format without any deviation.
   For consultation or operational intentions that cannot be clearly determined, "other" can be output.
   4. Do not add any additional explanations or clarifications beyond the JSON output.
   5. Each conversation can have multiple consultation intentions and operational intentions.
   6. Customer emotions must have a value and cannot be null.
   
   ## For instance
   
   ### instance1
   
   **Input**:
   ```
   Customer: What is the recent yield of this fund? I saw that it performed well last year and would like to know about its recent dividend situation.
   Intelligent agent: Hello, this fund has a return rate of XX% in the past 3 months and XX% in the past 6 months. Last year did perform exceptionally well, with an annual revenue of XX%. The last dividend was on the 15th of last month, with a dividend of XX yuan per share.
   Customer: Okay, thank you for your answer. The information is very detailed.
   ```
   
   **Output**:
   ```json
   {
     "Consultation intention": "Product Returns",
     "Operational intention": "Other",
     "Customer Emotions": "Positive"
   }
   ```
   
   ### instance2
   
   **input**:
   ```
   Customer: I would like to buy 100 shares of the stock recommended by your company. May I place an order now?
   Agent: Hello, it is currently trading time and you can place an order immediately. May I ask which stock you want to buy?
   Customer: It's the XX stock recommended by the analyst yesterday, with the code XXXXX.
   Intelligent agent: Understood, you want to purchase XXXXX shares. The current stock price is XXXX yuan per share. Are you sure you want to purchase 100 shares at market price?
   Customer: Yes, confirm purchase.
   ```
   
   **Output**:
   ```json
   {
     "Consultation intention": "Other",
     "Operational intention": "Trading Operations",
     "Customer Emotions": "Neutral"
    }
   ```
   
   ### instance3
   
   **Input**:
   ```
   Customer: The market has been fluctuating greatly recently, and I would like to know the overall performance of the XX sector?
   Intelligent agent: Hello, the XX sector has indeed experienced significant fluctuations recently. In the past month, the XX sector as a whole has fallen by XX%, but when broken down, XX and XX related stocks have performed relatively steadily, rising by XX% and XX% respectively. Market analysts generally believe that with policy support and improved fundamentals, the XX sector still has good performance opportunities in the medium and long term.
   Customer: Understood, do I need to adjust my current XX stock holdings? I mainly hold XX and XX stocks.
   ```
   
   **Output**:
   ```json
   {
     "Consultation intention": "Market Analysis",
     "Operational intention": "Position Analysis",
     "Customer Emotions": "Neutral"
   }
   ```
   
   
   ```
   

   
   |parameter |example |
   |---|---|
   |user input |$ |
   |parallelism |1 |
   |timeout |180000ms |
   |number of retries |1 |
   |request interval |1000ms |
   |complete exception handling |terminate task |
   

3. Click **Test Execution** to view the output in the **Test Execution Results** bar.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/863c0dca887b40a7b44baaddeb5484e5~tplv-goo7wpa0wc-image.image) </span>

4. Click the + sign on the right side of the large model operator of Volcano Ark, click **Field Settings, and** tick the required field. Then click **Data Preview** to view the data results.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43945300cada42c892c49c1e92d27b61~tplv-goo7wpa0wc-image.image) </span>


<span id="e43fb49c"></span>
#### 1.4 Configuration data output


1. Click the + sign on the right side of the field settings, and click **Output \> Output.** 

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88f22d6f66594ed881319ef9c31b62d5~tplv-goo7wpa0wc-image.image) </span>

2. Click **New Data Set** to configure accordingly. See [Output to Dataset for details](https://www.volcengine.com/docs/6356/1222754?lang=zh).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fd1fbdbc8d204de7b46ae0bf707c9a5a~tplv-goo7wpa0wc-image.image) </span>

   
   |parameter |example |
   |---|---|
   |CDP application |common dataset |
   |type |ClickHouse |
   |data lifecycle |Keep the last 365 days |
   |partition |default |
   |cluster |rangers |
   |sort key |row_id |
   |sharding key |row_id |
   |Sample field |row_id |
   


<span id="079f3c33"></span>
#### 1.5 Execute the task


1. Click **Test Execution** in the upper right corner to debug the task according to the execution result. After the task debugging is completed, save the task configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/78c2e54efcca49aa804ee581752433cd~tplv-goo7wpa0wc-image.image) </span>

2. Click Back in the upper left corner to jump to the task details. Return to the Visual Modeling page and click **Run** of the current task to run it manually.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/053edf3078644243b2ac42c2dac1b29c~tplv-goo7wpa0wc-image.image) </span>


<span id="78f2e255"></span>
### 2. Data files


1. In the top navigation bar of the VeCDP console, select **Data Management \> Data Profile Management** and click the **Session Profiles** tab.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aec73b1867fe455798f03b4029e4ab35~tplv-goo7wpa0wc-image.image) </span>

2. Click **New Data File** , select **Session File** , support creating multiple, and complete the relevant configuration on the orchestration page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4babd9e3b3844adf8472f1917ec749c2~tplv-goo7wpa0wc-image.image) </span>

   
   |**parameter** |**parameter description** |**Parameter example** |
   |---|---|---|
   |session file |The session file obtains the data of the latest partition of the dataset every day. Please ensure that the latest "dataset partition" contains the attributes and characteristics of all session files. |session file |
   |dataset |Drop down and select the available datasets to register as data files that VeCDP can use for queries.<br><br><br>1. Only the dataset that the VeCDP application matches the data file type can be selected.<br><br>2. Only data sets that are routinely updated/updated in real time are allowed.<br><br>3. For query acceleration, some datasets may not be available when registering different types of data files, and ETL processing is required. |Dataset _2 |
   |data file name |Customization, no more than 100 words, allowing Chinese and English, numbers, and underscores. |data access |
   |Data profile description |Custom. |XX data access |
   |Associated Body |Select the principal under which the data file hangs. |person |
   |session data source |Drop down to select Enterprise Conversations \- Individual Chat, Agent, Voice Conversation. |Agent |
   |partition incremental update |Partition stores incremental data every day. If you want to query the data of a business meaning date in the last 7 days (such as the order creation time is the partition date), you need to query across partitions. |partition incremental update |
   |Session ID |Session unique identifier field, if the original session has a unique identifier for a conversation, the original ID is used. If not, it is a new ID aggregated through data processing. |'Unique session ID' |
   |session type |Session type: such as WeCom conversation\-single chat, voice outbound call\-A channel, etc., using the enumeration value defined by the system, and the field type is string. |string |
   |Principal OneID |The OneID field for the target principal. |'max_ user id' |
   |Customer ID |Used to save the customer ID segment. |'User _ID_STR ' |
   |Customer name |Field to hold the customer name. |'User name' |
   |Customer Service ID |Used to save the customer service ID field. |'Agent id' |
   |Customer service name |Field to hold the customer service name. |'Agent name' |
   |conversation content |A field used to hold a complete conversation. |'Conversation content summary' |
   |session start time |A field that holds the time when the first message of a conversation was sent. |'min_ time' |
   |session end time |A field that holds the time when the last message of a conversation was sent. |'max_ time' |
   |session duration |A field to hold the duration of this session. |'Session Duration ' |
   |time partition |The field type is date. |'p_date' |
   |character attribute |Used to hold a property field of type string. |/ |
   |numeric attribute |Used to hold an attribute field of type int. |/ |
   |floating point attribute |Used to hold a property field of type float. |/ |
   


<span id="916eb372"></span>
## Step 4: Create a new session insight task


1. In the top navigation bar of the VeCDP console select **More \> Session Insights \> Session Quality Assessment** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73966a45c7164f18a166cec0a5faf11b~tplv-goo7wpa0wc-image.image) </span>

2. On the **Session Quality Assessment** page, click **New Task**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae47d6d41dc846f7a375606599a13f70~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the **task name, data file** and **data date** , then click **Next**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f4a479cd9563458c80ca343430a6f0c4~tplv-goo7wpa0wc-image.image) </span>

   
   |parameter |explain ||||example |
   |---|---|---|---|---|---|
   |task name |Custom name. ||||data access |
   |task update type |Currently only offline session evaluation is supported. ||||offline session evaluation |
   |task update method |Support manual update or regular update (regular update can be set by day, week, month), and manual update is selected by default. ||||manual update |
   |data archive |You can single\-select session files under all subjects, and a file can be associated with up to 5 tasks. ||||Select the session file set in the previous step, data access |
   |data date |Select the range of data read by the task, either a dynamic date or a fixed date; or a single date. ||||Single date |
   | |dynamic date<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ac6289d7a4f4f34b11d02ac1f4719ce~tplv-goo7wpa0wc-image.image) </span> ||Fixed date<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/427a2e78745546f5bbd6daa72245642a~tplv-goo7wpa0wc-image.image) </span> |Single date<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/861d77733ed04b38b2504f3fe25ca907~tplv-goo7wpa0wc-image.image) </span> | |
   

4. Select **New application** , you can choose to copy from the existing application can also be created from the template, you can also click intelligent recommendation application, enter the session evaluation target, the system will recommend the corresponding application. When the new creation is complete, click **OK** . See the specific operation [Step 6: Session Quality Assessment](https://docs.byteplus.com/docs/undefined/6a200c3e04155105142ce01e#732d6b02).

   This scenario requires the creation of three applications: emotion recognition, consultation intent, and operation intent.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/324636fdfb5a477586a03ca1f37cf803~tplv-goo7wpa0wc-image.image) </span>

5. After creating the new app, click **Edit** to modify the **prompt word** and **structured output configuration**.

   Examples of cue words and structured output configurations for the three applications are as follows:

   * **Emotion recognition:** 

      * Structured output configuration:

         
         |parameter |example |
         |---|---|
         |field name |emotion |
         |field type |enumeration |
         |enumeration value |Positive, negative, neutral |
         |describe |emotion recognition |
         |Do you need a reason |open |
         |reason description |Clearly state the basis for judging the overall mood, citing key sentences or semantics in the conversation |
         

      * Cue word:

         ```Markdown
         # Customer emotion recognition expert
         ## role
         You are a professional customer emotion recognition expert with the ability to accurately analyze customer emotions and emotional transitions from dialogue texts, and provide accurate emotional judgments based on semantics and context.
         ## Mission objective
         Based on the provided dialogue text, complete the following analysis:
         1. Determine the customer's emotional state during the conversation (positive/neutral/negative)
         2. Identify emotional turning points and their reasons during the conversation process
         3. Output structured emotion analysis results
         ##Emotional judgment rules
         ### 1. Positive emotion recognition
         When customers express positive attitudes such as satisfaction and joy, it triggers positive emotions. Keywords include:
         Profit, make money, gain, rise, limit up, skyrocket, surge, satisfied, very good, XX...//Please supplement according to specific situations
         ### 2. Neutral emotion recognition
         When customers show a calm, objective, or inquiring state, neutral emotions are triggered. Keywords include:
         Understand, want to know, ask, consult, inquire, how, how, XX...//Please supplement according to specific situations
         ### 3. Negative emotion recognition
         When customers express dissatisfaction, anxiety, or complaints, negative emotions are triggered. Keywords include: loss, loss of money, loss of money, decline, limit down, plunge, plunge, collapse, XX...//Please supplement according to specific situations
         ## input information
         {session}
         ## processing logic
         1. Scan the conversation content and detect the occurrence of keywords
         2. Keyword matching priority: Negative>Positive>Neutral
         3. Determination of emotional transition:
         -When the emotion category changes in adjacent dialogue rounds
         -Reasons for the turning point need to be explained (combined with contextual semantic analysis)
         4. Overall emotional assessment:
         -Based on the emotional state at the end of the conversation
         -When negative emotions arise, prioritize labeling them as negative
         ## Restrictions
         -Analyze based solely on the dialogue content to avoid subjective speculation.
         -The output must be in a strict JSON structure without any additional instructions   or formatting modifications (such as Markdown)
         -Prohibit outputting JSON format
         -Block any possible privacy information
         ```
         

   * **Intentions for consultation:** 

      * Structured output configuration:

         
         |parameter |example |
         |---|---|
         |field name |zixunyitu |
         |field type |enumeration |
         |enumeration value |Product income, market analysis, policy interpretation, market interpretation, stock analysis, financial allocation, basic knowledge, etc |
         |describe |zixunyitu |
         |Do you need a reason |open |
         |reason description |The reason for generating the result of this description field: "zixunyitu" |
         

      * Cue word:

         ```Markdown
         # Consultation with intent recognition experts
         ## role
         You are a professional expert in customer consultation intention analysis, dedicated to accurately identifying customers' consulting needs in professional fields such as product returns, market analysis, policy interpretation, etc. from financial dialogue texts.
         ## task target
         Based on the conversation content, identify and output all the consulting intentions expressed by the customer (multiple choices are allowed):
         1. Product revenue
         2. Market analysis
         3. Policy interpretation
         4.XXXX
         5...//Please supplement according to specific circumstances
         ## Intention judgment rule
         ### 1. Product revenue
         When customers inquire about the returns, historical performance, or expected returns of a specific investment product. Keywords such as yield, return, profit, XXXX...//Please supplement according to specific situations
         ### 2. Market analysis
         When a customer inquires about market trends, trend analysis, sector performance, or macroeconomic conditions, it triggers. Keywords such as certificate index, XXXX...//Please supplement according to specific situations
         ### 3. Policy interpretation
         When customers inquire about the explanation and impact of financial policies, regulatory requirements, tax policies, or other related policies. Keywords such as CSRC announcements, exchange rules, tax regulations, XXXX....//Please supplement according to specific circumstances
         ### 4. Market Interpretation
         When customers inquire about the interpretation, trend analysis, or professional opinions of specific market trends. Keywords: market interpretation, market analysis, market trend, market forecast, market commentary, market analysis, market viewpoint, market report, market outlook, market review, market analysis, market interpretation, intraday observation, post market summary, pre-market forecast, technical interpretation, fundamental interpretation, policy interpretation, funding interpretation, market sentiment interpretation
         ### 5. Other
         When the customer fails to meet the above X situations, they are all other cases
         ### 6.XXXX.......//Supplement according to specific circumstances
         ## Processing logic
         1.**Single intent output principle**:
         Always output an optimal intention When multiple intentions are triggered, select based on matching priority Intention to choose keywords with higher density when given the same priority: perfect match>exact match>semantic match.
         2.**Keyword matching principle**:Complete matching requires 100% keyword matching. Accurate matching requires core terminology matching degree>80%.Semantic matching requires clear reasoning basis.
         ## input information
         {session}
         #Restrictions
         -Analyze based solely on the dialogue content to avoid subjective speculation
         -The output must be in a strict JSON structure without any additional instructions or formatting modifications (such as Markdown)
         -Prohibit output of JSON format
         -Block any possible privacy information
         ```
         

   * **Action intent cue**

      * Structured output configuration:

         
         |parameter |example |
         |---|---|
         |field name |operation_intention |
         |field type |enumeration |
         |enumeration value |Position analysis, fixed investment setting, threat and risk assessment, trading operations, account opening, account cancellation, account management, etc |
         |describe |Customer's operational intent recognition |
         |Do you need a reason |open |
         |reason description |Reasons for customer intent recognition |
         

      * Cue word:

         ```Markdown
         
         # Expert in Operational Intent Recognition
         ## Role
         You are a professional financial business operation intention analysis expert, dedicated to accurately identifying X-class business operation needs such as position analysis, fixed investment setting, risk assessment, etc. from customer conversations.
         ## Task target
         Identify and output all operational intentions expressed by the customer based on the conversation content (multiple choices are allowed)
         1. Position analysis
         2. Fixed investment settings
         3. Risk assessment
         4. XXXX....//Please supplement according to specific circumstances
         ## Intention judgment rule
         ### 1. Position analysis
         Triggered when clients consult or seek advice on adjusting their existing investment portfolio. Keywords: position analysis, position adjustment, position management, XXXX...//Please supplement according to specific situations
         ### 2. Fixed investment settings
         Triggered when customers inquire or operate on the setting, modification, or cancellation of regular fixed investment. Keywords: fixed investment, regular quota, XXXX....//Please supplement according to specific situations
         ### 3. Risk assessment
         Triggered when customers inquire about investment risk assessment, product risk level, or personal risk tolerance. Keywords: product risk level, customer risk level, XXXX....//Please supplement according to specific situations
         ### 4. Trading operations
         Triggered when customers inquire or engage in trading operations such as buying, selling, converting, etc. Keywords: buy, sell, subscribe, redeem, XXXX....//Add according to specific circumstances
         ### 5. Account Opening
         When a customer inquires or operates on the opening, registration process, and related requirements for a new account. Keywords: account opening, account opening, XXXX....//Please supplement according to specific circumstances
         ### 6. Account closure
         Triggered when the customer closes the account, keywords: account cancellation, deletion
         ### 7. Other account management
         When management issues such as customer inquiries or operational modifications are triggered. Keywords: account modification, password reset, information change, XXXX....//Please supplement according to specific circumstances
         ### 8. Other
         When the first 7 rules are not hit in other situations, it indicates other operational intentions
         
         ## Processing logic
         1.**Single intent output principle**:
         -Always output an optimal intention
         -When multiple intentions are triggered, select based on matching priority
         -Intention to choose keywords with higher density when given the same priority: perfect match>exact match>semantic match>other
         2.**Keyword matching principle**:
         A perfect match requires 100% keyword matching
         Accurate matching requires a core term consistency of>80%
         Semantic matching requires clear reasoning basis
         ## input information
         {session}
         ## Restrictions
         -Analyze based solely on the dialogue content to avoid subjective speculation
         -The output must be in a strict JSON structure without any additional instructions   or formatting modifications (such as Markdown)
         -Prohibit output of JSON format
         -Block any possible privacy information
         ```
         

6. After the configuration is completed, click **Debug** on the application interface, enter the session content for debugging, if it does not meet the business requirements, you can modify the prompt word and structured output of the previous step until the prompt word can meet the needs of the business, and then click **Save**.

7. On the New Task page of the VeCDP console, click **Next** , then **Test** , evaluate the entire task, and then click **Finish**.


<span id="8c161024"></span>
# View Results


1. On the **Session Quality Assessment** page, click **View Results** in the **action** bar of the task.

2. The evaluation result will be output to the dataset of VeCDP. Click the dataset name on the back of the **result output** to automatically jump to view. You can also click the **Run Results** tab to filter individual business dates and download the results.

3. In the **Data Overview** on the **Session Quality Assessment** page, you can clearly see label richness, null rate, and coverage.

4. On the **running results** of the **session quality evaluation** page, view the results of label extraction, and click **Details** to view the reason why the large model is labeled.


<span id="abea1b5d"></span>
# Project Results

Through the Volcano Engine intelligent marketing agent product, conversation data can be recognized, and the accuracy rate of customer intention recognition and emotion recognition has reached more than 90%, which is at the leading level in the industry and twice as high as the efficiency of manual recognition. Capturing customer intentions and emotions, driving precise business actions, and mining tags can help enterprises dynamically optimize customer follow\-up strategies, generate personalized recommendations, and form a closed loop of intelligent decision\-making from data analysis to business transformation.
