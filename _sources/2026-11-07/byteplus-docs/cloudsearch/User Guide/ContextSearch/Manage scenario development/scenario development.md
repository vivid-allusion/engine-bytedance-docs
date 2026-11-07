---
title: "scenario development"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Scenario_development"
---

After creating a scenario, you need to develop it before starting and using it. This article explains how to develop a scenario.

<span id="3WrttiLf"></span>
## Procedure


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. In the left navigation bar, select **ContextSearch \> My Scene**, then click the target scenario.

4. On the scenario configuration page, perform the following configurations.


<span id="hCrASqcK"></span>
### Storage and embedding configuration


1. On the scenario details page, click **Configure** to configure storage and embedding.

2. Configure the following parameters in the **Basic configuration** dialog, then click **OK**.

   
   |Parameter |Description |
   |---|---|
   |Storage location |Select the instance type for running the scene. Currently supports specifying database instances. |
   |Database type |Select the database type used in the scenario; currently supports Cloud Search service. |
   |Instance name/ID |Select the target OpenSearch instance from the dropdown list. Supports fuzzy search based on keywords in the instance name. If a new OpenSearch instance is needed, see [Create an instance](https://docs.byteplus.com/en/docs/cloudsearch/creating-an-instance-2).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only OpenSearch 2.9.0 or later instances support ContextSearch.</div><br> |
   |Authorize to use an instance |Display the instance authorization status. You can follow these steps to authorize full access for ContextSearch service to the OpenSearch instance.<br><br><br>1. Click **To authorize**.<br><br>2. In the **Instance authorization** dialog, enter the instance **username** and **password**, then click **OK**.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Without authorization, the scenario cannot use the OpenSearch instance resources.</div><br> |
   |Private network |To ensure smooth intranet access, it is recommended to select the VPC in the region where your existing cloud services are located. Subnets in different availability zones within the same VPC can communicate with each other. If you want to create a VPC, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC). |
   |Subnet |The system automatically filters available subnets based on the region, availability zone, and VPC that you select. If you want to create a new subnet, see [Creating a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet). |
   |Model source |Select **Default model** or **Ark model**. |
   |Model/inference service |Select models associated with the created inference service. |
   |API Key |Select the API Key used to call the model. If you need a new API Key, see [Create an API Key](https://docs.byteplus.com/docs/6465/1359479). |
   


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
|Model/inference service |Select models associated with the created inference service. |
|API Key |Select the API Key used to call the model. If you need a new API Key, see [Create an API Key](https://docs.byteplus.com/docs/6465/1359479). |



</Tab>
<Tab zoneid="bWHzl4oFfd" title="Image search scenario">
<TabTitle>Image search scenario</TabTitle>

This configuration item is not involved.


</Tab>
<Tab zoneid="kzHakrRG6s" title="Video search scenario">
<TabTitle>Video search scenario</TabTitle>

This configuration item is not involved.


</Tab>
</Tabs>


<span id="ERVLivJO"></span>
### Knowledge Q&A


<Tabs>
<Tab zoneid="TWRmPaKFk1" title="Knowledge base scenario">
<TabTitle>Knowledge base scenario</TabTitle>

In the Q&A session, documents related and filtered by the reordering module and user questions are input to the large language model. The large language model semantically analyzes the input, integrating the knowledge from retrieved documents with the user's questions to generate coherent text that provides high\-quality, targeted answers effectively responding to user inquiries.


|**Parameter** |**Description** |
|---|---|
|Model source |Select **Default model** or **Ark model**. |
|Model/inference service |Select models associated with the created inference service. |
|API Key |Select the API Key used to call the model. |
|Prompt |You can set appropriate prompts according to actual conversation needs to get more specific answers.<br><br>Example: You are a general knowledge base assistant; answer questions objectively. |



</Tab>
<Tab zoneid="npblKDDh7N" title="Image search scenario">
<TabTitle>Image search scenario</TabTitle>

This configuration item is not involved.


</Tab>
<Tab zoneid="brnYbt3I3D" title="Video search scenario">
<TabTitle>Video search scenario</TabTitle>

This configuration item is not involved.


</Tab>
</Tabs>


<span id="VRI3vuZi"></span>
### Retrieval parameters


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
### Add retrieval file

The scenario initializes automatically after configuration is complete. After initialization, retrieval files can be added.


1. Click **Add** in the **Retrieve file** area.

2. In the **Add file** dialog, choose **TOS** or **Local documentation**.

   * Object Storage: select the bucket and target folder for the files to add, then click **OK**. If there are no available buckets, first create a bucket. For detailed steps, see [Create bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).

   * Local documents: click the upload area and select files to upload, or drag files to the upload area. After uploading, click **OK**.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For knowledge base scenarios, after adding retrieval files, select <strong>...</strong> on the right side of the file <strong>View slices</strong> to see details of the file slices.</div>


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
   |version number |Set the version for the release scenario. The version number rules are as follows:<br><br><br>* The version number cannot exceed 255 characters.<br><br>* It can only contain English letters, numbers, and periods (.).<br><br>* It cannot contain consecutive periods (.). |
   |Description |Optional. Set the description for the publishing scenario, supporting up to 50 characters. |
   |Specification |Select the resource specification from the dropdown list. |
   |Number of nodes |Set the number of nodes. The number of nodes can be set from 2 to 512. |
   


<span id="oEO3NrVP"></span>
## Version management

Each publish generates a new version. You can click **Version management** to view published versions and delete unwanted versions as needed.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The version in use cannot be deleted.</div>


* <div data-tips="true" data-tips-type="warning">Deleting a version is irreversible; proceed with caution.</div>
