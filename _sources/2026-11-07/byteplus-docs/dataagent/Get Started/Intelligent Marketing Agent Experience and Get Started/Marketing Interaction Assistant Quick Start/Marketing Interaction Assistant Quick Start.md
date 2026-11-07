---
title: "Marketing Interaction Assistant Quick Start"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Marketing_Interaction_Assistant_Quick_Start_"
---

Intelligent conversation assistant is a conversation marketing hub that integrates real\-time customer portrait insights and AI decision engine, including enterprise knowledge engine, conversation insights and other functions. Enterprise knowledge engine is the underlying capability of intelligent conversation assistant, and enterprise knowledge engine function provides full\-process knowledge construction, management capabilities and intelligent AI application capabilities. This article shows you how to quickly set up and use an intelligent conversation assistant.

<span id="fe357abf"></span>
# Create a new knowledge base


1. After logging in to the Intelligent Marketing Agent page with the account password, find the "Intelligent Conversation Assistant" service card and click "Experience Now".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c20111ebcc44af29679d0b6b07d6d7f~tplv-goo7wpa0wc-image.image) </span>

2. Go to the Enterprise Knowledge Engine page and click "Knowledge Base" in the top navigation bar.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50a2b154b3794a62a6f1c8012fe87ea8~tplv-goo7wpa0wc-image.image) </span>

3. On the Enterprise Knowledge Engine Management page, click "Add Knowledge Base", fill in the basic configuration information, and click "Save" after completion to complete the creation of the new knowledge base. Take the example of creating a knowledge base of generic content types.

   
   |parameter |parameter description |example |
   |---|---|---|
   |name |Knowledge base name |Automotive Knowledge Base |
   |describe |Briefly describe the purpose or content of the enterprise knowledge engine (limited to 200 words). |Car related content |
   |content type |Select general content, support uploading files, importing from WeChat library, importing from object store, importing from relational database |generic content |
   |knowledge analysis model |It is used to convert natural language into vectors, perform semantic retrieval, and generate QA questions. It is currently standard as Doubao\-embedding, and also supports adaptation to your other vectorized models. |Doubao\-embedding |
   |Whether to update knowledge regularly |* No update required: One\-time import, no need to update data later.<br><br>* Timed update: Support setting the update frequency according to the day/week/month granularity, and specifying the specific update time. If there is no 31st day of the month, the date is skipped. Timely update of task execution, you can view the status of knowledge updates through each knowledge update time on the knowledge management page in the knowledge base.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3464fd2000da4608b6944683c5b9cca4~tplv-goo7wpa0wc-image.image) </span> |No update required |
   


<span id="8ede2566"></span>
# Import knowledge


1. Click on the new knowledge base to enter the knowledge base details page.

2. Click the " **Import Knowledge**" button to upload the knowledge file  **.** 

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca1adc307f6944299fe973759c59c3a5~tplv-goo7wpa0wc-image.image) </span>

3. Select the import method as Upload File, select the folder as the save path, and upload the relevant knowledge documents.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The currently supported upload formats include doc, docx, pdf, pptx, txt, md, html, json, xlsx, csv, png, jpg, etc. You can upload up to 10 files at a time, and a single file does not exceed 100M.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The system will automatically create a folder named after the knowledge base name based on the knowledge base you created as the default save path. If you need to save in another folder, you can create a new folder on the Knowledge Management page.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c127e5bc150f42b9a0db929c2478af18~tplv-goo7wpa0wc-image.image) </span>

4. After the upload is successful, click "Next", enter the knowledge segmentation configuration, configure relevant parameters, and click "Finish".

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Knowledge segmentation is the process of dividing long documents into smaller units that are easier to process and retrieve models. Reasonable configuration helps to improve the accuracy and efficiency of retrieval.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e0729f91356749a4976d9ed06b9e885c~tplv-goo7wpa0wc-image.image) </span>

   
   |**parameter** |**parameter description** |**default configuration** |
   |---|---|---|
   |**automatic keywords** |Extract the number of keywords in the segment and extract N keywords for each block to improve its ranking score. 0 means automatic extraction, up to 30 |0 |
   |**automatic question** |Automatically split the number of questions for question answering, extract N questions for each block to improve its ranking score, 0 means the system automatically splits, up to 10 |0 |
   |**split strategy** |* Based on plain text segmentation: based on plain text segmentation, without relying on any rich text format, only based on the natural boundaries of characters, punctuation, newlines, etc. in the text content, the long text is divided into shorter fragments. This method is often used in NLP preprocessing, RAG systems, document indexing, etc. The core is to preserve semantic coherence and adapt to model input constraints.<br><br>* Segmentation based on [paragraph/paragraph]: Taking the "paragraph" in the text as the natural segmentation unit, the long document is directly split into independent paragraph fragments, which is suitable for scenes that respect the original paragraph structure and semantic boundaries of the text and do not destroy the logical coherence within the paragraph.<br><br>* Segmentation based on document logical structure (document tree/chapter): According to the hierarchical organization framework of the document itself, the long document is divided into fragments corresponding to logical units such as "chapters, sub\-chapters, and subsections". It is suitable for scenarios where this framework needs to be followed to maximize the integrity of the document's knowledge system. |Segmentation based on document logical structure (document tree/chapter) |
   |**character length** |The character length of each block, in bytes. |512 |
   |**Whether to recognize PDF forms** |Controls whether to parse table data in PDF: Open to extract table structure information, close to process only plain text. |open |
   |**Whether to recognize PDF images** |After opening, the system will use the OCR tool to convert the PDF image to text, and then import it into the knowledge base. |open |
   |**PDF page limit** |The maximum number of pages to process a PDF at a time, and the excess part is automatically truncated: it is suitable for processing large files in batches to avoid memory overload. |1000 |
   |**Whether to merge small chunks** |Effective only when the split policy is paragraph: Automatically merge adjacent small paragraphs (character count < threshold) when turned on, reducing fragmentation. |open |
   |**Whether to parse scans** |Controls whether recognition of scans is enabled, and if turned off, only copyable text is processed. |open |
   |**Whether to use a pdf outline for chapter understanding** |Whether to intelligently identify the chapter structure based on the PDF catalog (Outline): Open to improve the accuracy of long document chapter segmentation. |open |
   |**custom separator** |* The current system uses the default delimiter (period/paragraph) for import knowledge content segmentation.<br><br>* If you also want to use other separators for splitting, you can configure a custom separator here. The custom separator takes precedence over the default separator.<br><br>* Support to add multiple custom delimiters, and use " |" to separate multiple custom delimiters, for example: `!\|?\|。` `\|####`。 |
   |**Whether to return as Markdown** |Control result format: return to structured Markdown format on, return to plain text on. |open |
   |**Markdown whether to fold** |Controls whether Markdown collapses. |close |
   |**Excel parsing whether to enable table recognition** |Controls whether to parse table data in Excel: On to extract table structured information, off to process only cell text. |open |
   |**Timeout for converting images** |The maximum time to convert images in pptx/ppt parsing, in seconds |60 |
   |**Use full\-page ppt images instead of small images** |After opening, in the ppt\-like file, use a full\-page ppt image instead of a small image to completely retain the layout, content logic, and visual details of the original PPT, and avoid the information being cropped or blurred due to the scaling of the small image. |close |
   |**Whether to use vlm capability** |VLM visual language model (Vision\-Language Model), including chapter understanding, picture understanding and so on. Once turned on, the system can recognize and understand the content of the image, and analyze it in combination with text; otherwise, only plain text is processed. |open |
   |**The maximum level of chapter expectations** |Force the maximum title level of document tree parsing (e.g. 2 means only secondary titles are recognized) to avoid interfering with semantics at too deep a level. |60 No default configuration |
   |**Document deduplicate** |After opening, the system will verify whether the content of the uploaded file is duplicate with the existing file in the knowledge base. If there is a duplicate, it cannot be uploaded. By verifying file MD5, only fully duplicated files are considered duplicates. |close |
   

5. After the knowledge segmentation configuration is completed and submitted, the knowledge import task begins to execute. The Knowledge Base Management list page displays the knowledge processing status, such as processing in progress, processing success, and so on.


<span id="da8f60fb"></span>
# Building an AI customer service application


1. Click "AI Application" in the navigation bar, click "New Application", you can directly enter the application name and description in the pop\-up window, and click Save.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ab4830188b943d885a038c0debd4d0c~tplv-goo7wpa0wc-image.image) </span>

2. On the Knowledge Base Edit page, click "+ Add Knowledge Base" and select the created knowledge base.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6291332a69f44f08b2df3c0e1350d589~tplv-goo7wpa0wc-image.image) </span>

   
   |parameter |explain |
   |---|---|
   |Configuration basic information |The application avatar, application name and description can be changed. |
   |Referred Knowledge Base |Configure enterprise knowledge engine association, support multi\-enterprise knowledge engine joint call. |
   

3. Complete the configuration on the orchestration page for creating an API app.

   
   |**parameter** |**parameter description** |**default value** |**tuning ideas** |
   |---|---|---|---|
   |selection model |Currently supports bean buns and DeepSeek series models. | | |
   |Set the opening line |You can define the opening remarks in the initial state by yourself. |Hello! I'm your assistant, how can I help you? | |
   |empty reply |After configuration, if the user's question is not retrieved in the Enterprise Knowledge Engine, the content configured here is used as the answer. If you want to provide your opinion when nothing is retrieved, please leave this blank. |empty | |
   |similarity threshold |Adjust according to specific application requirements. A higher threshold decreases the number of matches, but increases accuracy; a lower threshold increases the number of matches, but may decrease accuracy. |0.2 |If it is a precise question and answer for professional fields, such as law and medicine, the similarity threshold can be appropriately increased to 0.3\-0 to ensure that the recalled content is highly relevant to the problem; if it is a broad question and answer in general fields, such as life common sense, it can be kept at 0.2\-0 to obtain more potentially relevant content. |
   |keyword similarity weight |Adjust the weights according to the importance of the keywords. Key words that are important can be given higher weight to ensure that they account for a greater proportion of similarity calculations. |0.7 |In the professional domain, the keyword similarity weight can be increased to 0.8\-0 because the accuracy of the keyword is crucial; in the general domain, the vector cosine similarity may better capture the flexibility of semantics, and the keyword similarity weight can be set to 0.6\-0. |
   |Top N |Increasing N may provide more options, but it may also introduce more irrelevant results. Adjust according to the required diversity and accuracy. |30 |Specialized field problems may require more accurate results, and the Top N can be set to 10\-20; in general field, to provide users with more choices and references, the Top N can be set to 30\-50. |
   |multi\-round dialogue optimization |Control whether to enable multi\-round conversation context association optimization: enable to preserve historical conversation information and improve the semantic coherence of long conversations. |open |You can refer to the necessity of the scene to open it. If it is a precise question and answer for professional fields, it is recommended to open it to ensure coherent semantics and professional logic; if it is a broad question and answer in general fields, such as common sense, it can be kept dynamically open (only enabled when the process is guided). |
   |Number of dialogue rounds |The maximum number of rounds of historical dialogue is preserved, and earlier information beyond the number of rounds will be cleared to avoid context redundancy. |20 |If it is a precise question and answer in a professional field, it can be set to 20\-30 rounds in order to maintain the complete professional dialogue chain and ensure that the recalled content is highly relevant to the question. If it is a broad question and answer in a general field, such as life knowledge, it can be kept at 10\-20. |
   |variable |The name of a context variable passed in multiple rounds of dialogue to store intermediate results or user\-defined parameters (e.g. knowledge is identified by the enterprise knowledge engine). |knowledge |If the dialogue system only needs to refer to the relevant content in the enterprise knowledge engine, only the customized knowledge can be identified as the enterprise knowledge engine; if there are other variables in the dialogue, you can customize the parameters according to your needs. |
   |temperature |For tasks that require creativity and variety, increase the temperature; for tasks that require certainty and consistency, decrease the temperature. |1 |If you want to get an accurate, standard answer, the temperature can be set to 0.5\-0; to stimulate some innovative, open\-ended answers, you can increase the temperature to 0.8\-1. |
   |Top P |It is usually used in combination with temperature. Higher P\-values increase diversity, while lower P\-values increase certainty. |0.7 |For answers that require strict adherence to facts and norms, the Top P can be set to 0.6\-0; for creative, open\-ended questions, the Top P can be set to 0.8\-0. |
   |frequency penalty |Increasing the frequency of punishment can reduce repetition, but excessive punishment can lead to the loss of important information. |0 |Generally, it can be adjusted according to the specific generation results. If there are more duplicate content, the frequency penalty and the existence penalty can be appropriately increased, such as 0.1\-0. |
   |There are penalties |Similar to the frequency penalty, it is adjusted moderately to balance repetition and variety. |0 ||
   |Maximum number of tokens |Do not exceed the maximum number of tokens corresponding to the selection inference model. This number of tokens limits the length of each answer question. If it exceeds, the model will have the word "continue", and the input will continue to output content |512 |For short questions, the maximum number of tokens can be set to 256\-384; for complex questions or situations that require detailed explanation, it can be set to 512\-1024. |
   

4. Configure prompt words. In the **prompt word** area, you can optimize the prompt word yourself, such as character design, answer length and answer language.

5. In the **debugging and preview** area, you can simulate and inquire by yourself, accept the application effect, and readjust the parameter configuration based on the effect.

6. Once all the configuration is complete, click **Save and Publish** .


<span id="502156f5"></span>
# Release AI customer service application

On the AI application page, click "Release" of the corresponding application and select the **Web page** to complete the release of the AI customer service application.

Currently supports **Web pages, API** two publishing methods. This article takes publishing a Web page as an example.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cecbd59f064a46f4beb29dadaaa391b3~tplv-goo7wpa0wc-image.image) </span>

<span id="fee842ec"></span>
# Use AI customer service app

Publish as Web, you will get a dedicated URL, copy the link, and open it in your browser to use the app.

You can directly enter questions to get the answers you need, or you can upload attachments on the webpage to answer questions. (Uploading attachments is only supported for apps created using the doubao\-1\-5\-vision\-pro\-32k model.)

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/38080e0fd828430c842970b42526571b~tplv-goo7wpa0wc-image.image) </span>
