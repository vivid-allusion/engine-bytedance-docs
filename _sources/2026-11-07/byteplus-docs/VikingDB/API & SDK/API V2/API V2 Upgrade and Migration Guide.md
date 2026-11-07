---
title: "API V2 Upgrade and Migration Guide"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/APIV2Upgrade"
---

<span id="98fa08b9"></span>
# Background

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To better accommodate multimodal retrieval use cases and improve API stability and usability, we have upgraded to API V2. This version provides richer multimodal capabilities, more intuitive interface design, and clearer error code responses. <strong>New features will be iterated only in the API V2 version going forward. We recommend upgrading to and using API V2.</strong></div>


<div data-tips="true" data-tips-type="warning">We provide this document to help users understand and use the latest API V2 interfaces. We will also provide supporting SDK capabilities in the future.</div>


<span id="50572335"></span>
# **API V2 Upgrade Content Introduction**

<span id="2d3831f2"></span>
## Richer Features

More product features will be developed and provided to users through API V2 interfaces only. The following introduces capabilities that will be launched soon:


|**New Features** |**Description** |
|---|---|
|New video data writing and retrieval functionality |End\-to\-end vectorization capability for videos, supporting direct video data writing, automatic vectorization, and retrieval of video data in any modality. |
|Image data writing supports generic URL format |No longer requires users to write data with TOS URLs only. Data type restrictions have been relaxed, making it more user\-friendly for customers whose raw data is on other clouds. |
|Launch of multi\-keyword retrieval functionality |Supports users specifying multiple keywords for vector and keyword retrieval, suitable for keyword retrieval scenarios. |
|Image data writing supports TOS URL input after image processing |For images in TOS, since TOS already supports some image processing capabilities, we have integrated this functionality to support direct vectorization with TOS post\-processed URLs. [Image Processing Overview](https://docs.byteplus.com/en/docs/tos/docs-overview_2) |
|Temporary removal of sub\-index functionality |PartitionBy parameter in index management, partition parameter in data query and retrieval are temporarily not supported. This feature will be supported in the future in a more powerful and user\-friendly implementation. |


<span id="632fc84f"></span>
## More Intuitive Interfaces

In the API V2 version, for easier use, interfaces are divided into **Data Plane APIs** and **Control Plane APIs** by function, making it easier for users to quickly locate required interfaces and understand their functions.

**Data Plane APIs**

**Interfaces for operating on business data itself,**  such as data writing, updating, deleting, vectorization, point queries, and various retrieval capabilities. These are typically interfaces directly integrated and called by business parties, featuring **high throughput and low latency**. Request and response parameters use lowercase snake_case naming convention.

**Control Plane APIs**

**Interfaces for configuring or managing vector database resources,**  including creation, update, deletion, and query capabilities for datasets, indexes, and offline tasks. These are typically low\-frequency interfaces called by businesses. We maintain the same control plane interface style as other BytePlus products. Request and response parameters use UpperCamelCase naming convention.


* ### **Data Plane APIs**   <span id="data-plane-apis"></span>


Responsible for directly processing business data, including data writing, reading, deletion, and retrieval operations. Includes:

<span id="bf5544dc"></span>
#### Data Operations


|**Interface Capability** |**Interface Name** |**Upgrade Differences** |
|---|---|---|
|Data Writing |[UpsertData](https://docs.byteplus.com/docs/VikingDB/UpsertData_V2) |Automatically returns model consumption tokens, data limit optimizations, etc. |
|Data Update |[UpdateData](https://docs.byteplus.com/docs/VikingDB/UpdateData_V2) |Automatically returns model consumption tokens, data limit optimizations, etc. |
|Data Deletion |[DeleteData](https://docs.byteplus.com/docs/VikingDB/DeleteData_V2) |Changed the primary key parameter name from primary_keys to ids. |
|Point Query in Dataset |[FetchDataIn(Collection)](https://docs.byteplus.com/docs/VikingDB/FetchDataIn_Collection_V2) |The primary key parameter name is changed from primary_keys to ids, and primary keys are now listed separately in the response. |
|Point Query in Index |[FetchDataIn(Index)](https://docs.byteplus.com/docs/VikingDB/FetchDataIn_Index_V2) |The primary key parameter name is changed from primary_keys to ids, and primary keys are now listed separately in the response. |


<span id="a361d120"></span>
#### Retrieval Capabilities

Public parameters for retrieval have been systematically organized, **making them clearer and easier for you to choose the appropriate retrieval method for your business scenario.** 

Interface design differences: V1 interfaces placed various retrieval modes in the same interface, distinguished by different parameter combinations. **In V2, each retrieval mode has a corresponding interface, with parameters composed of common parameters and mode\-specific parameters.** 

**Common Parameters**

Refer to: [Common Search Parameters](https://docs.byteplus.com/docs/VikingDB/Common_Search_Parameters_V2)

**Differential Parameters**


|**Interface Capability** |**Interface Name** |**Differential Parameters** |
|---|---|---|
|Vector Retrieval/Dense\-Sparse Vector Hybrid Retrieval |[Vector Search](https://docs.byteplus.com/docs/VikingDB/Vector_Search_V2) |Set dense vector parameter dense_vector<br><br>Set sparse vector parameter sparse_vector (sparse vector is optional) |
|Multimodal Retrieval |[Multimodal Search](https://docs.byteplus.com/docs/VikingDB/Multimodal_Search_V2) |Set text parameter text (optional)<br><br>Set image parameter image (optional)<br><br>Set instruction parameter need_instruction (optional) |
|ID Retrieval |[Id Search](https://docs.byteplus.com/docs/VikingDB/Id_Search_V2) |Set parameter id |
|Scalar Sorting Retrieval |[Scalar Sort Search](https://docs.byteplus.com/docs/VikingDB/Scalar_Sort_Search_V2) |Set scalar parameter field<br><br>Set sort order parameter order |
|Random Retrieval |[Random Search](https://docs.byteplus.com/docs/VikingDB/Random_Search_V2) |None |
|Keyword Retrieval |[Keyword Search](https://docs.byteplus.com/docs/VikingDB/Keyword_Search_V2) |Set keyword list parameter keywords<br><br>Set case sensitivity parameter case_sensitive<br><br>This is a new capability. |


**Embedding Calculation**


|**Interface Capability** |**Interface Name** |**Upgrade Differences** |
|---|---|---|
|Vectorization Calculation |[Embedding Calculation](https://docs.byteplus.com/docs/VikingDB/Embedding_Calculation_V2) |Dense and sparse models can be specified independently, supporting any combination of dense+sparse, dense\-only, or sparse\-only embedding calculation.<br><br>Automatically returns model consumption tokens.<br><br>Default limit of no more than 10 data items per request, but with lower latency. For improvements, please contact Oncall. |



* ### **Control Plane APIs**   <span id="control-plane-apis"></span>


These APIs are responsible for resource management and configuration, such as managing datasets, indexes, tasks, and their associated metadata. Includes:

<span id="366d04c0"></span>
#### Dataset Management


|**Interface Capability** |**Interface Name** |**Upgrade Differences** |
|---|---|---|
|Create Dataset |[Create Vikingdb Collection](https://docs.byteplus.com/docs/VikingDB/Create_Collection_V2) |Parameter naming style changed to camelCase.<br><br>Vectorize parameter type adjustment: from []map to map.<br><br>Primary key parameter position adjustment. |
|Delete Dataset |[Delete Vikingdb Collection](https://docs.byteplus.com/docs/VikingDB/Delete_Collection_V2) |Parameter naming style changed to camelCase. |
|Update Dataset |[Update Vikingdb Collection](https://docs.byteplus.com/docs/VikingDB/Update_Collection_V2) ||
|View Dataset Details |[Get Vikingdb Collection](https://docs.byteplus.com/docs/VikingDB/Get_Collection_V2) ||
|View Dataset List |[List Vikingdb Collection](https://docs.byteplus.com/docs/VikingDB/List_Collection_V2) ||


<span id="bff8db26"></span>
#### Index Management


|**Interface Capability** |**Interface Name** |**Upgrade Differences** |
|---|---|---|
|Create Index |[Create Vikingdb Index](https://docs.byteplus.com/docs/VikingDB/Create_Index_V2) |Parameter naming style changed to camelCase. |
|Delete Index |[Delete Vikingdb Index](https://docs.byteplus.com/docs/VikingDB/Delete_Index_V2) ||
|Update Index |[Update Vikingdb Index](https://docs.byteplus.com/docs/VikingDB/Update_Index_V2) ||
|View Index Details |[Get Vikingdb Index](https://docs.byteplus.com/docs/VikingDB/Get_Index_V2) ||
|View Index List |[List Vikingdb Index](https://docs.byteplus.com/docs/VikingDB/List_Index_V2) ||


<span id="ebbcfa41"></span>
#### Task Management


|**Interface Capability** |**Interface Name** |**Upgrade Differences** |
|---|---|---|
|Create Offline Task |[Create Vikingdb Task](https://docs.byteplus.com/docs/VikingDB/Create_Task_V2) |Parameter naming style changed to camelCase. |
|Delete Offline Task |[Delete Vikingdb Task](https://docs.byteplus.com/docs/VikingDB/Delete_Task_V2) ||
|Update Offline Task |[Update Vikingdb Task](https://docs.byteplus.com/docs/VikingDB/Update_Task_V2) ||
|View Offline Task List |[List Vikingdb Task](https://docs.byteplus.com/docs/VikingDB/List_Task_V2) ||
|View Offline Task Details |[Get Vikingdb Task](https://docs.byteplus.com/docs/VikingDB/Get_Task_V2) ||


<span id="079e4924"></span>
## Clearer Error Codes and Troubleshooting Guide


|**V1 Error Codes and Troubleshooting Guide** |**V2 Error Codes and Troubleshooting Guide** |
|---|---|
|[Error codes for troubleshooting](https://docs.byteplus.com/docs/VikingDB/Error_codes_for_troubleshooting) |[API V2 Error Codes and Troubleshooting Guide](https://docs.byteplus.com/docs/VikingDB/FAQnew) |


<span id="299535b2"></span>
## Private Network Connection Service Update

Endpoint [Region and Endpoint](https://docs.byteplus.com/docs/undefined/68aecf6f817cd302c85e8ef4), Private[Connecting to VikingDB via a private link](https://docs.byteplus.com/docs/VikingDB/69762)


* **API V2 Data Plane**



|**Region Name** |**Region ID** |**Public Network Domain Name** |**PrivateLink Service Name** |
|---|---|---|---|
|Asia Pacific (Johor) |ap\-southeast\-1 |[api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com](http://api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com/) |com.bytepluses.privatelink.ap\-southeast\-1.vikingdb\-ann |



* **API V2 Control Plane**



|**Region Name** |**Region ID** |**Public Network Domain Name** |**PrivateLink Service Name** |
|---|---|---|---|
|Asia Pacific (Johor) |ap\-southeast\-1 |[vikingdb.ap-southeast-1.byteplusapi.com](http://vikingdb.ap-southeast-1.byteplusapi.com/) |com.bytepluses.privatelink.ap\-southeast\-1.api.vikingdb |


<span id="c2255402"></span>
# **API V2 Migration Guide**

<span id="98eafb14"></span>
## Preparation Before Upgrade

We will automatically confirm whether your datasets are suitable for using API V2 interfaces. If not, you can continue using the old API interfaces without any impact.

If you are willing to upgrade, please refer to the upgrade steps.

<span id="1cf38661"></span>
## Upgrade Steps


|**Step** |**Operation** |**Screenshot** |
|---|---|---|
|**Step 1: Console Upgrade.**  |You can complete the upgrade with one click by clicking the upgrade new version button on the page.<br><br>The console will automatically use API V2 interfaces to request your vector database, and incompatible datasets/indexes will also be marked, which can still be used through the old interfaces. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c0a03f000aec4c9b84f7de5cb7a07b17~tplv-goo7wpa0wc-image.image) </span> |
|**Step 2: New Interface Call.**  |Due to interface upgrades, TOS services need to be reauthorized. On the **Create Dataset** page, you need to reauthorize your TOS service.<br><br>Then you can refer to the upgrade documentation to use your vector database through API V2 interfaces. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c483db3de9e840ed9f51fafdc0b7b288~tplv-goo7wpa0wc-image.image) </span> |
|**Step 3: Testing** |**Perform functional and performance testing.**  Ensure that the vector storage, retrieval, and control plane interfaces work properly for your business use case.<br><br>If requirements cannot be met, you can click to return to the old version. | |
|**Step 4: Production Use** |**Switch to production use.**  | |


<span id="ceed05a2"></span>
## Notes


* **Version Compatibility:**  After upgrading to use API V2 interfaces, you can still use the old API interfaces. However, if there are no issues, it is recommended to migrate as soon as possible. New product features will be released for the API V2 interfaces.

* **Data Migration Required:**  No migration needed. Data will not be affected in any way. Only the calling method is updated. Any dataset can still use API V1 interfaces.


<span id="8c6b1516"></span>
## Frequently Asked Questions


* **Q1: The new version is not user\-friendly. How can I roll back to the old API?** 


You can switch back to the old version by clicking on the page. At the interface level, you can directly call the original API interfaces. We welcome feedback on any usability issues, and we will continue to optimize.


* **Q1: What improvements does the new version offer?** 


The introduction to this document describes improvements in new features, interface usability, and other areas.


* **Q3: I am a new user. How do I use API V2?** 


New users are directed to the new version page by default. You can directly use it according to the page instructions.


* **Q4: Can I refer to current best practices?** 


The current quick start and best practices are still implemented with the old API V1. We will gradually update them in the future.
