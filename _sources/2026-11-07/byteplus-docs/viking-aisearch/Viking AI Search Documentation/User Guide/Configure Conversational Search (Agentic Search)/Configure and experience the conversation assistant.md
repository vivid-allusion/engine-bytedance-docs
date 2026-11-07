---
title: "Configure and experience the conversation assistant"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Configure_and_experience_the_conversation_assistant"
---

<span id="75f2ad10"></span>
# Overview of Conversational Search Assistant features

The Conversational Search Assistant is an advanced feature that uses **proactive reasoning** and **tool\-calling** to understand complex user requests. It searches across diverse data sources, including text, images, and video, to synthesize information and provide precise, context\-aware answers for various scenarios like e\-commerce recommendations and video content Q&A.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/32de818484dc45629ae6b18e3727b6af) </span>

&nbsp;

For image & text datasets and video applications, the Conversational Search Assistent supports the following scenario features:


| |**Image and text applications**<br><br>> Applications associated with graphic and text datasets |**Video applications**<br><br>> Applications associated with video datasets |
|---|---|---|
|**Knowledge data sources** |* **Image and text dataset:**  Linked to the application’s graphic and text dataset, allowing the agent to search, read, and summarize both text and image information within the dataset.<br><br>* **Document dataset:**  Linked to the document content in the application’s document dataset. Useful for supplementing industry knowledge, brand information, platform policies, and other information during the assistant’s Q&A process. |* **Video metadata:**  Metadata stored in the video dataset linked to the application, such as video titles, summaries, cast, and directors<br><br>* **Video audio\-visual text data:**  Derived from actual video files after processing by Large Models (LLMs). This includes **audio\-visual\-text "slices"**  (segmentation). In scenarios involving multi\-level media data with series and episodes, the model understands hierarchical relationships to enable cross\-episode understanding under the same series<br><br>* **Document data:**  Document content linked to the application's document dataset Provides supplementary information such as industry knowledge, brand knowledge, and platform policies during assistant Q&A sessions |
|**Supports Q&A scenarios** |**E\-commerce scenarios:** <br><br><br>* **Product recommendation:**  Analyzes user needs and recommends products on the platform, including general category recommendations and scenario\-based suggestions<br><br>* **Product content Q&A:**  Answers user questions about product parameters, functions, and usage based on the product dataset<br><br>* **Shopping guides:**  Combines information from the product dataset with platform and industry knowledge to provide users with "how to choose" and "which is better" style guides and Q&A |**Video platform scenarios:** <br><br><br>* **Conversational Video Recommendation:**  Parses complex user requests (e.g.,  *"Find me a sci\-fi movie with a melancholic atmosphere and a minimalist aesthetic"* ) to recommend matching video assets.<br><br>* **Plot Interpretation & Q&A:**  Analyzes video content to answer user queries regarding **plot development, character relationships**, or **key narrative events. ** For every answer provided, the assistant returns **high\-light fragment positioning**, allowing users to jump directly to the relevant scene.<br><br><br>**Video course scenarios:** <br><br><br>* **Curriculum Search & Recommendation:**  Analyzes the user's learning objectives or knowledge gaps to recommend the most suitable course series or modules.<br><br>* **Course Content Q&A:**  When users ask about specific knowledge points, the Agent generates responses based on the **multimodal content** (audio, visual, and captions) within the course videos.<br><br>* **Precision Timestamping:**  The assistant provides **exact timestamp links** to the corresponding sections within the video, enabling a "point\-to\-point" learning experience. |


<span id="a698cdcf"></span>
# Experience and configure the conversation search assistant

Once there is an active dataset in the application, you can start configuring the conversation experience. Go to the **Application \> Experience Center \> Conversation Experience** tab in the console to start configuring and testing the conversation.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/3cc7c67d465f4582bb93e0358a5976ab) </span>

&nbsp;

<span id="6727b50c"></span>
# Triggering Search within Conversations

During a conversation, when a user's intent requires retrieving specific item information from your datasets to provide an answer, the Conversational Search Assistent **automatically ** **initiate** ** a search request**. It intelligently queries all datasets associated with the application, retrieves relevant results, and synthesizes them into a smart, context\-aware response.

**Strategy Inheritance:**  When a search is triggered, the system utilizes the **Search Strategies** you have previously configured in the  **[Search Experience]** . These settings directly determine the search quality, which in turn impacts the assistant's ability to satisfy user intent and ensure accurate information delivery. Please consider the following association strategy configurations when setting up conversations:


* Configure reasonable data indexing in the application: see [Configure Search strategy](https://docs.byteplus.com/docs/393/Configure_search_strategy)
