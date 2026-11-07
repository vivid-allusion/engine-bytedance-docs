---
title: "Build an RAG system with Milvus for VectorDB and open-source dify"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Build_an_RAG_system_with_Milvus_for_VectorDB_and_open-source_dify"
---

This topic describes how to build RAG systems using Milvus for VectorDB and open\-source Dify.

<span id="t58unLDV"></span>
## Introduction to RAG principle

RAG (Retrieval\-Augmented Generation) is a large model application pattern that combines retrieval and generation. The principles are as follows: After a user request, the system first retrieves relevant knowledge fragments through the vector database, then passes these retrieval results as context to the large language model, helping the model generate more accurate, controllable, and business\-aligned answers. This approach alleviates the knowledge limitations of the model itself and avoids hallucinations caused by relying solely on parameter memory, thus improving result reliability and explainability.

<span id="x0YcF8j2"></span>
## Introduction to the open\-source Dify principles

Dify is an open\-source platform for developing large language model (LLM) applications. It integrates Backend as Service and LLMOps concepts, enabling developers to quickly build production\-grade generative AI applications. It also allows non\-technical users to participate in defining AI applications and managing data operations. Dify includes the key technology stack needed to build LLM applications, supporting hundreds of models, an intuitive prompt orchestration interface, a high\-quality RAG engine, a robust agent framework, and flexible workflows. It also offers an easy\-to\-use interface and API, allowing developers to focus on innovation and business needs.

<span id="eq4VaSCw"></span>
## Prerequisites


* An instance is created and is in the **Running** state. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance).

* An API Key for the embedding model is created in the [Volcano Ark Console](https://console.byteplus.com/ark/).

* An online inference endpoint is created in the [Volcano Ark console](https://console.byteplus.com/ark/), with a chat model (e.g., DeepSeek\-V3.1) and an embedding model (e.g., Doubao\-embedding) added.

* Git, Docker, and Docker\-Compose are installed. For more information, see [1.5 Getting Started - Installing Git](https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git), [Install Docker Engine](https://docs.docker.com/engine/install/), and [Overview of installing Docker Compose](https://docs.docker.com/compose/install/).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To access a Milvus instance using an IPv6 address, Docker\-Compose must support IPv6.   </div>
   

<span id="BZQkSK33"></span>
## Procedure

<span id="BZQkSK33"></span>
### Configure Docker (optional)

The default network mode for Docker is IPv4. To access a Milvus instance using an IPv6 address, go to the Docker settings page, select **Resources \> Network**, and set the Default networking mode to **Dual IPv4/IPv6**.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_82f4d6c9af989e1ed762b683f9c8c022.png) </span>

<span id="vogS9jkj"></span>
### Clone Dify

Use Git commands to clone the open\-source Dify project locally.

```Bash
# Clone code
git clone https://github.com/langgenius/dify.git
cd dify
```


<span id="1g671QeU"></span>
### Configure the `.env` file

```Bash
# Switch to the docker subdirectory in the root directory
cd docker
cp .env.example .env

# Edit the .env file, change the vector database to Milvus, and configure the parameters required for Milvus
VECTOR_STORE=milvus
MILVUS_URI="http://milvus-{Milvus 实例 ID}.milvus.ivolces.com:19530" 
MILVUS_USER="readwrite_user"
MILVUS_PASSWORD="readwrite@SINF"
```


The following content in the `.env` file needs to be modified.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b1f32910b7110d2994183eeb74f0f974.png) </span>

<span id="fGCq5WYq"></span>
### Configure access point rate limiting


1. Enter the [Volcano Ark Console](https://console.byteplus.com/ark/).

   2. Select **Model Inference** \> **Online Inference** from the left navigation bar.

   3. On the **User\-defined Inference Access Point** tab, click the target inference access point.

   4. On the **Overview** tab, in the **Basic information** area, click the edit icon next to **Access Point Rate Limiting**.

   5. In the rate limiting dialog, configure **RPM** (Requests Per Minute) and **TPM** (Tokens Per Minute) as needed.</a\>

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Description   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">It is recommended to set <strong>TPM</strong> above 10,000; otherwise, errors may occur later.   </div>
   

<span id="kpsdddT9"></span>
### Start and log on to Dify


1. Run the following command to start Dify.

   ```Bash
   # Start service
   docker compose up -d
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The initial startup of Dify takes about ten minutes.   </div>
   

2. Open the browser and go to [http://localhost/install](http://localhost/install) to access the Dify registration page.

3. Enter your email, user name, and password, then click **Settings**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c4eedc2e6fc6143fb0018bc300355298.png) </span>

4. On the log in page, enter the email and password set in the previous step, then click **Log on**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4858f81807c180313c06027e320e6c30.png) </span>


<span id="5P44VYk4"></span>
### Configure model


1. Click the user avatar in the top right corner, then select **Settings**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_85aadc751985f50453ed010e82b88090.png) </span>

2. In the left navigation bar, select **Model supplier**. Under the **Install model supplier** region, locate Volcengine and click **Install**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3496e759f17028da5e743e2b95312486.png) </span>

3. In the pop\-up dialog, click **Install**. After the plugin finishes, click **Close**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_aef7ec35307a6d9c8797e5b2502d1c75.png) </span>

4. In the **Pending configuration** area, find the **Volcengine** card, then click **Add model**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b3bf0e4718c00fc7259667458bb69517.png) </span>

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Repeat steps 4 to 5 to add the chat model and the embedding model one by one.   </div>
   

5. In the **Add Volcengine** window, configure the following parameters and then click**Save**.

   
   <Tabs>
   <Tab zoneid="XiHF3Bfv5l" title="Add chat model">
   <TabTitle>Add chat model</TabTitle>
   
   
   |Parameter |Description |
   |---|---|
   |Model type |Select **LLM**. |
   |Model name |Enter the model name. |
   |Authentication method |Select **API Key**. |
   |API Key |Enter your API Key. |
   |VolcEngine region |Keep default value. |
   |API Endpoint Host |Keep the default value. |
   |Endpoint ID |Enter the ID of the Online inference endpoint you created. |
   |Base model |Enter the chat model added to the online inference endpoint you created, for example, DeepSeek\-V3.1. |
   
   
   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ffbc0936cabc4d8be1a7d5c7e7c28720.png) </span>
   
   
   </Tab>
   <Tab zoneid="cXnuw9S17S" title="Add embedding model">
   <TabTitle>Add embedding model</TabTitle>
   
   
   |Parameter |Description |
   |---|---|
   |Model type |Select **Text Embedding**. |
   |Model name |Enter the model name. |
   |Authentication method |Select **API Key**. |
   |API Key |Enter your API Key. |
   |VolcEngine region |Keep the default value. |
   |API Endpoint Host |Keep the default value. |
   |Endpoint ID |Enter the ID of the online inference endpoint you created. |
   |Base model |Enter the embedding model added to the online inference endpoint you created, for example, Doubao\-embedding. |
   
   
   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3e10dc6ccaa0b67005cb9d9ebda6f4b6.png) </span>
   
   
   </Tab>
   </Tabs>
   

6. In the **Model list** area, click **System model configuration**. Under **System inference model**, select the added chat model. Under **Embedding model**, choose the added embedding model, then click**Save**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_544c625ab7630153a146ddabd0b6a303.png) </span>


<span id="Vxa9WGNX"></span>
### Create a knowledge base


1. In Dify's top navigation bar, select **Knowledge base**, then click **Create knowledge base**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_980ccc5fe30064b7247754f22653b4dd.png) </span>

2. In the **Select data source** step, under **Select data source**, choose **Import existing text**. Under **Upload text file**, click **Select file** to choose a local knowledge base file or drag the file into the upload area, then click **Next**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7a95a9c6be8deffe78c6d28fdd3c1888.png) </span>

3. In the **Text segmentation and cleaning** step, keep all parameters at their default values, then click **Save and process**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9c4ab30fc0922e9f02838e08c508e64b.png) </span>

4. In the **Process and complete** step, wait for the document embedding to finish, then click **go to document**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8f8846bbcb5d8bb948c0b907c1abcb0f.png) </span>

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_22b666e4218dbe7aae751d847f8171e9.png) </span>


<span id="AFz7nb6R"></span>
### Confirm the document has been written

Call the API to confirm the document has been written to the Milvus for VectorDB vector database. For detailed operations, refer to [List Collections](https://milvus.io/api-reference/restful/v2.5.x/v2/Collection%20(v2)/List.md).


* Get database name

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_de9aa740986f0cf137d7c1d851cf1563.png) </span>

* Get collection name

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dddcbb4679f41a802ffa58afa3110452.png) </span>

* Get the number of documents in the collection

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_352f53d0aed2cc6c6c7f7e46e74730d9.png) </span>


<span id="u5uQqNhB"></span>
### Create application


1. In the Dify top navigation bar, select **Studio**, then click **Create from application template** on the **Create application** card.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_83471568e1f4fda2c347d25c846fd871.png) </span>

2. In the left navigation bar, select **Knowledge Retrieval**, then click **Use this template** on the **Knowledge base + chatbot** card.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fda99e3c65fd92efed315ad7e354163d.png) </span>

3. In the popup dialog, configure the following parameters, then click **Create**.

   
   |Parameter |Description |
   |---|---|
   |Application Name & Icon |* Enter the application name.<br><br>* Click the example icon, then select an emoji or upload an icon locally. |
   |Description |Enter the application description. |
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1b81517faff9e7e69ec1c577cecb3bad.png) </span>

4. On the application configuration page, ignore the popup, click **Knowledge retrieval node**, then click the  **+**  icon after **Knowledge base**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_036dc3e01aa55bc344c3e0887624257e.png) </span>

5. In the popup dialog, select the added knowledge base, then click **Add**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_92012ed9b20656e5bdceebe67f662618.png) </span>

6. Configure the **knowledge retrieval**, **LLM**, **Parameter extractor**, and **Direct reply** nodes in sequence.

   1. Click the **LLM** node, then configure the following parameters.

      
      |Parameter |Description |
      |---|---|
      |Model |Select the chat model to add. |
      |Context |Select `{x} result`. |
      |SYSTEM |Copy the sample prompt in [Appendix](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Build_an_RAG_system_with_Milvus_for_VectorDB_and_open-source_dify?lang=zh#xgnxeeFf) and paste it into the text box, then replace `{{ placeholder }}` with `/`, and then select **Context**. |
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_94bf3185f03aee9bf191416bd7f7dfbf.png) </span>

   2. Right\-click the **Parameter extractor**, then select **Delete**.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_17b348b45074c4cc7d57bddd7c74e4bf.png) </span>

   3. Drag the  **+**  icon on the right side of the **LLM** node to the right to connect it to the **Direct reply** node.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9beb313eed59955823333991ee4e3f99.png) </span>

   4. Click the **Direct reply** node, clear the content in the **Reply** text box, enter `/`, then select `{x}text`.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d8c054ffd0dcb882225503cd0039055c.png) </span>

7. Click **Preview** in the upper right corner of the page, enter a question in the text box, then click the send button. The system will respond based on the knowledge base content.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b590b5f31498461c5fc2252d89763ffd.png) </span>

8. After confirming the application runs as expected, click **Publish** in the upper right corner of the page, then click **Publish update**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e5a09b615bc64d5357de64ebd43d5416.png) </span>

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ca62fd06b69f5b0cb0a2d2b3ba4ff3f3.png) </span>


<span id="xgnxeeFf"></span>
### Appendix

Prompt

```Plain Text
Act as a Milvus expert, relying exclusively on content from `Milvus_Knowledge` (never using pre-existing internal knowledge) to answer user questions.

# Milvus_Knowledge
{{ placeholder }}

# Additional Details
- All answers must be directly derived from explicit information in `Milvus_Knowledge`.  
- Avoid assumptions, inferences, or details not explicitly stated in `Milvus_Knowledge`.  

# Steps
1. **Understand User Query**: Identify the specific Milvus-related question (e.g., index creation, cluster management, performance tuning).  
2. **Extract from Milvus_Knowledge**: Scan `Milvus_Knowledge` to locate details (e.g., parameters, workflows, definitions) that directly address the user’s query.  
3. **Validate Relevance**: Ensure extracted information is explicitly tied to the user’s question; discard unrelated or tangential content.  
4. **Formulate Response**: Combine the validated information into a clear, concise answer that directly answers the user’s query.  

# Output Format
A structured response prioritizing numbered lists (e.g., "1. ...", "2. ...") to clearly address the user’s question. Each list item should:

Directly relate to the user’s query.
Include specific details from the Milvus_Knowledge (e.g., parameter names like "nlist", values like "1024-16384", or step names like "segment merging").
Use natural language without markdown formatting.

Responses may span 1-3 concise paragraphs if needed, but list formatting is preferred to highlight key points extracted from the Milvus_Knowledge.
 

# Examples
**User Query**: "How to configure IVF_FLAT index in Milvus 2.3?"
**Milvus_Knowledge** (placeholder):  
"Milvus 2.3 IVF_FLAT configuration: (1) Set 'metric_type' to 'L2' or 'IP' based on similarity needs. (2) 'nlist' parameter controls the number of clusters (recommended range: 1024-16384). (3) Use 'index_file_size' to define segment size (default: 1024MB)." 

**Answer**:  
"To configure IVF_FLAT in Milvus 2.3: (1) Set metric_type to 'L2' (Euclidean distance) or 'IP' (inner product) depending on your similarity calculation needs. (2) Adjust nlist to control the number of clusters, with a recommended range of 1024-16384. (3) Use index_file_size to define segment size, which defaults to 1024MB. These settings are specific to Milvus 2.3 IVF_FLAT index configuration."

# Notes
- If `Milvus_Knowledge` contains no relevant details, respond with: "No applicable Milvus information found in milvus knowledge to answer your query."  
- Prioritize precision: Include exact parameter names (e.g., `auto_index`) and constraints (e.g., "not compatible with HNSW") from `Milvus_Knowledge`.  
- Do not include hypothetical scenarios or general advice not explicitly stated in `Milvus_Knowledge`.
```


&nbsp;

&nbsp;
