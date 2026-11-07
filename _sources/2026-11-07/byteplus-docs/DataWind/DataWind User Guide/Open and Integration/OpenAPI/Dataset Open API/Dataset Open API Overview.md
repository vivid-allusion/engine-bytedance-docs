---
title: "Dataset Open API Overview"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Dataset_Open_API_Overview"
---

<span id="_1-概述"></span>
# 1. Overview

**Dataset Open API** provides APIs for operations related to datasets, allowing flexible dataset access through open capabilities. The Dataset Open API mainly includes: dataset operation APIs, dataset information APIs, dataset synchronization task APIs, dataset visual query parameter APIs, dataset model canvas and operations and maintenance tool APIs, project dataset tag and folder APIs, project dataset and data source APIs, and project cluster configuration APIs. This document provides a brief introduction to the Dataset Open API. Other APIs will be introduced in separate documents.

Caution: Before you start using the interfaces described in this document, please first understand the [Invocation Methods](https://docs.byteplus.com/docs/DataWind/Invocation_Methods).

<span id="_4-所有数据集接口介绍"></span>
# 2. Introduction to all dataset interfaces


* The new V4 version of the interfaces adopts a standard RESTful interface naming convention, that is, resource plus action naming.

* The documentation is organized by resource. To perform an operation on a specific resource, find the corresponding action API under the relevant documentation section.

* Each interface provides a cURL example that can be directly imported into Postman for customer convenience. Since the DataWind domain name and each request in different environments contain common variables, all cURL examples for each interface use {{}} to enclose variables. The `{{variable}}` format can be directly recognized by Postman.


Variable meaning reference table:

```JSON
jwtToken -> {{jwtToken}}
aeolus 域名 -> {{domain}} 
项目 ID -> {{appId}} 
数据集 ID -> {{dataSetId}} 
数据集标签 Id {{tagId}}
数据集文件夹 Id {{dataSetFolderId}}
```


Applicable product version for this document: 2.48.0 and above


|Interface type |Interface description |Detailed documentation |
|---|---|---|
|Dataset operation API |Users can use the API to update, move, and delete datasets, check and move datasets to the recycle bin, and perform other operations. |[Dataset Operation API](https://docs.byteplus.com/docs/DataWind/Dataset_Operation_API) |
|Dataset information API |Users can use the API to view the basic information on the dataset details and edit pages, update basic information, set tags, and perform other operations. |[Dataset Information API](https://docs.byteplus.com/docs/DataWind/Dataset_Information_API) |
|Dataset synchronization task API |Users can use the API to view and update dataset synchronization task settings, submit a backtracking task for dataset synchronization, terminate dataset synchronization task instances, and perform other operations. |[Dataset Synchronization Task API](https://docs.byteplus.com/docs/DataWind/Dataset_Synchronization_Task_API) |
|Dataset visual query parameter API |Users can view and update visualization query parameter configurations through the API. |[Dataset Visualization Query Parameters API](https://docs.byteplus.com/docs/DataWind/Dataset_Visualization_Query_Parameters_API) |
|Dataset model canvas and operations and maintenance tools API |Users can perform operations such as viewing the dataset model canvas and refreshing base table metadata through the API. |[Dataset Model Canvas and Operations Tools API](https://docs.byteplus.com/docs/DataWind/Dataset_Model_Canvas_and_Operations_Tools_API) |
|Dataset API within a project |Users can use the API to retrieve, create, and update dataset information and folder information within a project, as well as retrieve, add, and delete the list of users with write access to a private cluster. |[Project-Level Dataset APIs](https://docs.byteplus.com/docs/DataWind/Project-Level_Dataset_APIs) |
