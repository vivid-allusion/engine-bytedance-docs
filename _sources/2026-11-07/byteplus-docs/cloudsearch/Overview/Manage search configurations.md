---
title: "Manage search configurations"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Manage_search_configurations"
---

The index search configuration defines search behavior and result presentation, such as tokenization rules, matching strategies, relevance calculation, and performance parameters, ensuring search results meet business needs while optimizing performance. This article explains how to manage search configurations in AI Search.

<span id="kX1RLQpg"></span>
## Prerequisites


* Created an OpenSearch 2.9.0 or later instance. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/cloudsearch/creating-instance).

* Created AI Search. For more information, see [Create AI search](https://docs.byteplus.com/en/docs/cloudsearch/Create_an_AI_search_service).

* Created an index. For more information, see [Create an index](https://docs.byteplus.com/en/docs/cloudsearch/Create_index).


<span id="8MqYiEeK"></span>
## Create a search configuration


1. Log on to the[Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. Select **AI search** in the left navigation bar, then find and click the target service name.

4. Select **Index management** in the left navigation bar, then click **Manage search configuration** in the **Operation** column of the target index

5. In the **Search configuration** tab, click **Create search configuration**

6. In the create search configuration dialog, set the following parameters, then click **OK** to enter the **CreateSearch template** page

   
   |Parameter |Description |
   |---|---|
   |Search configuration name |Set the search configuration name. Naming rules are as follows:<br><br><br>* Cannot start with a number or a hyphen (\-).<br><br>* Length must be between 1 and 128 characters.<br><br>* Can only contain letters, numbers, underscores (_), and hyphens (\-). |
   |Description |(Optional) Set a description for the search configuration. Length must not exceed 256 characters. |
   


<span id="1raMHBGl"></span>
## Edit search configuration

You can choose **Quick configuration** or **Advanced configurations**


<Tabs>
<Tab zoneid="L20hl6hSEr" title="Quick configuration">
<TabTitle>Quick configuration</TabTitle>

Configure the following items as needed.


|Parameter |Description |
|---|---|
|Full\-text search |Turn on or turn off as needed. Turned on by default. Configure the following parameters after turning on:<br><br><br>* Field name: Select the field used for full\-text search from the dropdown list. The field's **Type** must be **Text** and have the **Searchable** property checked. For more information, see [Create an index](https://docs.byteplus.com/en/docs/cloudsearch/Create_index).<br><br>* Weight: Configure the field's weight. Default value: **1.0**.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">At least one field must be configured.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Click <strong>add</strong> or the trash icon to add or delete a field.</div><br> |
|Vector retrieval |Turn on or turn off as needed. Turned on by default. When turned on, configure the following parameters:<br><br><br>* Model source: select **Default model** or **Ark model**.<br><br>* Model/inference service: select the model associated with the created inference service.<br><br>* API Key: select the created API Key. If you need a new API Key, see [Create an API Key](https://docs.byteplus.com/docs/6465/1359479).<br><br>* Field name: select the field used for vector retrieval from the index in the dropdown list. The **Type** of the field must be **Vector** and have the **Searchable** property checked. For more information, see [Create an index](https://docs.byteplus.com/en/docs/cloudsearch/Create_index).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Click <strong>add</strong> or the trash can icon to add or delete fields.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The selected field's dimension must match the dimension of the selected model/inference service.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Configuring vector search requires installing the <strong>opensearch\-remote\-reference</strong> plugin. For details, see <a href="https://docs.byteplus.com/en/docs/cloudsearch/manage-built-in-plugins?lang=zh">System built\-in plugin</a>.</div><br> |
|Return fields |Turn on or off as needed. Turned on by default. After turning on, select the fields to be queried and returned. Select at least one field. |
|Sorting fields |Enable or disable as needed. Enabled by default. After turning on, configure the following parameters:<br><br><br>* Field name: Select the field used for sorting in the index from the dropdown list. The field must have the **Aggregatable** attribute selected. For more information, see [Create an index](https://docs.byteplus.com/en/docs/cloudsearch/Create_index).<br><br>* Value: Choose **Ascending** or **Descending**.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Fields can be left unconfigured. When not configured, the returned content will be sorted in descending order by search score.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Click <strong>Add</strong> or the trash icon to add or delete fields.</div><br> |
|Other configurations |* Full text/vector search weight: score ratio between full\-text search and vector search in hybrid search.VectorVectorVector Configurable only when both **Full\-text search** and  ** Vector search** are enabled. The sum of both is 1.0. Default value: 0.50:0.50.<br><br>* Default returned quantity (optional): set the number of results returned. Default value: 10.<br><br>* Description (optional): set the description of the search template. Length must not exceed 256 characters. |


After configuring, click **Save**.


</Tab>
<Tab zoneid="axlfxYcYgB" title="Advanced configurations">
<TabTitle>Advanced configurations</TabTitle>

Select **Visual editing** or **user\-defined editing**.


<Tabs>
<Tab zoneid="zQL4SYVqfD" title="Visual editing">
<TabTitle>Visual editing</TabTitle>

1. Click the **query** node, expand **global configuration**, and then configure the following items.

   
   |Parameter |Description |
   |---|---|
   |Enter |Configure search input, including the following parameters:<br><br><br>* Variable: Enter the variable name.<br><br>* Type: Select **text** or **picture**.<br><br>* Default value: set the default value of the variable.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">At least one variable must be configured.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can click <strong>Add</strong> or the trash icon to add or delete variables.</div><br> |
   |Return to fields |Turn on or off as needed. Turned off by default. After turning on, select the fields to be queried and returned. At least one field must be selected. |
   |Sort field |Turn on or off as needed. Turned off by default. After turning on, click **Add** and then configure the following parameters:<br><br><br>* Field name: select the field used for sorting in the index from the dropdown list. The field must have the **Aggregatable** property checked. For more information, see [Create an index](https://docs.byteplus.com/en/docs/cloudsearch/Create_index).<br><br>* Value values: **Ascending** or **Descending**.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Field configuration is optional. If not configured, the returned content will be sorted in descending order by search score.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Click <strong>Add</strong> or the trash can icon to add or delete fields.</div><br> |
   |Reranking settings |Turn on or off as needed. Off by default. Configure the following parameters after turning on:<br><br><br>* Model/inference service: select a model associated with the created inference service.<br><br>* API Key: select an existing API Key. If you need a new API Key, see [Create an API Key](https://docs.byteplus.com/docs/6465/1359479).<br><br>* Reordering field: select the field used for reordering from the dropdown list.<br><br>* Reorder query statement: enter the query statement used for reordering. |
   |Other settings |Turn on or off as needed. Turned off by default. Enabling allows configuring the **Default returned quantity**.<br><br><br>* Default returned quantity: sets the number of returned results. Default value: 10.<br><br>* Description (optional): set the description of the search template. |
   

2. Click the  **+**  after the **query** node to add the required nodes in order. Example below.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_94423603eac84b096888ec6e3c3757f8.png) </span>


</Tab>
<Tab zoneid="SKS0EJceKq" title="Custom editing">
<TabTitle>Custom editing</TabTitle>

Enter JSON format configuration code in the **DSL Template** and  ** SearchPipeline **  code boxes.


</Tab>
</Tabs>


Click **Validate** at the top right corner of the page. After confirming the configuration is correct, click **Save**.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When selecting <strong>User\-defined editing</strong>, only format validation is supported; actual effects require search testing.</div>



</Tab>
</Tabs>


<span id="BDUDYwYN"></span>
## Manage search configuration versions

<span id="CnlcJ1Tx"></span>
### Create search configuration version


1. On the **Search configuration** tab, click **Version management** in the **Operation** column of the target search configuration.

2. In the search configuration panel, click **Create version** to create a new version, or select  **... \> Copy and create** after the target version to create a new version based on the target version.

3. Edit the search configuration. For more information, see [Edit search configuration](https://docs.byteplus.com/en/docs/cloudsearch/Manage_search_configurations?lang=zh#1raMHBGl).


<span id="AicD0vQ8"></span>
### Edit search configuration version


1. On the **Search configuration** tab, click **Version management** in the **Operation** column of the target search configuration.

2. In the search configuration panel, select  **... \> Edit** after the target version.

3. Edit the search configuration. For more information, see [Edit search configuration](https://docs.byteplus.com/en/docs/cloudsearch/Manage_search_configurations?lang=zh#1raMHBGl) for detailed steps.


<span id="VhgpLHIk"></span>
### Test search configuration version


1. Under the **search configuration** tab, click **version management** in the **actions** column of the target search configuration.

2. In the search configuration panel, select  **... \> Search test** after the target version.

3. In the **search test** window, choose **natural language** and enter keywords, or select **JSON query** and enter JSON code, then click **start test**.

4. Confirm whether the query statement corresponds with the search results.


<span id="8kgauglT"></span>
### Apply search configuration version


1. Under the **search configuration** tab, click **version management** in the **actions** column of the target search configuration.

2. In the search configuration panel, select  **...**  after the target version **Application**.

3. In the popup dialog, click **OK**.


<span id="4wdvaRfa"></span>
### View search configuration version differences


1. On the **search configuration** tab, click **version management** in the **actions** column of the target search configuration.

2. In the search configuration panel, select  **... \> View diff** after the target version.

3. In the **Version diff** window, select **Capability configuration item** or **Search template**.

4. Select the version to compare from the dropdown list on the right, then view the differences between the two versions.


<span id="gswWTpdS"></span>
### Delete search configuration version

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Deleted search configuration versions cannot be recovered; proceed with caution.</div>



1. On the **Search configuration** tab, click **Version** management in the Operation**actions** column of the target search configuration.

2. In the search configuration panel, select  **... \> Delete** after the target version.

3. In the popup dialog, click **OK**.
