---
title: "Building an Enterprise Intelligent Customer Service Assistant"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Building_an_Enterprise_Intelligent_Customer_Service_Assistant"
---

Taking financial knowledge base as an example, this paper introduces how to build an intelligent customer service assistant (intelligent question answering tool) based on the core capabilities of the large model and through the enterprise knowledge engine, so as to realize the functions of knowledge import and intelligent response.

<span id="7881b067"></span>
# Create a knowledge base


1. Log into the Marketing Agent console and select **Enterprise Knowledge Engine** in the left navigation bar.

2. In the left navigation bar of Enterprise Knowledge Engine, select **Knowledge Management** \> **Knowledge Base** .

3. Added knowledge base. Fill in the basic configuration information, click **Save** when done, and complete the creation of the new knowledge base.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6389f9f7f1b743aaaff5880fc010f09a~tplv-goo7wpa0wc-image.image) </span>

   The specific parameter configuration instructions are as follows:

   
   |parameter |parameter description |example |
   |---|---|---|
   |name |Knowledge base name |XX Bank Intelligent Assistant Knowledge Base Demo |
   |describe |Briefly describe the purpose or content of the enterprise knowledge engine (limited to 200 words). |XX bank intelligent assistant |
   |content type |Select the type of knowledge base. Currently, the following five types are supported:<br><br><br>* General content: Support uploading files, importing from WeChat library, importing from object store, importing from relational database.<br><br>* Query cache: Support XLSX, CSV and other format files.<br><br>* QA Q & A: Support XLSX, CSV and other format files.<br><br>* Terminology: Supports XLSX, CSV and other formats.<br><br>* Customer data: used to create a principal repository that supports uploading principal data already in VeCDP. |generic content |
   |Whether to update knowledge regularly |No update required: One\-time import, no need to update data later.<br><br>Timed update: Support setting the update frequency according to the day/week/month granularity, and specifying the specific update time. If there is no 31st day of the month, the date is skipped. Timely update of task execution, you can view the status of knowledge updates through each knowledge update time on the knowledge management page in the knowledge base.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a259065abe34453bd936f6a01a3efad~tplv-goo7wpa0wc-image.image) </span> |No update required |
   

4. Click on the new knowledge base to enter the knowledge base details page. Click **Import Knowledge** and select **Upload File.** 

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/634b9d52d95945148215756d38ff0dc5~tplv-goo7wpa0wc-image.image) </span>

5. Upload files directly as knowledge base content. Then click **Next** .

   Uploaded documents include: branch information, financial risk disclosure and product manuals, financial agreement documents, product sales documents, and product additional instructions.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e7f9b657e5f0403ca5045f2412c2fcbe~tplv-goo7wpa0wc-image.image) </span>

6. To configure the knowledge segmentation method, select the default configuration method, and then click Finish. Please refer to the specific parameter details [Import Knowledge](https://docs.byteplus.com/docs/dataagent/Import_Knowledge).

   After the import is successful, all file content is automatically segmented and displayed on the Knowledge Base Content page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/82bd0dd76ce445afab783b6814d2a728~tplv-goo7wpa0wc-image.image) </span>


<span id="78ac41b8"></span>
# Create a quiz app


1. Select **Search Apps** in the left navigation bar and tab New App on the **Q & A Apps** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc85ae75ead743c79b6a3bdc0cc7e693~tplv-goo7wpa0wc-image.image) </span>

2. On the app's orchestration page, set the basic information. See the details of the parameters [Step1: Create an API application](https://docs.byteplus.com/docs/dataagent/User_Case_Knowledge_Q_A_Scenario#67a94136).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1acee04c6d554f40b7d736b402aacfb4~tplv-goo7wpa0wc-image.image) </span>

   
   |parameter |Example of parameters in this article |
   |---|---|
   |Configuration basic information |\*\* Smart Q & A app |
   |Referred Knowledge Base |Click **Add Knowledge Base** and select the bank knowledge base created in the previous step. |
   |selection model |Select the Doubao model |
   |Set the opening line |Hello! I'm your assistant, how can I help you? |
   |empty reply |/ |
   |similarity threshold |0.2 |
   |keyword similarity weight |0.7 |
   |Top N |30 |
   |multi\-round dialogue optimization |open |
   |Number of dialogue rounds |20 |
   |variable |Knowledge is optional. |
   |temperature |Open, 1 |
   |Top P |0.7 |
   |frequency penalty |close |
   |There are penalties |close |
   |Maximum Number of Tokens Generated |512 |
   

3. On the app's choreography page, set the prompt word information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f5b5caa5dfd241adb5ce08de55037a2e~tplv-goo7wpa0wc-image.image) </span>

   The example of this article is as follows:

   ```Markdown
   # Role
   You are a friendly and approachable customer service knowledge assistant of Rural Commercial Bank, providing accurate and detailed answers to various knowledge questions about Rural Commercial Bank's financial products with a warm and approachable attitude.
   
   ## Skills
   ### Skill 1: Answer product knowledge questions
   1. When users ask questions about the knowledge of rural commercial bank related wealth management products, the first step is to search for relevant content from the knowledge base.
   2. If there is relevant information in the knowledge base, it is necessary to provide a detailed list of the data in the knowledge base for answering. At the same time, the language style should be friendly and natural, and more colloquial expressions should be used to bring the user closer.
   3. If all the content in the knowledge base is unrelated to the question, the answer must clearly include the sentence "Dear, the answer you are looking for was not found in the knowledge base!" and express an attitude of trying to help the user as much as possible.
   4. During the answering process, it is necessary to fully consider the chat history.
   
   ## Restrictions:
   - Only answer questions related to agricultural and commercial bank product knowledge, refuse to answer irrelevant topics, and use friendly and tactful refusal methods, such as "Dear, let's mainly talk about agricultural and commercial bank product knowledge, this topic is not very relevant".
   - The answer should provide a detailed list of knowledge base data (if any), ensuring that the answer content is complete, accurate, and the language style is friendly and natural.
   - The answer must conform to logic and language expression habits, and convey a friendly and enthusiastic feeling.
   
   The following is the knowledge base：
    {knowledge}
   The above is the knowledge base
   ```
   

4. In the **debugging and preview** area, you can simulate and inquire by yourself, accept the application effect, and readjust the parameter configuration based on the effect.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a4a94c1ce3a34e26ad7f105687652dc6~tplv-goo7wpa0wc-image.image) </span>

5. Once all the configuration is complete, click on the top right corner **Save and publish.** 


<span id="d2a8474b"></span>
# Publish App


1. Click Create a **Publish** app.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/489cd31be1044a009b27e9cec2d0104f~tplv-goo7wpa0wc-image.image) </span>

2. Select the form of Web page publishing and click the Copy icon.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/55379e83f7884289b0182a89f36ba25c~tplv-goo7wpa0wc-image.image) </span>

3. Paste this link in your browser to access the created customer service assistant app.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f905272a659451c9065130e07ea9a73~tplv-goo7wpa0wc-image.image) </span>


<span id="b66ff057"></span>
# Verification effect

You can have a conversation with the intelligent customer service assistant, and the assistant will provide you with relevant knowledge answers based on the content of the uploaded file.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/00628716577e4ce5ab4fde513c029575~tplv-goo7wpa0wc-image.image) </span>
