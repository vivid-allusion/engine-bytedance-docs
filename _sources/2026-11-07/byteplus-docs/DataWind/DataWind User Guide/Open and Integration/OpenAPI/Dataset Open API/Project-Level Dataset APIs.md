---
title: "Project-Level Dataset APIs"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Project-Level_Dataset_APIs"
---

<span id="_1-概述"></span>
# 1. Overview

This document introduces the "Open APIs for project\-level datasets," mainly including the project dataset tag and folder APIs, project dataset APIs, and project cluster configuration APIs. You will learn that users can use these APIs to retrieve, create, and update dataset and folder information within a project, as well as retrieve, add, and remove users from the private cluster write user list.

Caution: Before using the APIs described in this document, you must complete the prerequisites for integrating JWT\-Token and applying for a Token. Please first review the invocation method. For details, see [Invocation Methods](https://docs.byteplus.com/docs/DataWind/Invocation_Methods).

<span id="_3-数据集标签"></span>
# 2. Dataset tags

<span id="_3-1-获取项目下数据集标签信息"></span>
## 2.1 Retrieve dataset tag information within a project


* Permission requirements

   
   |Resource |Permission |
   |---|---|
   |Project |read |
   

* API description: Retrieve information about dataset tags that have been created within a project.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/97d52ffa3f6c4330bafdd446d3c870d6~tplv-goo7wpa0wc-image.image) </span>


<span id="3414620a"></span>
#### Request description


* Request URL: `{{domain}}/aeolus/api/v4/open/app/{{appId}}/dataSetTag`


<span id="9984caa4"></span>
#### Request example

```bash
curl --location --request GET '{{domain}}/aeolus/api/v4/open/app/{{appId}}/dataSetTag' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}'
```


<span id="20f2fafe"></span>
#### Request parameters


|Parameter |Type |Required |Description |Example value |
|---|---|---|---|---|
|appId |integer |Yes |Project ID |123 |


<span id="c38eea91"></span>
#### Response parameters


|Parameter |Type |Description |
|---|---|---|
|appId |integer |Project ID |
|colour |string |Dataset label color<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6501cd22ef714d3da6675f2709ea6350~tplv-goo7wpa0wc-image.image) </span> |
|ctime |string |Dataset label creation time |
|dataSetInfos |object |Dataset label application status in datasets |
|dataSetInfos.id |integer |Dataset ID |
|dataSetInfos.name |string |Dataset name |
|id |integer |Dataset label ID |
|mtime |string |Dataset label modification time |
|name |string |Dataset label name |
|reportEnable |integer |Whether the chart title inherits this label |
|status |integer |Dataset label status |


<span id="response-example"></span>
#### Response example  

```json
{
    "code": "aeolus/ok",
    "data": [
        {
            "appId": 7******,
            "colour": "purple",
            "ctime": "2022-12-13 16:48",
            "dataSetInfos": [
                {
                    "id": 19****,
                    "name": "v4专用测试数据集"
                },
                {
                    "id": {{dataSetId}},
                    "name": "测试open-api专用数据集1"
                }
            ],
            "id": 153,
            "mtime": "2022-12-13 16:48",
            "name": "test用",
            "reportEnable": 0,
            "status": 0
        }
    ],
    "msg": "成功"
}
```


<span id="_3-2-创建项目下数据集标签"></span>
## 2.2 Create a dataset tag within a project


* Permission requirements

   
   |Resource |Permission |
   |---|---|
   |Project |admin |
   

* API description: Create a dataset tag within a project.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f80f80f0545943558b22ed080f0c4db6~tplv-goo7wpa0wc-image.image) </span>


<span id="9144d2c1"></span>
#### Request description


* Request URL: `{{domain}}/aeolus/api/v4/open/app/{{appId}}/dataSetTag`


<span id="b99f8f12"></span>
#### Request example

```bash
curl --location --request POST '{{domain}}/aeolus/api/v4/open/app/{{appId}}/dataSetTag' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}' \
--data-raw '{
    "name": "test用",
    "colour": "purple",
    "reportEnable": 0
}'
```


<span id="77f6a72d"></span>
#### Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|appId |integer |Yes |123 |Project ID |
|name |string |Yes |For testing |Dataset label name |
|colour |string |Yes |blue<br><br>green<br><br>lightGreen<br><br>lightYellow<br><br>orange<br><br>purple<br><br>red<br><br>yellow |Dataset label color |
|reportEnable |integer |No | |Whether the chart inherits this dataset label |


<span id="115f374e"></span>
#### Response parameters


* Response description: `$.data.id` is the ID of the newly created dataset tag.

   ```json
   {
       "code": "aeolus/ok",
       "data": {
           "id": 154
       },
       "msg": "成功"
   }
   ```
   


<span id="_3-3-更新项目下数据集标签信息"></span>
## 2.3 Update dataset tag information within a project


* Permission requirements

   
   |Resource |Permission |
   |---|---|
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae9139e7ce714df4949bc94c88f36f12~tplv-goo7wpa0wc-image.image) </span>


<span id="fbb330ec"></span>
#### Request description


* Request URL: `{{domain}}/aeolus/api/v4/open/app/{{appId}}/dataSetTag/{{tagId}}`


<span id="a9afd77a"></span>
#### Request example

```bash
curl --location --request PUT '{{domain}}/aeolus/api/v4/open/app/{{appId}}/dataSetTag/{{tagId}}' \
--header 'Content-Type: application/json' \
--header 'app-id: 77*****' \
--header 'Authorization: Bearer {{jwtToken}}' \
--data-raw '{
    "colour": "purple",
    "name": "12",
    "reportEnable": 0
}'
```


<span id="c1eab921"></span>
#### Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|appId |integer |Yes |123 |Project ID |
|tagId |integer |Yes |123 |Dataset label ID |
|name |string |Yes |For testing |Dataset label name |
|colour |string |Yes |blue<br><br>green<br><br>lightGreen<br><br>lightYellow<br><br>orange<br><br>purple<br><br>red<br><br>yellow |Dataset label color |
|reportEnable |integer |No |0 |Whether the chart inherits this dataset label |


<span id="da690a52"></span>
#### Response example

```json
{
    "code": "aeolus/ok",
    "data": null,
    "msg": "成功"
}
```


<span id="_3-4-删除项目下数据集标签"></span>
## 2.4 Delete a dataset tag within a project


* Permission requirements

   
   |Resource |Permission |
   |---|---|
   |Project |admin |
   

* API description: Delete dataset tag information within a project.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aad2e815a378447aa58ed36092aeb43e~tplv-goo7wpa0wc-image.image) </span>


<span id="a39b9e27"></span>
#### Request description


* Request URL: `{{domain}}/aeolus/api/v4/open/app/{{appId}}/dataSetTag/{{tagId}}`


<span id="d27d95f5"></span>
#### Request example

```bash
curl --location --request DELETE '{{domain}}/aeolus/api/v4/open/app/{{appId}}/dataSetTag/{{tagId}}' \
--header 'Content-Type: application/json' \
--header 'app-id: 7777947' \
--header 'Authorization: Bearer {{jwtToken}}'
```


<span id="b804c8c1"></span>
#### Request parameters


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|appId |integer |Yes |123 |Project ID |
|tagId |integer |Yes |123 |Dataset tag ID |


<span id="response-parameters"></span>
#### Response parameters  

```json
{
    "code": "aeolus/ok",
    "data": null,
    "msg": "成功"
}
```


<span id="_4-数据集文件夹"></span>
# 3. Dataset folders

<span id="_4-1-获取项目下数据集文件夹信息"></span>
## 3.1 Retrieve dataset folder information within a project


* Permission requirements

   
   |Resource |Permission |
   |---|---|
   |Project |read |
   

* API description: Delete dataset tag information within a project.


<span id="f60484ab"></span>
#### Request description


* Request URL: `{{domain}}/aeolus/api/v4/open/app/{{appId}}/dataSetFolder`


<span id="2df4d154"></span>
#### Request example

```json
curl --location --request GET '{{domain}}/aeolus/api/v4/open/app/{{appId}}/dataSetFolder' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}'
```


<span id="cbe7ab0f"></span>
#### Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|appId |integer |Yes |123 |Project ID |


<span id="fd063a62"></span>
#### Response parameters


|Parameter |Type |Description |
|---|---|---|
|appId |integer |Project ID |
|ctime |string |Dataset folder creation time |
|deleteTime |string |Dataset folder deletion time |
|descr |string |Dataset folder description |
|id |integer |Dataset folder ID |
|mtime |string |Dataset folder modification time |
|name |string |Dataset folder name |
|ownerEmailPrefix |string |Dataset folder owner |
|parentId |integer |Parent folder of the dataset folder; if 0, it means there is no parent folder and the folder is in the root directory. |
|status |integer |Dataset folder status |
|childList |list |Dataset folder subfolder list<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa09bf82c6d3459d8cb1a08ed3979d02~tplv-goo7wpa0wc-image.image) </span> |


<span id="response-example"></span>
#### Response example  

```json
{
    "code": "aeolus/ok",
    "data": [
        {
            "appId": *******,
            "ctime": "2022-04-02 11:52",
            "deleteTime": null,
            "descr": "",
            "id": 2320,
            "mtime": "2022-04-02 11:52",
            "name": "test1",
            "ownerEmailPrefix": "userEmailPrefix",
            "parentId": 0,
            "status": 0
        },
        {
            "appId": *******,
            "childList": [
                {
                    "appId": *******,
                    "childList": [
                        {
                            "appId": *******,
                            "childList": [
                                {
                                    "appId":*******,
                                    "ctime": "2022-12-14 12:14",
                                    "deleteTime": null,
                                    "descr": "",
                                    "id": 3075,
                                    "mtime": "2022-12-14 12:14",
                                    "name": "子文件夹-层级3",
                                    "ownerEmailPrefix": "userEmailPrefix",
                                    "parentId": 2706,
                                    "status": 0
                                }
                            ],
                            "ctime": "2022-09-29 16:30",
                            "deleteTime": null,
                            "descr": "",
                            "id": 2706,
                            "mtime": "2022-12-14 12:13",
                            "name": "子文件夹-层级2",
                            "ownerEmailPrefix": "userEmailPrefix",
                            "parentId": 2704,
                            "status": 0
                        }
                    ],
                    "ctime": "2022-09-29 16:29",
                    "deleteTime": null,
                    "descr": "111",
                    "id": 2704,
                    "mtime": "2022-12-14 12:13",
                    "name": "子文件夹-层级1",
                    "ownerEmailPrefix": "userEmailPrefix",
                    "parentId": 2321,
                    "status": 0
                }
            ],
            "ctime": "2022-04-02 11:53",
            "deleteTime": null,
            "descr": "",
            "id": 2321,
            "mtime": "2022-05-04 11:24",
            "name": "模板数据集",
            "ownerEmailPrefix": "userEmailPrefix",
            "parentId": 0,
            "status": 0
        },
        {
            "appId": *******,
            "ctime": "2022-12-14 12:14",
            "deleteTime": null,
            "descr": "",
            "id": 3076,
            "mtime": "2022-12-14 12:14",
            "name": "测试文件夹1",
            "ownerEmailPrefix": "userEmailPrefix",
            "parentId": 0,
            "status": 0
        }
    ],
    "msg": "成功"
}
```


<span id="_4-2-创建项目下数据集文件夹"></span>
## 3.2 Create a dataset folder within a project


* Permission requirements

   
   |Resource |Permission |
   |---|---|
   |Parent folder |write |
   |Project (when parentId=0) |write |
   

   To create a folder in the root directory, **project write permission is required.** 

* API description: Create a folder in the root directory or within another folder.


<span id="20144381"></span>
#### Request description


* Request URL: `{{domain}}/aeolus/api/v4/open/app/{{appId}}/dataSetFolder`


<span id="7495f607"></span>
#### Request example

```bash
curl --location --request POST '{{domain}}/aeolus/api/v4/open/app/{{appId}}/dataSetFolder' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}' \
--data-raw '{
    "name": "子文件夹1111",
    "descr": "666",
    "confidentiality": "L3",
    "isPersonalDataRelated": true,
    "dataRegion": [
        "CN"，
        "US"
    ],
    "parentId": 0
}'
```


<span id="fdf45c3c"></span>
#### Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|appId |integer |Yes |123 |Project ID |
|name |string |Yes |Subfolder 1 |Folder name |
|descr |string |No |666 |Folder description; if not provided, this field will be empty. |
|parentId |integer |Yes |0 |Parent folder ID. If parentId is 0, the folder is created in the root directory. |
|confidentiality |string |No |L3 |Dataset folder confidentiality level (non\-TOB environment) |


<span id="2fba2af8"></span>
#### Response example


* Response description: `folderId` is the ID of the new folder.

   ```json
   {
       "code": "aeolus/ok",
       "data": {
           "folderId": 3079
       },
       "msg": "成功"
   }
   ```
   


<span id="2d305e22"></span>
## 3.3 Update dataset folder information in the project


* Permission requirements

   
   |Resource |Permission |
   |---|---|
   |Dataset folder |write |
   

* Interface description and notes


<span id="d8ea8828"></span>
#### Request description


* Request URL: `{{domain}}/aeolus/api/v4/open/app/{{appId}}/dataSetFolder/{{dataSetFolderId}}`


<span id="d122869d"></span>
#### Request example

```bash
curl --location --request PUT '{{domain}}/aeolus/api/v4/open/app/{{appId}}/dataSetFolder/{{dataSetFolderId}}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}' \
--data-raw '{
    "name": "测试文件夹1",
    "descr": "111",
    "isPersonalDataRelated": true,
    "dataRegion": [
        "CN"，
        "US"
    ],
    "confidentiality": "L2"
}'
```


<span id="3bd884a8"></span>
#### Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|appId |integer |Yes |123 |Project ID |
|dataSetFolderId |integer |Yes |3079 |Dataset folder ID |
|name |string |Yes |Test folder 1 |Dataset folder name |
|descr |string |No |111 |Dataset folder description |


<span id="c86829c9"></span>
#### Response example


* Response description: The returned `folderId` indicates that the folder information was updated successfully.

   ```json
   {
       "code": "aeolus/ok",
       "data": {
           "folderId": 3079
       },
       "msg": "成功"
   }
   ```
   


<span id="_5-数据集"></span>
# 4. Datasets

<span id="_5-1-获取项目下数据集信息列表"></span>
## 4.1 Retrieve the list of dataset information in the project


* Permission requirements

   
   |Resource |Permission |
   |---|---|
   |Dataset folder |read |
   

* Interface description and notes: Retrieve the list of information for all current datasets in the project.


<span id="ddec44bc"></span>
#### Request description


* Request URL: `{{domain}}/aeolus/api/v4/open/app/{{appId}}/dataSetList`


<span id="1d35a173"></span>
#### Request example

```bash
curl --location --request GET '{{domain}}/aeolus/api/v4/open/app/{{appId}}/dataSetList?needSyncInfo=0&needUpstreamInfo=0&dataSetIdList=186583,186600' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}'
```


<span id="3e8f8d3d"></span>
#### Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|appId |integer |Yes |123 |Project ID |
|needSyncInfo |integer |No |0,1 |Whether to include dataset synchronization information in the dataset information<br><br>Setting to 0 can speed up the interface |
|needUpstreamInfo |integer |No |0,1 |Whether to include upstream data source information in the dataset information<br><br>Setting to 0 can speed up the interface |
|dataSetIdList |list |No |186583,186600 |Dataset ID list; if not provided, all projects are queried by default. Otherwise, only the dataset information specified by this parameter is returned. Multiple dataset IDs should be separated by commas. |


<span id="e1fa1ba8"></span>
#### Response parameters


|Parameter |Type |Description |
|---|---|---|
|ctime |integer |Dataset creation date |
|elapsedTimeForLastSuccessTaskTime |integer |Duration of the most recent successful synchronization task |
|frequency |string |Dataset synchronization task frequency |
|id |integer |Dataset ID |
|lastSuccessTaskTime |string |Business date of the most recent successful synchronization |
|lastSyncTime |string |Most recent synchronization time |
|mtime |string |Most recent dataset modification time |
|name |string |Dataset name |
|owner |string |Dataset owner |
|rowsForLastSuccessTaskTime |integer |Number of data rows in the most recent successful synchronization task |
|scheduleDay |string |Automatic daily scheduling for dataset synchronization<br><br>When the frequency is set to the hourly or minute level<br><br>scheduleDay is at the hour level, that is, synchronization starts at a specific hour |
|scheduleTime |string |Automatic hourly scheduling for dataset synchronization<br><br>When the frequency is set to the hourly or minute level<br><br>scheduleTime is at the minute level, that is, synchronization starts at a specific minute |
|status |integer |Dataset status |
|syncType |integer |Dataset synchronization type |
|ttl |integer |Dataset lifecycle |
|type.name |string |Dataset type name |
|upstreamInfo.dbName |string |DBName of the upstream data source used by the dataset |
|upstreamInfo.tableName |string |tableName of the upstream data source used by the dataset |
|url |string |URL of the dataset details page |


```json
{
    "code": "aeolus/ok",
    "data": [
        {
            "ctime": "2022-12-14 12:17:54",
            "elapsedTimeForLastSuccessTaskTime": 501,
            "frequency": "daily",
            "hivePartitionSpecified": false,
            "hiveTableUsed": false,
            "hsqlList": [],
            "hsqlUsed": false,
            "id": {{dataSetId}},
            "lastSuccessTaskTime": "2022-12-14 00:00:00",
            "lastSyncTime": "2022-12-15 18:19:19",
            "mtime": "2022-12-15 19:37:31",
            "name": "测试open-api专用数据集1",
            "owner": "userEmailPrefix",
            "rowsForLastSuccessTaskTime": 56,
            "scheduleDay": "0",
            "scheduleTime": "00:00",
            "status": 0,
            "syncType": 2,
            "ttl": 8,
            "type": {
                "code": 22,
                "name": "prep 数据集"
            },
            "upstreamInfo": [
                {
                    "dbName": "aeolus_excel_upload_aeolus_toy",
                    "tableName": "table_4f0cc551_9dfa_4915_a38f_737c716591a8"
                }
            ],
            "url": "https://aeolus-release.fedev.bytedanc*.net/aeolus#/dataManage/detail/{{dataSetId}}?appId=7777947"
        }
    ],
    "msg": "成功"
}
```


<span id="_5-2-获取项目下数据集简略信息列表"></span>
## 4.2 Retrieve the list of summary information for datasets in the project


* Minimum supported version **2.58.1.** 

* Permission requirements

   
   |Resource |Permission |
   |---|---|
   |Dataset |read |
   

* Interface description and notes: Retrieve the list of information for all current datasets in the project.


<span id="1f882095"></span>
#### Request description


* Request URL: `{{domain}}/aeolus/api/v4/open/app/{{appId}}/dataSetSimpleList`


<span id="8a5e711c"></span>
#### Request example

```bash
curl --location --request GET '{{domain}}/aeolus/api/v4/open/app/{{appId}}/dataSetSimpleList?page=1&perPage=2&kw=测试' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}'
```


<span id="ee0460b3"></span>
#### Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|appId |integer |Yes |123 |Project ID |
|kw |string |No |Test |Dataset name, fuzzy match |
|page |integer |No |1 |Pagination \- page number<br><br>Must be used together with perPage |
|perPage |integer |No |2 |Pagination \- items per page<br><br>Must be used together with page |


<span id="f6b64144"></span>
#### Response parameters


|Parameter |Type |Description |
|---|---|---|
|appId |integer |Project name |
|belong |integer |Public dataset or personal dataset |
|ctime |string |Dataset creation time |
|mtime |string |Last modification time of the dataset |
|name |string |Dataset name |
|ownerEmailPrefix |string |Dataset owner |
|status |integer |Dataset status |
|type |integer |Dataset type |
|totalSize |integer |Total number of datasets visible with permission (used with pagination) |


<span id="response-example"></span>
#### Response example  

```json
{
    "code": "aeolus/ok",
    "data": {
        "dataSetList": [
            {
                "appId": 1,
                "belong": 1,
                "ctime": "2023-10-16 19:51",
                "id": 1,
                "mtime": "2023-10-16 19:51",
                "name": "data_set_name",
                "ownerEmailPrefix": "user",
                "status": 0,
                "type": 22
            }
        ],
        "totalSize": 1
    },
    "msg": "成功"
}
```


<span id="_5-3-获取项目下上游为某数据源的数据集信息"></span>
## 4.3 Retrieve dataset information in the project where the upstream is a specified data source


* First supported version 2.51.

* Permission requirements

   
   |Resource |Permission |
   |---|---|
   |Project |read |
   

* Interface description and notes: By specifying `dataSourceType` (data source type), `dbName` (database name of the data source, not applicable for some data sources), and `tableName` (table name of the data source), you can query the basic information of all datasets that use this data source as upstream.

   Note: The current query scope does not include datasets of custom SQL type.


<span id="77d97d95"></span>
#### Request description


* Request URL: `{{domain}}/aeolus/api/v4/open/app/{{appId}}/dataSourceLineage`


<span id="b1223aef"></span>
#### Request example

```bash
curl --location --request POST '{{domain}}/aeolus/api/v4/open/app/{{appId}}/dataSourceLineage' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}'
--data '{
    "dataSourceType": "click_house",
    "dbName": "aeolus_excel_upload_aeolus_toy",
    "tableName": "table_35b15b69_2ea5_****_****_*********",
    "authOnly": false
}'
```



* Request parameters

   
   |Parameter |Type |Required |Example value |Description |
   |---|---|---|---|---|
   |appId |integer |Yes |123 |Project ID |
   |dataSourceType |string |Yes |hive<br><br>click_house |Data source type |
   |dbName |string |No |aeolus_excel_upload_aeolus_toy |Data source \- database name |
   |tableName |string |No |table_35b15b69_2ea5_ **_** _\*\*\*\*\*\*\*\*\* |Data source \- table name |
   |authOnly |boolean |No |false |Whether to return only the dataset information for the user associated with the current token (with read\-only or higher permission). Default value: false. |
   


<span id="106c62bd"></span>
#### Response parameters


* Response description: See the detailed description for the response fields under `dataSetList`.

   [Interface \- View basic dataset information]

   
   |Parameter |Type |Description |
   |---|---|---|
   |dataSetList |list |Result content |
   |dataSourceType |string |dataSourceType used for the query |
   |dbName |string |dbName used for the query |
   |tableName |string |tableName used for the query |
   |listSize |integer |Number of datasets found |
   

   #### Response example      <span id="response-example"></span>

   ```json
   {
       "code": "aeolus/ok",
       "data": {
           "dataSetList": [
               {
                   "appId": "*******",
                   "appName": "hsm",
                   "demoUrl": "",
                   "descr": null,
                   "detailUrl": "https://aeolus-integration.bytedanc*.net/aeolus#/dataManage/detail/193016?appId=7778352",
                   "folderName": [
                       "根目录"
                   ],
                   "id": ******,
                   "name": "good_hive_data_set",
                   "ownerEmailPrefix": "husimin.xcl",
                   "status": 0,
                   "type": 2
               },
               {
                   "appId": "*******",
                   "appName": "hsm",
                   "demoUrl": "",
                   "descr": null,
                   "detailUrl": "https://aeolus-integration.bytedanc*.net/aeolus#/dataManage/detail/196003?appId=7778352",
                   "folderName": [
                       "原始内容保留",
                       "根目录"
                   ],
                   "id": 196003,
                   "name": "测试tableSchema权限",
                   "ownerEmailPrefix": "husimin.xcl",
                   "status": 0,
                   "type": 2
               }
           ],
           "dataSourceType": "hive",
           "dbName": null,
           "listSize": 2,
           "tableName": "hsm_own_metrics"
       },
       "msg": "成功"
   }
   ```
   


<span id="_6-集群配置"></span>
# 5. Cluster configuration

<span id="_6-1-获取私有集群写入用户列表"></span>
## 5.1 Retrieve the list of users with write access for a private cluster


* Permission requirements: The user must be the owner or person in charge of the private cluster, and also a project administrator.

* Interface description and notes: Retrieve the list of admitted users for a cluster in the project.


<span id="9685f3c4"></span>
#### Request description


* Request URL: `{{domain}}/aeolus/api/v4/open/app/{{appId}}/clusterWriteUserList`


<span id="9b3c76ee"></span>
#### Request example

```bash
curl --location --request GET '{{domain}}/aeolus/api/v4/open/app/{{appId}}/clusterWriteUserList?clusterId=1' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}'
```


<span id="add084cb"></span>
#### Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|appId |integer |Yes |123 |Project ID |
|clusterId |integer |Yes |1 |Cluster ID |


<span id="6feb6779"></span>
#### Response parameters


|Parameter |Type |Description |
|---|---|---|
|userList |array |Allowlist user list |


<span id="response-example"></span>
#### Response example  

```json
{
    "code": "aeolus/ok",
    "data": [
        "luowenlei",
        "chenweichen.six"
    ],
    "msg": "成功"
}
```


<span id="_6-2-新增私有集群写入用户列表"></span>
## 5.2 Add users with write access to a private cluster


* Permission requirements: The user must be the owner or person in charge of the private cluster, and also a project administrator.

* Interface description and notes: Add certain users to the admission user list of a specific cluster under the project.

* Note: If the cluster's permissions are already available to the entire project, this operation will not change the current state of project\-wide availability. The permissions for the added users will be redundant and will only take effect after the project\-wide permissions are removed. If an error occurs during batch write, you can retry the write operation. The interface is idempotent for successful results.


<span id="afeb1fba"></span>
#### Request description

Request URL: `{{domain}}/aeolus/api/v4/open/app/{{appId}}/clusterWriteUserList`

<span id="dca1a901"></span>
#### Request example

```bash
curl --location --request POST '{{domain}}/aeolus/api/v4/open/app/{{appId}}/clusterWriteUserList' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}'\
--data-raw '{
    "userList": ["******.****"],
    "clusterId": 1
}'
```


<span id="66cc5bf6"></span>
#### Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|appId |integer |Yes |123 |Project ID |
|userList |list |Yes |["\*\* **.** "] |Added usernames (idempotent, existing usernames will not be added again) |
|clusterId |integer |Yes |1 |Cluster ID |


<span id="4f0bc65c"></span>
#### Response example


* `$.data.id` is the cluster ID.


```json
{
    "code": "aeolus/ok",
    "data": {
        "id": 1
    },
    "msg": "成功"
}
```


<span id="_6-3-删除私有集群写入用户列表"></span>
## 5.3 Delete private cluster write user list


* Permission requirements: The user must be the owner or person in charge of the private cluster, and also a project administrator.

* Interface description and notes: Remove certain users from the admission user list of a specific cluster under the project.

* Note: If an error occurs during batch deletion, you can retry the write operation. The interface does not guarantee idempotency for successful results.


<span id="6301100b"></span>
#### Request description


* Request URL: `{{domain}}/aeolus/api/v4/open/app/{{appId}}/clusterWriteUserList`


<span id="e76a8239"></span>
#### Request example

```bash
curl --location --request DELETE '{{domain}}/aeolus/api/v4/open/app/{{appId}}/clusterWriteUserList' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}'\
--data-raw '{
    "userList": ["*******.****"],
    "clusterId": 1
}'
```


<span id="131c1dc4"></span>
#### Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|appId |integer |Yes |123 |Project ID |
|userList |list |Yes |["\*\* **.** "] |Deleted usernames (idempotent, if the user does not have permission, the API will not return an error) |
|clusterId |integer |Yes |1 |Cluster ID |


<span id="2a80d185"></span>
#### Response example


* `$.data.id` is the cluster ID.


```json
{
    "code": "aeolus/ok",
    "data": {
        "id": 1
    },
    "msg": "成功"
}
```
