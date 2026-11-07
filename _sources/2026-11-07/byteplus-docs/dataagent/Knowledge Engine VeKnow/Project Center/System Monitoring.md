---
title: "System Monitoring"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/System_Monitoring"
---

The function of system monitoring is to track the running status of the knowledge base in real time (such as visits, query success rate, content update) and abnormalities (such as failures, inefficient retrieval) to ensure its stable and efficient operation. Applicable scenarios are scenarios that need to ensure the continuous availability of the knowledge base and optimize the operation efficiency. In particular, it is suitable for high\-volume customer service knowledge base operation and maintenance, enterprise core business knowledge system stability assurance, and multi\-end point knowledge base service quality monitoring. This article describes how to monitor assets and models.

<span id="b54d41bf"></span>
# Asset Monitoring


1. Log into the Marketing Agent console and select **Enterprise Knowledge Engine** in the left navigation bar.

2. In the left navigation bar of the Enterprise Knowledge Engine, select **Project Center** \> **System Management** \> **Asset Monitoring**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cbd4be3a1d2d4ef09bb27562ad2c0c42~tplv-goo7wpa0wc-image.image) </span>

3. On the asset monitoring page, set a time interval to filter out information such as the number of AI applications associated with the enterprise knowledge engine, content usage effectiveness (such as recall times), and so on.

4. Click "Update Record" to view the update records of the enterprise knowledge engine. It can be filtered by parameters such as operation type and operation object. The update records of the same knowledge base store the most recent 3 months of data by default.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b2aa5cc82b54bc38185d9af76281dd1~tplv-goo7wpa0wc-image.image) </span>

   
   |**Parameter** |**Explain** |
   |---|---|
   |Number of associated AI applications |The total number of AI applications currently tied to the enterprise's knowledge engine |
   |Recall times |Total number of times enterprise knowledge engine content is invoked by AI applications |
   |Number of sessions |Total number of sessions using AI apps |
   |Number of likes/clicks |During the AI application session, the total number of likes and clicks on the reply question by the user |
   |Operation type |Radio selection, including create, copy, edit, import, delete, re\-sharding. Default "All Operation Types"<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When filtering, merge types, edit knowledge base names, edit knowledge base descriptions, and edit paragraphs are all edits</div><br> |
   |Action object |Single selection, including knowledge base, documentation, sharding. Default "All Object Types" |
   |Update Person |Radio selection, default "All Updater" |
   |Update time |Default last 30 days |
   


<span id="989e4937"></span>
# Model Monitoring


1. Log into the Marketing Agent console and select **Enterprise Knowledge Engine** in the left navigation bar.

2. In the left navigation bar of the Enterprise Knowledge Engine, select **Project Center** \> **System Administration** \> **Model Monitoring**.

3. On the model monitoring page, you can filter and view the called model performance indicators (such as call volume, token consumption, response speed, etc.) by selecting the user, application, and time, providing data support for resource optimization and exception troubleshooting.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1b26708e7771490088d62614ea3c100f~tplv-goo7wpa0wc-image.image) </span>

   
   |**Parameter** |**Explain** |
   |---|---|
   |Total number of calls |Associated model, total number of calls |
   |Total Number of Tokens Invoked |Input and output Token cumulative consumption |
   |Enter Total Tokens |Input Token Cumulative Consumption |
   |Number of Tokens Output |Cumulative consumption of output Tokens |
   |Average response duration |Time taken from request initiation to return result (milliseconds) |
