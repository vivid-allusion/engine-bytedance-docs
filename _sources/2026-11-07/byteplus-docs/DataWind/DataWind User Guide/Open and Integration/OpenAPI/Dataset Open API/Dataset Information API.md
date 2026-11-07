---
title: "Dataset Information API"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Dataset_Information_API"
---

<span id="_1-概述"></span>
# 1. Overview

This document introduces the "Open API for dataset information". You will learn how users can use the API to view the basic information on the dataset details page and edit page, as well as perform operations such as updating basic information and setting tags.

Caution: Before using the APIs described in this document, you must complete the prerequisites of integrating JWT\-Token and applying for a Token. Please familiarize yourself with the invocation method. For details, see [Invocation Methods](https://docs.byteplus.com/docs/DataWind/Invocation_Methods).

<span id="_3-接口介绍"></span>
# 2. API introduction

<span id="_3-1-查看数据集信息-详情页"></span>
## 2.1 View dataset information \- details page


* Permission requirements

   
   |Resource |Permission |
   |---|---|
   |Dataset |read |
   

* API description and notes: Obtain the dataset information displayed on the dataset details page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/97801541f6984b84a9de9da3badf027b~tplv-goo7wpa0wc-image.image) </span>


<span id="c23a0ea9"></span>
#### Request description


* Request URL: `{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/overview`


<span id="7a1ba522"></span>
#### Request example

```bash
curl --location --request GET '{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/overview' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}'
```


<span id="f7675702"></span>
#### Request parameters


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|dataSetId |integer |Yes |123 |For how to obtain the dataset ID, see [How to Obtain Resource IDs](https://docs.byteplus.com/docs/DataWind/How_to_Obtain_Resource_IDs) |


<span id="d9d7b1e5"></span>
#### Response parameters


|**Parameter** |**Type** |**Description** |
|---|---|---|
|accessCount |integer |Page views (PV) of related dataset chart pages in the past 30 days |
|appId |integer |Project ID |
|connectionMode |integer |Dataset connection mode [0: extraction, 1: direct connection] |
|ctime |datetime |Dataset creation time |
|dagTagConf.dimTbNodes |list |Dimension table node ID |
|demoUrl |string |Dataset usage instructions |
|descr |string |Dataset description |
|doradoPriority |string |Synchronization task priority [normal, high, super_high] |
|driverName |string |Database driver name |
|editable |boolean |Whether the dataset can be edited [true, false] |
|frequency |string |Dataset synchronization frequency [daily, hourly, weekly, monthly] |
|hot |integer |Access frequency [0: no frequency] |
|id |integer |Dataset ID |
|lastSyncTime |datetime |Last synchronization time |
|lineNum |integer |Number of data entries stored in the dataset |
|mtime |datetime |Last modified time of the dataset |
|name |string |Dataset name |
|onPrivateCluster |integer |Whether the dataset is created on a private cluster [0: not a private cluster; 1: private cluster] |
|roleList |list |Dataset permissions owned by the current token identity [admin (owner), read_role (read role), write_role (write role), view_only_role (view\-only role), read_all_role (global view role)] |
|size |float |Data size stored in the dataset [unit is dynamic, may be KB, MB, GB, and so on] |
|sourceKey |string |Dataset creation/output source [abi, cdp, prep]<br><br>Note: prep indicates a dataset generated through visual modeling |
|status |integer |Dataset status; 0 means normal status |
|syncMode |integer |Synchronization mode [0: Bdb to ClickHouse channel tasks, 1: visual modeling tasks, 2: Bdp hsql tasks using tqs for import] |
|syncType |integer |Synchronization scheduling mode [1 for automatic synchronization; 2 for manual synchronization] |
|ttl |integer |Dataset lifecycle \-\> Data retention period, default is 7 days<br><br>Note: The definition is the dataset's lifecycle, but in practice it refers to the data retention period of the dataset. For example, if the default is 7 days, then all data generated more than 7 days ago will be deleted. |
|type |integer |Dataset type [Common types: 0: Dataset generated from a ClickHouse table as the data source, 2: Dataset generated from a Hive table as the data source, 8: Dataset generated from custom SQL, 10: Dataset generated from a MySQL table as the data source, 22: Prep type dataset] |
|writePartition |integer |Write partition [0 for day partition; 1 for day + hour partition] |
|sensitiveConf |string |Dataset data masking settings [undef: not set; sensitiveWithoutDe: sensitive but not masked; sensitiveWithDe: sensitive and masked; unsensitive: not sensitive] |


<span id="8cb03469"></span>
#### Response example

```json
{
    "code": "aeolus/ok",
    "data": {
        "accessCount": 0,
        "appId": 77*****,
        "connectionMode": 0,
        "ctime": "2022-12-14 12:17:54",
        "dagTagConf": {
            "dimTbNodes": []
        },
        "dataSetLabelType": 0,
        "demoUrl": "http://xxx.com",
        "descr": "这是一段描述，描述数据集的作用",
        "disablePreview": 0,
        "doradoPriority": "normal",
        "driverName": "click_house",
        "editable": true,
        "frequency": "daily",
        "groupType": 0,
        "hot": 0,
        "id": {{dataSetId}},
        "isAppAdminView": 1,
        "lastSyncTime": "2022-12-14 12:38",
        "lineNum": "56",
        "mtime": "2022-12-14 12:18",
        "name": "测试open-api专用数据集1",
        "onPrivateCluster": 0,
        "ownerEmailPrefix": "userEmailPrefix",
        "parentId": 3075,
        "partitionRange": [
            {
                "id": 158**********,
                "max": "2022-12-13",
                "min": "2022-12-13",
                "name": "p_date"
            }
        ],
        "previewInfo": "",
        "retryNum": 0,
        "roleList": [
            {
                "action": "admin",
                "roleName": "所有者"
            },
            {
                "action": "view_only_role",
                "roleName": "仅阅览角色"
            },
            {
                "action": "write_role",
                "roleName": "写角色"
            },
            {
                "action": "read_role",
                "roleName": "读角色"
            }
        ],
        "size": "2.86KB",
        "slaStatus": 0,
        "sourceKey": "abi",
        "status": 0,
        "statusDesc": "正常",
        "syncMode": 2,
        "syncType": 1,
        "tagInfo": null,
        "thirdPartyConf": {},
        "ttl": 7,
        "type": 22,
        "uneditableReason": null,
        "writePartition": 0,
        "yarnName": "root.default_hrtech_da_pm"
    },
    "msg": "成功"
}
```


<span id="_3-2-查看数据集完整信息-编辑页"></span>
## 2.2 View complete dataset information \- edit page


* Permission requirements

   
   |Resource |Permission |
   |---|---|
   |Dataset |read |
   

* API description and notes: Obtain complete dataset information, corresponding to the dataset edit page on the frontend.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/475af3ca6104439097730b42dffd6df0~tplv-goo7wpa0wc-image.image) </span>


<span id="4f467e5d"></span>
#### Request description

Request URL: `{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/info`

<span id="d2d445e3"></span>
#### Request example

```bash
curl --location --request GET '{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/info' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}'
```


<span id="32e589d4"></span>
#### Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|dataSetId |integer |Yes |123 |Dataset ID. For how to obtain it, see [How to Obtain Resource IDs](https://docs.byteplus.com/docs/DataWind/How_to_Obtain_Resource_IDs) |


<span id="504b8100"></span>
#### Response parameters


|Parameter (jsonPath) |Type |Description |
|---|---|---|
|$.baseConf |object |[Dataset Open API Overview](https://docs.byteplus.com/docs/DataWind/Dataset_Open_API_Overview) |
|$.baseConf.appId |integer |Project ID |
|$.baseConf.demoUrl |string |Dataset usage instructions |
|$.baseConf.name |string |Dataset name |
|$.baseConf.ownerEmailPrefix |string |Dataset owner |
|$.baseConf.parentId |integer |Folder containing the dataset; 0 indicates the root directory |
|$.baseConf.syncMode |integer |Synchronization mode [1 for manual; 2 for automatic] |
|$.baseConf.type |integer |Dataset type [Common types: 0: Dataset generated from a ClickHouse table as the data source, 2: Dataset generated from a Hive table as the data source, 8: Dataset generated from custom SQL, 10: Dataset generated from a MySQL table as the data source, 22: Prep type dataset] |
|$.dagTagConf.dimTbNodes |list |Dataset dimension table node nodeId |
|$.syncConf |object |[Dataset Synchronization Task API](https://docs.byteplus.com/docs/DataWind/Dataset_Synchronization_Task_API) |
|$.whereConf |object |Dataset model data source node filter conditions and global filter conditions |


<span id="response-example"></span>
#### Response example  

```json
{
    "code": "aeolus/ok",
    "data": {
        "baseConf": {
            "appId": 77*****,
            "connectionMode": 0,
            "demoUrl": null,
            "descr": "这是一段描述，描述数据集的作用",
            "generalTags": [],
            "groupType": 0,
            "id": {{dataSetId}},
            "isAuthEnabled": 1,
            "isIntelligentSyncEnable": 1,
            "lineOfBusiness": [],
            "name": "测试open-api专用数据集1",
            "ownerEmailPrefix": "userEmailPrefix",
            "parentId": 3075,
            "productName": "",
            "regionType": [],
            "syncMode": 2,
            "thirdPartyConf": null,
            "type": 22
        },
        "dagTagConf": {
            "dimTbNodes": []
        },
        "dimMetList": [
            {
                "calcType": null,
                "dataFormat": null,
                "dataTypeName": "date",
                "defaultDataTypeName": "date",
                "descr": "p_date",
                "dimMetCategoryId": null,
                "dimMetCategoryType": null,
                "dimMetMixOrder": 0,
                "dimMetOrder": 0,
                "dimMetThirdPartyConf": null,
                "dimMetVariety": 1,
                "editable": 0,
                "errCode": "ok",
                "expr": "p_date",
                "exprAsDim": null,
                "fieldList": "[\"p_date\"]",
                "fullExpr": "p_date",
                "groupType": 0,
                "hitFilterRuleList": [],
                "id": 158**********,
                "isDeletedField": 0,
                "isPartitionField": 1,
                "lodType": null,
                "mapType": 0,
                "name": "p_date",
                "operationCode": 0,
                "ownerEmailPrefix": "userEmailPrefix",
                "paramIdList": [],
                "showExpr": 1,
                "visible": 1
            },
            .........
        ],
        "labelConf": {
            "dataSetLabelType": 0,
            "labelParams": null,
            "subjectList": null
        },
        "linkConf": [],
        "nodeConf": [
            {
                "clusterName": "cn",
                "dataSourceId": 25***,
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
                "fileId": "13516",
                "fullOption": false,
                "hiveOwner": "userEmailPrefix",
                "lastDdlTime": "2022-12-13 12:49:00",
                "metadataLink": "https://data.bytedanc*.net/coral/datamap/detail/table_info/clickhouse/aeolus_excel_upload_aeolus_toy/table_4f0cc551_9dfa_****_****_**********#group=default",
                "nodeId": "77b3df39-834c-4da4-908e-4b54846bc599",
                "nodeType": "table",
                "params": {
                    "extractType": "{\"key\":\"full\"}"
                },
                "partitionConfList": [],
                "query": "",
                "schemaName": "Sheet1",
                "tableAlias": "table_4f0cc551_9dfa_4915_****_************",
                "tableRowFilter": {},
                "tbId": "cn//aeolus_excel_upload_aeolus_toy//table_4f0cc551_9dfa_4915_****_************",
                "tbName": "table_4f0cc551_9dfa_4915_****_************"
            }
        ],
        "parseEngine": 0,
        "syncConf": {
            "backtrackingConf": {
                "dateRange": {
                    "endDate": "2022-12-13",
                    "startDate": "2022-12-13"
                },
                "enable": 1
            },
            "doradoPriority": "normal",
            "frequency": "daily",
            "monitorConf": {
                "alarmRules": [
                    {
                        "failedAlarmItems": [
                            {
                                "item": "retry_failed"
                            }
                        ],
                        "id": 6826,
                        "name": "auto_aeolus_rule_{{dataSetId}}_167099*******_dev",
                        "normalNoticeConf": [
                            {
                                "dutySchedules": [],
                                "noticeChannel": "lark",
                                "users": [
                                    "userEmailPrefix"
                                ]
                            }
                        ],
                        "resultAlarmItems": [],
                        "timeoutAlarmItems": []
                    }
                ]
            },
            "paramsConfList": [
                {
                    "name": "tqs.query.auto.retry.enable",
                    "value": "true"
                }
            ],
            "performanceSettings": {
                "chQueryParams": {},
                "clusterName": "cnch_alpha_lq",
                "cnchVwDefault": "vw_default",
                "cnchVwWrite": "vw_write",
                "dataSourceId": 14*,
                "driverName": "click_house",
                "partitionKey": [
                    "p_date"
                ],
                "primaryKeyList": [],
                "sampleKey": null,
                "sampleRate": 1.0,
                "shardKey": null
            },
            "retryInterval": 5,
            "retryNum": 1,
            "scheduleDay": "0",
            "scheduleTime": "00:00",
            "scheduleTimeType": 0,
            "slaDaytime": null,
            "slaStatus": 0,
            "syncType": 1,
            "ttl": 7,
            "upstreamSettings": {
                "dynamicPartitionConfList": [],
                "dynamicPartitionMode": false,
                "partitionConfList": [],
                "uniqueIndexList": []
            },
            "writePartition": 0,
            "yarnName": "root.default_hrtech_da_pm"
        },
        "whereConf": {
            "nodeRowFilter": {},
            "requiredRowFilter": []
        }
    },
    "msg": "成功"
}
```


<span id="_3-3-查看数据集基础信息"></span>
## 2.3 View basic dataset information


* Permission requirements

   
   |Resource |Permission |
   |---|---|
   |Dataset |read |
   

* API description and notes: Obtain basic dataset information, which can be used to roughly display the dataset content when integrating with third\-party systems.


<span id="858afcae"></span>
#### Request description


* Request URL: `{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/digest`


<span id="80160bb8"></span>
#### Request example

```bash
curl --location --request GET '{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/digest' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}'
```


<span id="ce5757a9"></span>
#### Request parameters


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|dataSetId |integer |Yes |123 |Dataset ID. For how to obtain it, see [How to Obtain Resource IDs](https://docs.byteplus.com/docs/DataWind/How_to_Obtain_Resource_IDs) |
|folderPath |integer |No |0 |Whether a complete folder path is required [0 not required; 1 required] |


<span id="6e3c9f19"></span>
#### Response parameters


|Name |Type |Description |
|---|---|---|
|id |integer |Dataset ID |
|appID |integer |Project ID |
|appName |string |Project name |
|detailUrl |string |Dataset frontend page address, can be directly accessed |
|folderName |list |Dataset folder path \-\> **The root directory is the default value, indicating that this dataset is not stored in a folder**<br><br>If the input parameter folderPath=0, then in the following JSON example, folderName is only "folderName": [ "Subfolder \- Level 3" ] |
|name |string |Dataset name |
|ownerEmailPrefix |string |Dataset owner |
|status |integer |Dataset status \-\> Normally, status=0 |
|type |integer |Dataset types [Common types: 0: Dataset generated from a ClickHouse table as the data source, 2: Dataset generated from a Hive table as the data source, 8: Dataset generated from custom SQL, 10: Dataset generated from a MySQL table as the data source, 22: Prep\-type dataset] |


```json
{
    "code": "aeolus/ok",
    "data": {
        "appId": 7777947,
        "appName": "测试项目-名称",
        "demoUrl": "http://xxx.com",
        "descr": "这是一段描述，描述数据集的作用",
        "detailUrl": "https://aeolus-release.fedev.bytedanc*.net/aeolus#/dataManage/detail/{{dataSetId}}?appId=77*****",
        "folderName": [
            "子文件夹-层级3",
            "子文件夹-层级2",
            "子文件夹-层级1",
            "模板数据集",
            "根目录"
        ],
        "id": {{dataSetId}},
        "name": "测试open-api专用数据集1",
        "ownerEmailPrefix": "userEmailPrefix",
        "status": 0,
        "type": 22
    },
    "msg": "成功"
}
```


<span id="_3-4-更新数据集基础信息"></span>
## 2.4 Update basic dataset information


* Permission requirements

   
   |Resource |Permission |
   |---|---|
   |Dataset |write |
   

* API description and notes: Update the basic description information of the dataset on the frontend.


Caution: The information that can be updated through this API differs from that of the `View basic dataset information` API.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/93a379311ebe4feca70f3235f70aecd0~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fc8c09f5947c48eb9a0c193df1e6b1d0~tplv-goo7wpa0wc-image.image) </span>

<span id="a40565a2"></span>
#### Request description


* Request URL: `{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/digest`

   **Caution: This is a full overwrite update. If you need to update a specific attribute, you must also provide the original content of all other attributes in full. Otherwise, blank values will overwrite the existing attributes.** 


<span id="e7335b4a"></span>
#### Request example

```bash
curl --location --request PUT '{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/digest' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}' \
--data-raw '{
    "dataSetName": "测试open-api专用数据集1",
    "dataSetDescr": "这是一段描述，描述数据集的作用"
}'
```


<span id="f840b2e8"></span>
#### Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|dataSetId |integer |Yes |123 |Dataset ID. See [How to Obtain Resource IDs](https://docs.byteplus.com/docs/DataWind/How_to_Obtain_Resource_IDs) for how to obtain it. |
|dataSetName |integer |Yes |Dataset 1 |Dataset name |
|dataSetDescr |string |Yes |This is a dataset description |Dataset description |


<span id="02dc5d68"></span>
#### Response example

```json
{
    "code": "aeolus/ok",
    "data": {
        "affectedRows": 1
    },
    "msg": "成功"
}
```


<span id="_3-5-设置数据集的标签"></span>
## 2.5 Set dataset tags


* Permission requirements

   
   |Resource |Permission |
   |---|---|
   |Dataset |write |
   

* Interface description and notes: Set the label information for the dataset. Dataset labels are attached to the project and must be used together with the "Dataset Label \- Get Dataset Label Information Under Project" API.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9a2b9a44b81a49fb94e2dc97231ff91a~tplv-goo7wpa0wc-image.image) </span>


<span id="dc689585"></span>
#### Request description


* Request URL: `{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/dataSetTag`


<span id="f27b69d1"></span>
#### Request example

```bash
curl --location --request POST '{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/dataSetTag' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}' \
--data-raw '{
    "tagIdList": [
        153
    ]
}'
```


<span id="856b2009"></span>
#### Request parameters


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|dataSetId |integer |Yes |123 |Dataset ID. See [How to Obtain Resource IDs](https://docs.byteplus.com/docs/DataWind/How_to_Obtain_Resource_IDs) for how to obtain it. |
|tagIdList |list < integer \> |Yes |153 |Tag ID. Multiple tags can be set for a dataset at once; the frontend allows multiple selections |


<span id="6b5f7acd"></span>
#### Response example

```json
{
    "code": "aeolus/ok",
    "data": {},
    "msg": "成功"
}
```


<span id="c4b0ca9b"></span>
## 2.6 Get the list of dataset folders under the project

Version: V2.76.0 and above


* Permission requirements



|Resource |Permission |
|---|---|
|Project |read |


<span id="af29418c"></span>
#### Request description

Get the folder list under the project


* API path

   `{{domain}}/aeolus/api/v4/open/app/{{appId}}/dataSetFolderTreeV2`

    &nbsp;


<span id="request-example"></span>
#### Request example


* cURL example


```JSON
curl --location --request GET '{{domain}}/aeolus/api/v4/open/app/{{appId}}/dataSetFolderTreeV2' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}'
```


<span id="a1e34926"></span>
#### Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|appId |integer |Yes |123 |Project ID. See [How to Obtain Resource IDs](https://docs.byteplus.com/docs/DataWind/How_to_Obtain_Resource_IDs) for how to obtain it. |


<span id="126ad5ee"></span>
#### Response parameters


|Name |Type |Description |
|---|---|---|
|official |list |Official directory |
|private |list |Personal directory |
|public |list |Public directory |
|appID |integer |Project ID |
|id |integer |Dataset ID |
|belong |integer |1 is a public dataset, 2 is a personal dataset |
|ctime |datetime |Dataset creation time |
|deleteTime |datetime |Dataset deletion time |
|mtime |datetime |Dataset last modified time |
|descr |string |Dataset description |
|name |string |Dataset name |
|ownerEmailPrefix |string |Dataset owner |
|status |integer |Dataset folder status: 0 is normal, 1 is permanently deleted, 2 is in the recycle bin |
|parentId |integer |Parent folder of the dataset folder. If 0, it means there is no parent folder and it is in the root directory |
|childList |list |List of subfolders in the dataset folder<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/149d47c4039b47c4ab4f58f98c9f58c0~tplv-goo7wpa0wc-image.image) </span> |


<span id="d12d2dc6"></span>
#### Response example

```JSON
{
    "code": "aeolus/ok",
    "data": {
        "official": [
            {
              "appId": 7*******,  #项目id
              "belong": 1,     #归属 1是公共，2是个人
              "ctime": "2024-05-30 11:57",
              "deleteTime": null,
              "descr": null,
              "id": 12107,
              "mtime": "2024-05-30 11:57",
              "name": "测试",
              "ownerEmailPrefix": "userEmailPrefix",
              "parentId": 12101,  #父目录id
              "status": 0,   
              "childList": [],   #子目录list
            }
        ],
        "private": [],
        "public": [],
    }
    "msg": "成功"
}
```
