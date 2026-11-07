---
title: "Audit"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Audit"
---

The audit module provides two core features: **usage records** and **query records**, enabling comprehensive tracking and review of agent operations.


* Usage records: You can gain an overview of agent invocation activities.

* Query records: You can examine the detailed content of each conversation round, user feedback, and operational status. This data helps with troubleshooting, behavior analysis, and resource management, ensuring agent operations are transparent and controllable.


<span id="6543ce60"></span>
# Usage records


1. After logging in to the BytePlus console, click Intelligent Analysis Agent, select a project, and access the agent list. Under the corresponding agent, click the **Agent configuration** button to enter the agent configuration page.

2. In the left navigation bar of the agent configuration, click the audit module, then on the right page, click the **Usage records** tab to view usage records. Usage records support viewing information such as today's DAU, yesterday's DAU, this week's WAU, last week's WAU, DAU trends, WAU trends, and more. You can filter by time range.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e86e332aeb54a799d91b11586d096fe~tplv-goo7wpa0wc-image.image) </span>

<span id="df36153d"></span>
# Query records


1. After logging in to the BytePlus console, click Intelligent Analysis Agent, select a project, and access the agent list. Under the corresponding agent, click the **Agent configuration** button to enter the agent configuration page.

2. In the left navigation bar of the agent configuration, click the audit module, then click the query records tab to view query records.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/11602700286649898edc8475a32b81bf~tplv-goo7wpa0wc-image.image) </span>


3. In the query records list, you can view detailed information related to query records. You can set query date, user, mode, query terminal, session ID, and status as filter conditions for the query records you want to view.

   Caution: When the filter condition is 'mode', the corresponding list information for intelligent queries or in\-depth research will differ. The descriptions of specific query record list items are as follows:

   
   |List item name |Description |
   |---|---|
   |Time |The specific date and time when the agent user initiated the query. |
   |Username |The account of the agent user who initiated the query. |
   |Mode |The analysis mode used when asking questions (intelligent query/deep research). |
   |Question |The specific content of the question asked by the intelligent agent user. |
   |Conversation ID |The unique identifier for each conversation, used to associate multiple rounds of Q&A within the same conversation. |
   |Question terminal |The device or platform used by the intelligent agent user (Feishu/web client/push/OpenAPI). |
   |Status |The result status of question processing (success/failure). |
   |Dataset |The data table or data source associated with or queried during this question.<br><br>Caution: When the mode type is deep research, this column is not displayed. |
   |Like/dislike |The feedback from the intelligent agent user on the answer (like or dislike), used to evaluate answer quality.<br><br>Caution: When the mode type is deep research, this column is not displayed. |
   |Feedback |Detailed written feedback submitted by the intelligent agent user.<br><br>Caution: When the mode type is deep research, this column is not displayed. |
   |Single/multiple rounds |Indicates whether this question belongs to a single\-round Q&A or is one round in a multi\-round conversation.<br><br><br>* Single\-round conversation: A conversation under the same conversation ID that contains only one question.<br><br>* Multi\-round conversation: A conversation under the same conversation ID that contains multiple questions. |
   |Details |Administrators with access to all datasets bound to the intelligent agent can click the list details, process details, or result details buttons to view different detailed information:<br><br><br>* When the mode type is deep research, click the details button in the details column to view the process details and result details.<br><br>* When the mode type is intelligent query, you can click the process details or result details button as needed to view the corresponding process details or result details. |
   


&nbsp;
