---
title: "API-Based Access to Knowledge Base Retrieval Capability"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/api-based-access-to-knowledge-base-retrieval-capability"
---

Taking financial knowledge base as an example, this paper introduces how to build an intelligent retrieval tool through enterprise knowledge engine based on the core capabilities of large model, and realize the functions of knowledge import and intelligent response.

# Step 1: Create a knowledge base

1. Log into the Marketing Agent console and select **Enterprise Knowledge Engine** in the left navigation bar.

2. In the left navigation bar of Enterprise Knowledge Engine, select **Knowledge Management** \> **Knowledge Base**.

3. Added knowledge base. Fill in the basic configuration information, click **Save** when done, and complete the creation of the new knowledge base.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7370383c215146acb3bb425c3bbdb592~tplv-goo7wpa0wc-image.image)

   The specific parameter configuration instructions are as follows:

   |Parameter |Parameter description |Example |
   |---|---|---|
   |name |Knowledge base name |XX Bank Intelligent Assistant Knowledge Base Demo |
   |describe |Briefly describe the purpose or content of the enterprise knowledge engine (limited to 200 words). |XX Bank Intelligent Assistant |
   |content type |Select the type of knowledge base. Currently, the following five types are supported:<br><br><br>* General content: Support for uploading files, importing from WeChat library, importing from object store, importing from relational database.<br><br>* Query cache: Support XLSX, CSV and other format files.<br><br>* QA Q & A: Support XLSX, CSV and other format files.<br><br>* Terminology: Supports XLSX, CSV and other formats.<br><br>* Customer data: used to create a principal repository that supports uploading principal data already in VeCDP. |generic content |

4. Click on the new knowledge base to enter the knowledge base details page. On the **Knowledge Management** page, click **Import Knowledge**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dbda8130e87443918e045931211efb41~tplv-goo7wpa0wc-image.image)

5. Select the **common document** import method.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/576a255ac46b4bba8eb7b264dec951d5~tplv-goo7wpa0wc-image.image)

6. Set the file save path and upload the file as Knowledge Base content. Then click **Next**.

   Uploaded documents can include: branch network information, financial risk disclosure and product manuals, financial agreement documents, product sales documents, and product additional instructions.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/060a8a2ba2814ac7b5a96a0ff7c593f7~tplv-goo7wpa0wc-image.image)

7. Configure the knowledge segmentation method, select the **automatic segmentation** method, and then click **Finish**.

   See the specific parameter details [Import Knowledge](https://docs.byteplus.com/docs/dataagent/Import_Knowledge).

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c0a7115ce3c042f388df8877d392a374~tplv-goo7wpa0wc-image.image)

   After the import is successful, all file contents will be automatically segmented and viewed on the **knowledge management** page after the parsing is completed.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a2ab8b4b8afe4d9aa9a5b24bce38f709~tplv-goo7wpa0wc-image.image)

   Click on the knowledge name to enter the knowledge details page to view the segmentation details.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/819bcb912edb4bad9de81e041a7a9ce8~tplv-goo7wpa0wc-image.image)

# Step 2: Create a search application

1. Select **Search Application** in the left navigation bar of Enterprise Knowledge Engine and create a new application.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5a024b29a2c436aae80d05bb4133b16~tplv-goo7wpa0wc-image.image)

2. Custom Settings Retrieve the name and description of your app and click **Save**.

   For example:

   * Name : XX Bank Financial Assistant

   * Description: XX intelligent question answering application

3. On the left side of the app choreography page, set the search parameters.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e7fa46e50624a84a1310f36803701fc~tplv-goo7wpa0wc-image.image)

   |**Parameter** |**Parameter description and example values** |
   |---|---|
   |basic information |* Name : XX Bank Financial Assistant<br><br>* Description: XX intelligent question answering application |
   |cite knowledge |Add **Knowledge Base**, select the bank knowledge base created in the previous step. |
   |Vector search weight |Adjust the proportion of keyword matching and semantic understanding: the lower the value, the more attention is paid to accurate word hits, and the higher the value, the more attention is paid to the overall semantic relevance.<br><br>Example value: 0.5 |
   |Mixed similarity threshold |Lower bound of relevance score for synthetic semantic matching and keyword matching. It will only be recalled if the mixed similarity of the candidate documents exceeds this threshold. The higher the value, the more accurate the recall result but the smaller the quantity; the lower the value, the wider the recall range but may introduce noise.<br><br>Example value: 0.2 |
   |sorting strategy |* Semantic model ranking: Use a dedicated semantic ranking model to re\-rank initial shardings by relevance. Fast and cost\-effective, it is suitable for most scenarios.<br><br>* Large model sorting: Call the large language model to evaluate the matching degree of sharding to the problem one by one, and the sorting quality is higher, but the speed is slightly slower. It is suitable for scenarios where there are high requirements for answer quality.<br><br><br>Example Value: Semantic Model Sorting |
   |Number of shardings |The number of candidate shardings retrieved and returned from the knowledge base. The higher the value, the wider the coverage of the recall, but it will increase the processing time. This value should be ≥ the number of selected shardings.<br><br>Example value: 30 |
   |Sort score threshold |When the threshold is set, only recall shardings with a score ≥ the threshold are retained, and results below the threshold are directly filtered and do not participate in the final display. The higher the threshold, the more accurate the results, but the number of recalls may decrease; the lower the threshold, the richer the results, but the less relevant content may be mixed in.<br><br>Example value: 0.5 |
   |recall segment count |After reordering, the final number of shardings displayed and fed to the large model in the search list. The higher the value, the more reference information the model can obtain, but it may introduce noise.<br><br>Example value: 5 |
   |enable intelligent search |After opening, the system will rewrite the recalled keywords semantically through the large model to improve the retrieval effect. In the returned results, the first item is the summary summary generated by the large model based on the recalled content, and the rest are the relevant document segments that were matched. Attention: When this function is enabled, the search time will increase.<br><br>Example Value: On |

4. On the right side of the application layout page, enter keywords to debug the application, accept the application effect, and readjust the parameter configuration based on the effect.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b7fdf3adf424874adca13235f0bd3aa~tplv-goo7wpa0wc-image.image)

5. When all configurations are complete, click Publish in the upper right corner of the page.

# Step 3: Apply for an API for the application

1. Select **Search Applications** in the left navigation bar of the Enterprise Knowledge Engine.

2. In the Search Apps list, find the search app you created in the previous step and click **Apply for API Token**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a6a6ebfbb294d5398045eca07a2ea1a~tplv-goo7wpa0wc-image.image)

3. Go to the **app management** page of the **open API** and click **New app** on the right side of the page.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6c1999722efd46bd994013dd06196904~tplv-goo7wpa0wc-image.image)

4. On the **New App** page, complete the following configuration and click **Save**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a1b6fe5537bc4091b6397bf6d6615191~tplv-goo7wpa0wc-image.image)

   Parameter description:

   * App name: Custom name, such as `call retrieval app`.

   * APIs available to the app: Select **Enterprise Knowledge Engine** \> **Call Retrieval App.**

   * Access to Authorizable Items: Select the specified item.

   * Associated User: Select the currently logged in user.

5. In the app management list, view the created apps and copy the **app token**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9b9750d0f4de4a0887dca4d53c36757b~tplv-goo7wpa0wc-image.image)

# Step 4: Access the search application through the API

In the left navigation bar of the Enterprise Knowledge Engine console, enter the **open API** \> **open capability** page, refer to the OpenAPI **access process** and **retrieval application call** API provided by the platform, and connect the retrieval application to your business system. See the API documentation description [Retrieval Application Call](https://docs.byteplus.com/docs/dataagent/retrieval-application-call).

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a049f0eba48342bda7d016f281c4d298~tplv-goo7wpa0wc-image.image)

Taking a third\-party platform (such as Mail carrier) as an example, calling a **search application calling** an API to get a search result is shown in the figure below.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f37cd0d9d0b4484cbbc64095e1f40dcf~tplv-goo7wpa0wc-image.image)
