---
title: "Intelligent assistant"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/intelligent-assistant"
---

ByteHouse intelligent assistant provides intelligent Q&A, AI log retrieval, and natural language\-to\-SQL generation capabilities, assisting you in quickly getting started with ByteHouse. The AI log retrieval function supports log retrieval and analysis. It can also convert natural language into log retrieval SQL statements, helping you quickly locate anomalies and improving the efficiency of problem\-solving. The intelligent assistant also supports associating with the knowledge base you create to answer and locate problems more accurately. The natural language\-to\-SQL generation function can convert the natural language you input into corresponding SQL commands. This tutorial introduces how to use Intelligent Assistant.

<span id="5d2d8d3a"></span>
# Feature overview

ByteHouse intelligent assistant relies on ByteHouse’s built\-in knowledge base, enhancing search capabilities to provide knowledge inquiry and problem\-solving services covering product usage and business knowledge scenarios. Meanwhile, the intelligent assistant supports linking your created knowledge bases, combining your business and industry knowledge for more precise answers to usage questions and abnormal event analysis, improving problem resolution efficiency. The intelligent assistant currently focuses on ByteHouse product knowledge Q&A and does not support consultations on other products or fields.

ByteHouse intelligent assistant helps data developers, database administrators, and analysts improve work efficiency and applies to the following scenarios:


* **Intelligent Q&A**: Intelligent assistant can quickly resolve issues you encounter using ByteHouse.

* **AI log search**: Intelligent assistant supports log insights, summarizes key log points, analyzes potential problems, and provides optimization suggestions. The intelligent assistant also converts your natural language commands into SQL statements and searches the corresponding logs.

* **Generate SQL using natural language**: By asking questions to the intelligent assistant in natural language, the intelligent assistant will generate corresponding SQL statements. It supports functions such as generating example query statements and optimizing SQL queries.


<span id="f5cdf7e4"></span>
# Usage restrictions

This feature is in Beta. To use it, you can submit a ticket or contact the ByteHouse team for white list access.

<span id="8aa87523"></span>
# (Optional) Prerequisites

ByteHouse intelligent assistant supports linking [Knowledge base](https://docs.byteplus.com/docs/bytehouse/knowledge-base). To link a knowledge base within the assistant, ensure you have completed the following preparations:


* You have obtained knowledge base management permission. You can check your knowledge base management permission by ByteHouse Cloud Data Warehouse Console \> **Access control** \> **Users** \> **Your username** \> **Resource privileges** path. If you have not been authorized yet, please contact the administrator for authorization.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5c9dfa46cd34e1db0d3f99f41a51d08~tplv-goo7wpa0wc-image.image) </span>

* You have created a knowledge base. For more details, refer to [Quick start: Create and import a knowledge base](https://docs.byteplus.com/docs/bytehouse/knowledge-base#ab13513a).


<span id="56d2c932"></span>
# Use ByteHouse intelligent assistant

<span id="1c74d607"></span>
## Intelligent Q&A

ByteHouse includes a default knowledge base that answers questions related to ByteHouse products. You can quickly obtain ByteHouse\-related knowledge by asking the intelligent assistant.

On any page of the ByteHouse console, click **Intelligent assistant**, enter your question, and click the send button to get related knowledge.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f6daa24565294eabb8a4680d1b8ac087~tplv-goo7wpa0wc-image.image) </span>

You can also click the **Knowledge base** button in the intelligent assistant input box, select the corresponding knowledge base, and get precise answers combined with your business knowledge base.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d6428180f5ce4d168a7fb0290d526de4~tplv-goo7wpa0wc-image.image) </span>

<span id="8a5c9376"></span>
## AI log search

The intelligent assistant offers AI log search and analysis, supporting log insight and SQL statement generation. You can use it together with the [Log retrieval analysis](https://docs.byteplus.com/docs/bytehouse/log-retrieval-analysis) feature to improve log search and analysis efficiency.

<span id="69a84a10"></span>
### Log insight


1. In the ByteHouse console, click **SQL worksheet**, then click the **Log search and analysis** button to enter the **Log search and analysis** page. On this page, click **Intelligent assistant**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7842f8b38a28414a94e01b038e2f12c7~tplv-goo7wpa0wc-image.image) </span>

2. After generating the log search results according to the operations in [Log retrieval analysis](https://docs.byteplus.com/docs/bytehouse/log-retrieval-analysis), click the **Log Insight** on the right of **Data details**. The system automatically generates insight commands and analyzes the current search results automatically, identifies potential problems, and provides optimization suggestions for you to apply as needed.

   You can also click the \*\*Knowledge base \*\*button in the intelligent assistant input box to select your knowledge base to help the intelligent assistant to better understand log issues and improve log search accuracy.

   For more detailed analysis, you can continue entering insight commands in the input box, and the intelligent assistant will continue analyzing for you.


<span id="4ce775d0"></span>
### Generate SQL statements

Click the first icon at the bottom left of the input box, select **Generating SQL Statements**, enter a natural language command, and click the **send** button. The smart assistant will automatically generate corresponding SQL search statements. You can click **Inquire**, and the system will retrieve and display the corresponding log details for you.

The following example queries logs within the specified time frame that contain specified keywords:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f9005e9dcb4944a18affaba77eb4593f~tplv-goo7wpa0wc-image.image) </span>

<span id="4680eeff"></span>
## Generate SQL using natural language

ByteHouse intelligent assistant supports generating SQL statements from your natural language input, and provides features such as generating query sample statements, SQL query optimization, and many other features. You can use natural language to provide content such as table structure, field type, business scenarios, and more. The intelligent assistant will automatically generate the corresponding SQL statements.

On any page of the ByteHouse Console, click **Intelligent assistant**, enter a natural language command in the input box, and click the **Send** button. The Smart Assistant will automatically generate the corresponding SQL statement.

You can copy the statement, replace the placeholders with actual information, and then execute the statement at **SQL worksheet**.

**Example**: Generate a sample query statement

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9722280659604a8a974af362eb320afb~tplv-goo7wpa0wc-image.image) </span>
