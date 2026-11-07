---
title: "Search Application"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/search-application"
---

Enterprise knowledge engine supports creating agent and correlating knowledge base. By building\-debugging\-publishing retrieval application, enterprise knowledge engine OpenAPI can be called later to integrate retrieval application in external system to realize knowledge retrieval and question answering capability.

For example, in a customer service/shopping guide scenario, the search application of the enterprise knowledge engine can accurately identify needs, generate intelligent speech skills, and provide personalized product recommendations, enabling full\-link task automation from demand analysis to after\-sales support.

# New search application

1. Log in to the Marketing Agent console.

2. Select **Enterprise Knowledge Engine** in the left navigation bar.

3. In the left navigation bar of Enterprise Knowledge Engine, select **Search Application**.

4. On the right side of the **Search Application** page, click **New Search Application**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4fbb8e6534114d6d8a5b9aa7c64dc894~tplv-goo7wpa0wc-image.image)

5. In the **New Search Application** pop\-up window, customize the **name** and **description**, and click **Save**.

6. On the left side of the application detailed configuration page, complete the following configuration.

   |**Configuration item** |**Description** |
   |---|---|
   |Basic information |That is, the name and description filled in in the previous step, which support modification. |
   |Cite knowledge |1. Click  **+ Knowledge Base** to select the specified knowledge base, folder, or knowledge from the knowledge base as the data source for the current application.<br><br>2. Click the  **+ knowledge tag**, narrow the search range through the knowledge tag, and only hit the content that meets the label conditions. Multiple values within the same label are "or" relationships, and different labels are "and" relationships. If "Select" Department = Sales/Marketing "+" Language = Chinese ", the document" Sales or Marketing Department "and" Language is Chinese "will be hit.<br><br>3. Click **Edit Weight** to support editing knowledge base priority (priority order P0 \> P1 \> P2). When retrieving, the content of the high\-priority knowledge base will be returned first. When there are enough matching results in the high\-priority knowledge base, low\-priority content will not be included. The default weight priority is P0. If the data source is deleted or no longer referenced by the application, the weights are automatically cleared. |
   |Search |* Vector search weight: Adjust the proportion of keyword matching and semantic understanding. The lower the value, the more attention is paid to accurate word and sentence hits, and the higher the value, the more attention is paid to the overall semantic relevance.<br><br>* Mixed similarity threshold: the lower bound of relevance score for synthetic semantic matching and keyword matching. It will only be recalled if the mixed similarity of the candidate documents exceeds this threshold. The higher the value, the more accurate the recall result but the smaller the quantity; the lower the value, the wider the recall range but may introduce noise.<br><br>* Sorting strategy: support selection **not sorting**, **semantic model sorting**, **large model sorting**.<br><br>   * Semantic model sorting: Use a dedicated semantic sorting model to re\-sort initial shardings by relevance. Fast and cost\-effective, it is suitable for most scenarios.<br><br>   * Large model sorting: Call the large language model to evaluate the matching degree of sharding to the problem one by one, and the sorting quality is higher, but the speed is slightly slower. It is suitable for scenarios where there are high requirements for answer quality.<br><br>   > **注意**<br>   <br><br>   > To use semantic model sorting and large model sorting, you need to configure the corresponding model in the privatization minibase first. If the model is not configured, the selection of semantic model sorting and large model sorting is not supported.<br>   <br><br>* Number of initial shardings: The number of candidate shardings retrieved from the knowledge base and returned. The higher the value, the wider the coverage of the recall, but it will increase the processing time. This value should be larger than or equal to the number of selected shardings.<br><br>* Sorting score threshold: When the threshold is set, only recall shardings with scores ≥ this threshold are retained, and results below the threshold will be filtered directly and will not participate in the final display. The higher the threshold, the more accurate the results, but the number of recalls may decrease; the lower the threshold, the richer the results, but the less relevant content may be mixed in.<br><br>* Recall segment count: The number of shardings that were finally displayed in the search list and fed to the large model after reordering. The higher the value, the more reference information the model can obtain, but it may introduce noise. |

7. On the left side of the application detailed configuration page, enter the search keyword for recall testing.

   The recall accuracy is evaluated based on the index of recall paragraph sort, reorder score, mixture similarity and so on.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3d0ee5949404d4db8503277cd91f253~tplv-goo7wpa0wc-image.image)

8. After the configuration is complete and the recall test meets the requirements, select **Save** or **Publish** the app in the upper right corner of the app detail configuration page.

   * **Save:**  Do not publish the application, only save the application in the search application list.

   * **Release:**  Publish the application, and then bind the OpenAPI for external systems to call the application.

# Publish search application

1. Log in to the Marketing Agent console.

2. Select **Enterprise Knowledge Engine** in the left navigation bar.

3. In the left navigation bar of Enterprise Knowledge Engine, select **Search Application**.

4. In the Apps list, find the app whose status is **Unpublished**, and click **Publish** in the **operation** column.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d412b0db1625483280c84f4f8bd95a0a~tplv-goo7wpa0wc-image.image)

# Apply for an API for the app.

1. Log in to the Marketing Agent console.

2. Select **Enterprise Knowledge Engine** in the left navigation bar.

3. In the left navigation bar of Enterprise Knowledge Engine, select **Search Application**.

4. Select **API** \> **Apply for API Token** in the top right corner of the list.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8f3bd495a3d4018b86a7b36b9afff3a~tplv-goo7wpa0wc-image.image)

   * You can click **View API Access Documentation** to view detailed interface parameter descriptions.

   * Later, when applying for API to obtain Token, click **View API Token** to quickly redirect to view Token.

5. Jump to the **New Application** page, in **the application can use the API** configuration item, add **retrieval application call** API.

   For details on application management configuration, see [Create an application to call OpenAPI](https://docs.byteplus.com/docs/dataagent/Open_API#0c19c694).

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/63ef4da81e2c4099aa84a672243a7e1d~tplv-goo7wpa0wc-image.image)

6. In the **application management** list, get the Token of the above application.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14892e2091c341b6a2921350a2dd5f1c~tplv-goo7wpa0wc-image.image)

7. The retrieval application can be used in the external system by calling the API in the open capability of the enterprise knowledge engine to connect with the external system.

   For instructions on using open capabilities, see [View open capabilities](https://docs.byteplus.com/docs/dataagent/Open_API#09dbb536).

# Edit/Delete Search Application

1. Log in to the Marketing Agent console.

2. Select **Enterprise Knowledge Engine** in the left navigation bar.

3. In the left navigation bar of Enterprise Knowledge Engine, select **Search Application**.

4. In the operation column of the specified application, the following operations are supported.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68855fa6ee5640ca825307f12d6b123e~tplv-goo7wpa0wc-image.image)

   * **Edit:**  Enter the application details page, support modifying the application configuration items and re\-debugging, and support saving or publishing after no problems.

   * **Delete:**  Apps that are no longer used support deletion, and apps will no longer be available after deletion.

      > **注意**

      > Once the retrieval application is deleted, it cannot be restored. Please proceed with caution.
