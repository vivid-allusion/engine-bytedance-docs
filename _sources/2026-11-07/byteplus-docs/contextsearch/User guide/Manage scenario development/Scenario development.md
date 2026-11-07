---
title: "Scenario development"
product: "ContextSearch"
product_code: "contextsearch"
source: "https://docs.byteplus.com/en/docs/contextsearch/Scenario_development"
---

After creating a scenario, you need to develop it before starting and using it. This topic describes how to develop a scenario.

<span id="h805KalJ"></span>
## Precautions

This topic only covers scenario development for knowledge base, picture search, and video search scenarios. For scenario development of Personalization search, Agentic Search, and Multimodal search, see [Personalization search](https://docs.byteplus.com/en/docs/contextsearch/Personalization_Search), [Agentic Search](https://docs.byteplus.com/en/docs/contextsearch/Agentic_Search), and [Multimodal search](https://docs.byteplus.com/en/docs/contextsearch/Multimodal_search).

<span id="3WrttiLf"></span>
## Procedure


1. Log on to the [ContextSearch console](https://console.byteplus.com/context-search).

2. In the top navigation bar, select the target project and region.

3. In the left navigation bar, select **My Scenario**, then click the target scenario.

4. On the scenario configuration page, perform the following configurations.


<span id="hCrASqcK"></span>
### Basic configuration


1. On the scenario details page, click **Configure** to configure storage and embedding.

2. In the **Basic configuration** panel, configure the following parameters, then click **OK**.

   
   |Parameter |Description |
   |---|---|
   |Storage location |Select the instance type for running the scene. Currently supports specifying database instances. |
   |Database type |Select the database type for the scenario. Currently supported are **Cloud Search**, **Milvus**, and **TOS Vectors**. |
   |Affiliated project |Project to which the scene belongs. Configuration cannot be switched during basic setup. To switch, close the dialog and modify it from the top navigation bar. |
   |Instance name/ID |Select the target OpenSearch instance from the dropdown list. Supports fuzzy search based on keywords in the instance name. If a new OpenSearch instance is needed, see [Create an instance](https://docs.byteplus.com/en/docs/cloudsearch/creating-an-instance-2).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only OpenSearch 2.9.0 or later instances support ContextSearch.</div><br> |
   |User name |Enter the username of the instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is visible only when the database type is <strong>Cloud Search</strong> or <strong>Milvus</strong>.</div><br> |
   |Password |Enter the instance password.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is visible only when the database type is <strong>Cloud Search</strong> or <strong>Milvus</strong>.</div><br> |
   |Vector bucket |Select the vector bucket to use from the dropdown list. <br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is visible only when the database type is <strong>TOS Vectors</strong>.</div><br> |
   |Select model/inference service |Select models associated with the created inference service. If a new inference service is needed, see [Create a custom inference service](https://docs.byteplus.com/en/docs/contextsearch/Create_a_custom_inference_service). |
   |API Key |Select the API Key to call the model. If you need a new API Key, see [Create an API Key](https://docs.byteplus.com/en/docs/contextsearch/Create_an_API_Key). |
   |Field configuration |After configuring fields, you can perform data structuring and search filtering on uploaded retrieval files. |
   


<span id="kOdSBbIs"></span>
### Reranking


<Tabs>
<Tab zoneid="yFay3sQSj4" title="Knowledge base scenario">
<TabTitle>Knowledge base scenario</TabTitle>

Input the recall results from the knowledge retrieval stage into the reranking model for semantic\-level reranking and output the top N documents with the highest scores.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Reranking is enabled by default and supports custom configuration. If reranking is not required, turn off this feature.</div>



|**Parameter** |**Description** |
|---|---|
|Select model/inference service |Select models associated with the created inference service. If a new inference service is needed, see [Create a custom inference service](https://docs.byteplus.com/en/docs/contextsearch/Create_a_custom_inference_service). |
|API Key |Select the API Key to call the model. If you need a new API Key, see [Create an API Key](https://docs.byteplus.com/en/docs/contextsearch/Create_an_API_Key). |



</Tab>
<Tab zoneid="bWHzl4oFfd" title="Image search scenario">
<TabTitle>Image search scenario</TabTitle>

Input the recall results of pictures into the reranking model for semantic\-level reranking, outputting the Top N pictures with the highest scores.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Reranking is enabled by default and supports custom configuration. If reranking is not required, turn off this feature.</div>



|**Parameter** |**Description** |
|---|---|
|Select model/inference service |Select models associated with the created inference service. If a new inference service is needed, see [Create a custom inference service](https://docs.byteplus.com/en/docs/contextsearch/Create_a_custom_inference_service). |
|API Key |Select the API Key to call the model. If you need a new API Key, see [Create an API Key](https://docs.byteplus.com/en/docs/contextsearch/Create_an_API_Key). |



</Tab>
<Tab zoneid="kzHakrRG6s" title="Video search scenario">
<TabTitle>Video search scenario</TabTitle>

This configuration item is not involved.


</Tab>
</Tabs>


<span id="ERVLivJO"></span>
### Knowledge Q&A


<Tabs>
<Tab zoneid="zpqx3JNCHE" title="Knowledge base scenario">
<TabTitle>Knowledge base scenario</TabTitle>


|**Parameter** |**Description** |
|---|---|
|Retrieval strategy |Select the retrieval strategy for the knowledge base.<br><br><br>* Fast: completes retrieval faster, suitable for lightweight tasks focused on efficiency.<br><br>* Standard: Balances speed and quality for most everyday needs.<br><br>* Deep: Provides more comprehensive and detailed deep reasoning, a high\-precision mode designed for demanding scenarios. |
|Back quantity |Set the number of documents returned by the search. |



</Tab>
<Tab zoneid="wpZCBZdntZ" title="Image search scenario">
<TabTitle>Image search scenario</TabTitle>


|**Parameter** |**Description** |
|---|---|
|Back quantity |Set the number of pictures returned by the retrieval. |



</Tab>
<Tab zoneid="QhtqmbmzvE" title="Video search scenario">
<TabTitle>Video search scenario</TabTitle>


|**Parameter** |**Description** |
|---|---|
|Back quantity |Set the number of videos returned in the search results. |



</Tab>
</Tabs>


<span id="78BmujEO"></span>
### Add a retrieval files

The scenario initializes automatically after configuration is complete. After initialization, you can add retrieval files.


<Tabs>
<Tab zoneid="zNY3qd7W90" title="Knowledge base scenario">
<TabTitle>Knowledge base scenario</TabTitle>

1. Click **Add** in the **Search file** area.

2. In the **Add file** panel, configure the following parameters, then click **OK**.

   
   |Parameter |Description |
   |---|---|
   |Upload/select file |Select **TOS** or **Local documentation**. When **Local documentation** is selected, click the upload area to select files or drag files to the upload area. |
   | Select bucket |Select the bucket containing the files to add. If there are no available buckets, create one. For more information, see [Creating buckets](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket). |
   |Target folder |Select the folder containing the files to add. |
   |Structured fields |Enter the name and value of the field. click **add field** to add a new structured field. |
   |Import configuration |Select whether to turn on the OCR model for imported files. When turned on, the model recognizes and extracts text from pictures or scanned documents to improve search results. Sub\-parameters:<br><br><br>* Model/inference service: select a model associated with the created inference service. If a new inference service is needed, see [Create a custom inference service](https://docs.byteplus.com/en/docs/contextsearch/Create_a_custom_inference_service).<br><br>* API Key: select the API Key used to call the model. If you need a new API Key, see [Create an API Key](https://docs.byteplus.com/en/docs/contextsearch/Create_an_API_Key). |
   


</Tab>
<Tab zoneid="HdYGgGKYHr" title="Image search scenario">
<TabTitle>Image search scenario</TabTitle>

1. Click **Add** in the **Search file** area.

2. In the **Add file** panel, configure the following parameters, then click **OK**.

   
   |Parameter |Description |
   |---|---|
   |Upload/select file |Select **TOS** or **Local documentation**. When selecting **Local documentation**, click the upload area and select files to upload, or drag files to the upload area. |
   | Select bucket |Select the bucket containing the files to add. If there are no available buckets, create one. For more information, see [Creating buckets](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket). |
   |Target folder |Select the folder containing the files to add. |
   |Structured fields |Enter the name and value of the field. click **add field** to add a new structured field. |
   |Import configuration |Select whether to turn on the picture understanding model for imported pictures. When enabled, the model automatically generates descriptive text for added pictures, enhancing search results. Sub\-parameters:<br><br><br>* Model/inference service: select a model associated with the created inference service. If a new inference service is needed, see [Create a custom inference service](https://docs.byteplus.com/en/docs/contextsearch/Create_a_custom_inference_service).<br><br>* API Key: select the API Key used to call the model. If you need a new API Key, see [Create an API Key](https://docs.byteplus.com/en/docs/contextsearch/Create_an_API_Key).<br><br>* Prompt: Add prompts to the model based on requirements. Example: Describe the content of the picture. |
   


</Tab>
<Tab zoneid="FpQ5rmHPqS" title="Video search scenario">
<TabTitle>Video search scenario</TabTitle>

1. Click **Add** in the **Search file** area****.

2. Configure the following parameters in the **Add file** panel, then click **OK**.

   
   |Parameter |Description |
   |---|---|
   |Upload/select file |Select **TOS** or **Local documentation**. When selecting **Local documentation**, click the upload area and select files to upload, or drag files to the upload area. |
   | Select bucket |Select the bucket containing the files to add. If there are no available buckets, create one. For more information, see [Creating buckets](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket). |
   |Target folder |Select the folder containing the file to add. |
   |Import configuration |Select whether to turn on the speech recognition service model/inference service and video understanding model for imported videos. After turning it on, the model will automatically convert speech from audio to text and perform semantic analysis on video content to enhance search results. Sub\-parameters:<br><br><br>* Model/inference service: select a model associated with the created inference service. If a new inference service is needed, see [Create a custom inference service](https://docs.byteplus.com/en/docs/contextsearch/Create_a_custom_inference_service).<br><br>* API Key: select the API Key used to call the model. If you need a new API Key, see [Create an API Key](https://docs.byteplus.com/en/docs/contextsearch/Create_an_API_Key).<br><br>* Prompt: add prompts to the model based on requirements. Example: summarize video content. |
   |Maximum slice length |Specify the maximum allowed duration for each video segment during processing. Videos exceeding this length will be automatically split into multiple segments for processing. Valid values are as follows:<br><br><br>* 15 seconds<br><br>* 30 seconds<br><br>* 60 seconds<br><br>* Custom |
   


</Tab>
</Tabs>


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">After adding retrieval files, click <strong>View Slices</strong> to see details of the file slices.</div>


<span id="hWTcBMa8"></span>
### Debug preview

After completing the scenario development configuration, enter your questions or requests in the **Debug preview** area to test.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Knowledge base scenarios support displaying referenced document information in output results.</div>


<span id="r5WHKQXe"></span>
## View logs

You can click **Logs** on the scene development page to view the logs of the scene. Logs can be filtered by time range, log level, file, and keyword.

<span id="L7OnAPJU"></span>
## View configuration information

You can click **Configuration** on the scene development page to view the scene’s **Basic information**, **Release resources**, **Storage location**, **Embedding**, and **Access information**.


|**Category** |**Details** |
|---|---|
|Basic information |Includes the scene's name, description, and creation time. |
|Publish resource |Includes the status, resource type, specification, and number of nodes of the scenario. You can click **Stop**, **Restart**, or **Modification** to perform the corresponding actions. |
|Storage location |Includes services related to the scenario and the instance name/ID. |
|Embedding |Includes the embedding model used in the scenario and the associated inference service. |
|Access information |Includes virtual private cloud, availability zone, subnet, private network access status, public network access status, private network access address, and public access address of the scenario. After turning on private network access or public network access, you can view the corresponding access address. |


<span id="h0obf9JM"></span>
## View call examples

You can click **API example** on the scene development page to see call examples for the scene, available in cURL or Python format.

<span id="hbb6726d"></span>
## View monitoring

You can click **Monitor** on the scene development page to view the scene’s monitoring information. Monitoring indicators include **QPS**, **TPS**, **average response time** and **request success rate**. Filtering monitoring information by time range is supported.

<span id="hbb6726d"></span>
## Publish scene

After debugging the scene, you can publish it online.


1. On the scene development page, click **Release**.

2. In the **Release** dialog, configure the following parameters, then click **OK**.

   
   |Parameter |Description |
   |---|---|
   |Version number |Set the version for the release scenario. The version number rules are as follows:<br><br><br>* The version number cannot exceed 255 characters.<br><br>* It can only contain English letters, numbers, and periods (.).<br><br>* It cannot contain consecutive periods (.). |
   |Description |Optional. Set the description for the publishing scenario, supporting up to 50 characters. |
   |Specification |Select the resource specification from the dropdown list. |
   |Number of nodes |Set the number of nodes. The number of nodes can be set from 2 to 512. |
   


<span id="oEO3NrVP"></span>
## Version management

Each publish generates a new version. You can click **Version management** to view published versions and delete unwanted versions as needed.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The version in use cannot be deleted.</div>


* <div data-tips="true" data-tips-type="warning">Deleting a version is irreversible; proceed with caution.</div>
