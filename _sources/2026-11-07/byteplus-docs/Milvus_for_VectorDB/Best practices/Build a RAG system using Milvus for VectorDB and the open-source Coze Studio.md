---
title: "Build a RAG system using Milvus for VectorDB and the open-source Coze Studio"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Build_a_RAG_system_using_Milvus_for_VectorDB_and_the_open-source_Coze_Studio"
---

This topic describes how to build a RAG system using Milvus for VectorDB and the open\-source Coze Studio.

<span id="PJtGn16y"></span>
## RAG principles

RAG (Retrieval\-Augmented Generation) is a large model application that combines retrieval with generation. The principles are as follows: After the user submits a request, the system first retrieves relevant knowledge fragments through the vector database, then passes these results as context to the large language model to help it generate more accurate, controllable, and business\-aligned responses. This approach alleviates the model’s inherent knowledge limitations and avoids hallucinations caused by over\-reliance on parameter memory, improving the reliability and interpretability of the results.

<span id="p8BJwMiH"></span>
## Introduction to the open\-source Coze Studio platform

[Coze Studio](https://github.com/coze-dev/coze-studio/) is ByteDance’s next\-generation AI large model intelligent agent development platform. It integrates rich features such as plugins, workflows, and cards to help you quickly and easily build personalized or commercially valuable intelligent agents.

<span id="DIinq2ZP"></span>
## Prerequisites


* An instance is created and is in the **Running** state. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance).

* An API Key for the embedding model has been created in the [Volcano Ark console](https://console.byteplus.com/ark/).

* An online inference endpoint has been created in the [Volcano Ark console](https://console.byteplus.com/ark/), with a chat model (such as Doubao\-Seed\-1.6) and an embedding model (such as Doubao\-embedding) added.

* Git, Docker, and Docker\-Compose are installed. For more information, see [1.5 Getting Started - Install Git](https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git), [Install Docker Engine](https://docs.docker.com/engine/install/), and [Overview of installing Docker Compose](https://docs.docker.com/compose/install/).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To access a Milvus instance using an IPv6 address, Docker\-Compose must support IPv6.   </div>
   

<span id="UAJhV4Iz"></span>
## Procedure

<span id="Bng7uE0T"></span>
### Configure Docker (optional)

The default network mode for Docker is IPv4. To access a Milvus instance using an IPv6 address, go to Docker settings, select **Resources \> Network**, and set the Default networking mode to **Dual IPv4/IPv6**.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_82f4d6c9af989e1ed762b683f9c8c022.png) </span>

<span id="kShPrOU6"></span>
### Configure Coze Studio


1. Clone the open\-source Coze Studio project to your local machine using Git commands.

   ```Bash
   # Clone code
   git clone https://github.com/coze-dev/coze-studio.git
   ```
   

2. Configure the model.

   1. Copy the doubao\-seed\-1.6 model template files from the template directory and paste them into the configuration file directory.

      ```Bash
      cd coze-studio
      # Copy model configuration template
      cp backend/conf/model/template/model_template_ark_doubao-seed-1.6.yaml backend/conf/model/ark_doubao-seed-1.6.yaml
      ```
      

   2. In the configuration file directory, modify the template files.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The configuration may change; for details, refer to the description in the <a href="https://github.com/coze-dev/coze-studio/blob/main/README.zh_CN.md#%E5%BC%80%E5%8F%91%E6%8C%87%E5%8D%97">Coze Studio Development Guide</a>.      </div>
      

      1. Enter directory `backend/conf/model`. Open the copied file `ark_doubao-seed-1.6.yaml`.

      2. Set the following fields and save the file.

         
         |Fields |Description |
         |---|---|
         |id |Model ID in Coze Studio, defined by the developer. It must be a non\-zero integer and globally unique. Default value can be used. Agents or workflows call the model based on the model ID.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Do not modify the model ID for models already online, as this may cause model call failures.</div><br> |
         |name |The model name displayed on the Agent configuration page. Default value can be used. |
         |base_url |Set to `https://ark.cn-beijing.volces.com/api/v3/`. |
         |meta.conn_config.api_key |API Key for the model service, which in this example is the Volcengine Ark API Key. |
         |meta.conn_config.model |The Model name of the model service, which in this example is the Model ID or Endpoint ID of Volcano Ark. |
         


<span id="hMFVJMkv"></span>
### Configure the `.env` file

```Bash
Switch to the docker subdirectory under the root directory
cd docker
cp .env.example .env

Edit the following fields in the .env file
# Settings for Embedding
export ARK_EMBEDDING_BASE_URL="https://ark.cn-beijing.volces.com/api/v3/"
export ARK_EMBEDDING_MODEL="***"
export ARK_EMBEDDING_API_KEY="***" Embedding model ID and API key
export ARK_EMBEDDING_DIMS="2048"  See the Ark model details page for the specific vector dimension returned by the model

Settings to replace Milvus instance, username, and password in VectorStore
export MILVUS_ADDR="http://milvus-{Milvus 实例 ID}.milvus.ivolces.com:19530"  Internal public test cluster export MILVUS_USER="readwrite_user" export MILVUS_PASSWORD="readwrite@SINF"
export MILVUS_USER="Milvus 用户名"
export MILVUS_PASSWORD="Milvus 用户密码"
```


The changes for the `.env` file are as follows.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4987d7e498859048d8c007d6bb02635b.png) </span>

<span id="jCZcYYf7"></span>
### Configure access point rate limiting


1. Go to the [Volcano Ark Console](https://console.byteplus.com/ark/).

   2. Select **Model Inference** \> **Online Inference** in the left navigation bar.

   3. On the **User\-defined Inference Access Point** tab, click the target inference access point.

   4. On the **Overview** tab in the **Basic information** area, click the edit icon to the right of **Access Point Rate Limiting**.

   5. In the rate limiting dialog, configure **RPM** (Requests Per Minute) and **TPM** (Tokens Per Minute) as needed.

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Description   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">It is recommended to set <strong>TPM</strong> to above 10,000 to avoid possible errors later.   </div>
   

<span id="DSnAc0GP"></span>
### Configure and start Coze Studio


1. Edit the `docker-compose.yml` file and modify the following:

   * The image tag for coze\-server

   * IPv6 support (optional, enables access to IPv6 addresses)

      ```YAML
      services:
        # ....
        coze-server:
          # ....
          image: cozedev/coze-studio-server:0.3.11.nightly4  # Because the official image does not yet support Milvus authentication, the image tag needs to be modified.
      networks:
        coze-network:
          driver: bridge
          enable_ipv6: true  # Add IPv6 support
      ```
      

2. Run the following command to start Coze Studio.

      ```Bash
      # Start service
      docker compose up -d
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The Coze Studio startup process takes about ten minutes.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If an abnormality occurs during startup, check the logs in Docker by selecting <strong>Containers \> coze\-studio \> coze\-server \> Logs</strong>.      </div>
      

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="2"><img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_71e647d2dd9375267b4ed5970a2ac87e.png" width="667px" />   </div>
   


<span id="HEtnddX4"></span>
### Create knowledge base


1. Open [http://localhost:8888/](http://localhost:8888/) in the browser to access the Coze Studio login page.

2. Enter your email and password, then click **Log in**. If you don't have an account, click **Register**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_90339d6e187e06a02bf950d1822d6a53.png) </span>

3. In the left sidebar, select **Workspace \> Resource**.

4. On the **Resource** page, click the  **+ Resource** button in the top right corner, then choose **Knowledge Base**.<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_866abd4bc9f9fc56c9b11e3643448141.png) </span>

5. In the **Create knowledge base** dialog, select **Text format**, configure the following parameters, then click **Complete creation**.

   
   |Parameter |Description |
   |---|---|
   |Name |Enter the knowledge base name. Length must be between 1 and 100 characters. |
   |Description (optional) |Enter the description of the knowledge base. Length from 0 to 2000 characters. |
   |Import type |Select **Local document**. |
   |Icon |Click the icon to upload the knowledge base icon file from local. |
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_acc5bb7623919470bd7805b19b7f6841.png) </span>

6. On the created knowledge base page, click **Add content** in the top right corner, then select **Local document**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4051874004d71fc2386dd57b3ee4f200.png) </span>

7. Complete the following steps on the **Create Knowledge Base** page.

   1. Click the upload area to select documents or drag documents to the upload area, then click **Next**.<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_19ac647aec50f528896fdae582fd3716.png) </span>

   2. Configure the parameters in the **Create settings** step as needed, then click **Next**.

   3. At the **Segmentation preview** step, preview the segmentation effect, then click **Next**.

   4. At the **Data processing** step, wait for the data to be processed, then click **Confirm**.


<span id="CtXD0l3r"></span>
### Confirm the document has been written

Call the API to confirm the document has been written to Milvus for VectorDB. Refer to [List Collections](https://milvus.io/api-reference/restful/v2.5.x/v2/Collection%20(v2)/List.md) for detailed operations.


* Get database name

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_de9aa740986f0cf137d7c1d851cf1563.png) </span>

* Get collection name

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dddcbb4679f41a802ffa58afa3110452.png) </span>

* Get the number of documents in the collection

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_352f53d0aed2cc6c6c7f7e46e74730d9.png) </span>


<span id="KfPBB3nK"></span>
### Verify whether the vector retrieval was successful


1. In the left navigation bar, click the  **+**  button.

2. In the create dialog, click **Create agent**.

3. In the create agent dialog, configure the following parameters, then click **Confirm**.

   
   |Parameter |Description |
   |---|---|
   |Agent name |Enter the name of the agent. Length must be between 1 and 20 characters. |
   |Agent feature introduction (optional) |Enter the agent description. Length must be between 0 and 500 characters. |
   |Workspace |Select the workspace to which the agent belongs. Default is **Personal Space**. |
   |Icon |Click the icon to upload the agent's icon file from local. |
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5023b21db44da64980e17e4ee8d7e72a.png) </span>

4. Configure the agent on the orchestration page.

   1. In the **Persona and reply logic** textbox on the left, set the role and answer format as needed. Recommended prompts are provided at the bottom of the page; select the appropriate card to insert.

   2. The middle section is for model configuration. Click the **Text** then the  **+**  icon to add a knowledge base created in [Create Knowledge Base](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Build_a_RAG_system_using_Milvus_for_VectorDB_and_the_open-source_Coze_Studio#HEtnddX4).

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1c47e0ece766f863f9bb5c490dad690.png) </span>

   3. Ask the agent. Example:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_16839e88aedee2f7cc5bddd5cfa04fe5.png) </span>


&nbsp;

&nbsp;
