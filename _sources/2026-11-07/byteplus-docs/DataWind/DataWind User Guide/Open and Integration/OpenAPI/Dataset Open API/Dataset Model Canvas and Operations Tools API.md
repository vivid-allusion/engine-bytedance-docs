---
title: "Dataset Model Canvas and Operations Tools API"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Dataset_Model_Canvas_and_Operations_Tools_API"
---

<span id="_1-概述"></span>
# 1. Overview

This document introduces the Open API for dataset model canvas and operations tools, allowing users to view dataset model canvas information, refresh base table metadata, and perform other operations through the API.

Caution: Before using the APIs described in this document, you must complete the prerequisite steps of integrating JWT\-Token and applying for a Token. Please review the invocation method first. For details, see [Invocation Methods](https://docs.byteplus.com/docs/DataWind/Invocation_Methods).

<span id="_3-查看数据集模型画布信息"></span>
# 2. View dataset model canvas information


* Permission requirements.

   
   |Resource |Permission |
   |---|---|
   |Dataset |read |
   

* API description and notes: This API only allows viewing the dataset model canvas information, including the field selection status of upstream data source nodes used in the dataset, data source information, join relationships between data sources, and filter conditions of each data source.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bfecb083410cc6921787dccfa52fe165.png) </span>


<span id="1438570b"></span>
#### Request description


* Request URL: `{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/model`


<span id="079f381d"></span>
#### Request example

```bash
curl --location --request GET '{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/model' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}'
```


<span id="f9b9c486"></span>
#### Request parameters


|Parameter |Type |Required |Enumeration value |Description |
|---|---|---|---|---|
|dataSetId |integer |Yes |123 |Dataset ID |


<span id="633633f9"></span>
#### Response parameters


|Parameter |Type |Description |
|---|---|---|
|$.nodeConf |list |Dataset model canvas information |
|$.nodeConf[i].tbName |string |Data source node table name |
|$.nodeConf[i].tableAlias |string |Data source node table alias |
|$.nodeConf[i].dbName |string |Data source node database name |
|$.nodeConf[i].dataSourceId |integer |Data source ID |
|$.nodeConf[i].clusterName |string |Data source cluster information |
|$.nodeConf[i].nodeId |string |Node ID of the data source in the canvas |
|$.nodeConf[i].nodeType |integer |Node type of the data source in the canvas |
|$.nodeConf[i].fields |list |Field information of the data source node |
|$.nodeConf[i].fields[i].type |string |Data source node field type |
|$.nodeConf[i].fields[i].name |string |Data source node field name |
|$.nodeConf[i].fields[i].alias |string |Data source node field alias \-\> Used when there are fields with the same name from different data sources |
|$.nodeConf[i].fields[i].comment |string |Data source node field comment |
|$.nodeConf[i].fields[i].status |integer |Data source node field status |
|$.nodeConf[i].fields[i].isSelect |bool |Whether the data source node field is selected<br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e5af91951eb7aa4061afb6f297229a99.png) </span> |


<span id="181424a6"></span>
#### Response example

```json
{
    "code": "aeolus/ok",
    "data": {
        "dagTagConf": {
            "dimTbNodes": []
        },
        "linkConf": [],
        "nodeConf": [
            {
                "clusterName": "cn",
                "dataSourceId": 2****,
                "dataSourceType": "ch_excel",
                "dbName": "aeolus_excel_upload_aeolus_toy",
                "displayDbName": "配比四刷-v4",
                "fields": [
                    {
                        "alias": "`字段四`",
                        "comment": null,
                        "isDynamicPartition": false,
                        "isSelect": true,
                        "isSourceTableField": false,
                        "name": "字段四",
                        "prepType": "string",
                        "status": 0,
                        "type": "Nullable(String)"
                    },
                    {
                        "alias": "`字段一`",
                        "comment": null,
                        "isDynamicPartition": false,
                        "isSelect": true,
                        "isSourceTableField": false,
                        "name": "字段一",
                        "prepType": "string",
                        "status": 0,
                        "type": "Nullable(String)"
                    },
                    {
                        "alias": "`字段三`",
                        "comment": null,
                        "isDynamicPartition": false,
                        "isSelect": true,
                        "isSourceTableField": false,
                        "name": "字段三",
                        "prepType": "string",
                        "status": 0,
                        "type": "Nullable(String)"
                    },
                    {
                        "alias": "`字段二`",
                        "comment": null,
                        "isDynamicPartition": false,
                        "isSelect": true,
                        "isSourceTableField": false,
                        "name": "字段二",
                        "prepType": "string",
                        "status": 0,
                        "type": "Nullable(String)"
                    }
                ],
                "fileId": "13***",
                "fullOption": false,
                "hiveOwner": "userEmailPrefix",
                "lastDdlTime": "2022-12-13 12:49:00",
                "metadataLink": "https://data.bytedance.net/coral/datamap/detail/table_info/clickhouse/aeolus_excel_upload_aeolus_toy/table_4f0cc551_9dfa_4915_****_***********#group=default",
                "nodeId": "77b3df39-834c-****-****-************",
                "nodeType": "table",
                "params": {
                    "extractType": "{\"key\":\"full\"}"
                },
                "partitionConfList": [],
                "query": "",
                "schemaName": "Sheet1",
                "tableAlias": "table_4f0cc551_9dfa_****_****_*********",
                "tableRowFilter": {},
                "tbId": "cn//aeolus_excel_upload_aeolus_toy//table_4f0cc551_9dfa_4915_a38******",
                "tbName": ""table_4f0cc551_9dfa_****_****_*********"
            }
        ],
        "parseEngine": 0,
        "whereConf": {
            "nodeRowFilter": {},
            "requiredRowFilter": []
        }
    },
    "msg": "成功"
}
```


<span id="_4-底表元数据刷新"></span>
# 3. Refresh base table metadata


* Supported in **version 58.1** and above.

* Permission requirements

   
   |Resource |Permission |
   |---|---|
   |Dataset |admin |
   

* API description and notes: Refreshes the keyword information of the base table corresponding to the extracted dataset. Supports refreshing sort keys and sample keys (not supported in SaaS environments).


<span id="d1201c8e"></span>
#### Request description


* Request URL: `{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/refreshDataTable`


<span id="be068dfe"></span>
#### Request example

```bash
curl --location --request GET '{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/refreshDataTable' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}' \
```


<span id="9cd55c96"></span>
#### Response example

```json
#data为更新后的关键字信息
{
    "code": "aeolus/ok",
    "data": {{"sample_key": "row_id_kmtq3k", "source_type": "Normal", "cnch_vw_default": "aeolus-turtle-lambda-default", "cnch_vw_write": "aeolus-turtle-lambda-write", "primary_key_list": ["row_id_km****"], "shard_key": "row_id_km****"}},
    "msg": "成功"
}
```
