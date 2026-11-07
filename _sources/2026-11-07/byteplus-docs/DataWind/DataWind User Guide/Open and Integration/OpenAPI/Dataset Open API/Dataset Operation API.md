---
title: "Dataset Operation API"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Dataset_Operation_API"
---

<span id="_1-概述"></span>
# 1. Overview

This document introduces the "Open API for dataset operations". You will learn how users can update, move, and delete datasets, as well as check and move datasets to the recycle bin through the API.

Caution: Before using the APIs described in this document, you must complete the prerequisite steps of integrating JWT\-Token and applying for a Token. Please familiarize yourself with the invocation method. For details, see [Invocation Methods](https://docs.byteplus.com/docs/DataWind/Invocation_Methods).

<span id="_3-接口介绍"></span>
# 2. API introduction

<span id="_3-3-检查数据集是否可被移入回收站"></span>
## 2.1 Check whether a dataset can be moved to the recycle bin


* Permission requirements

   
   |Resource |Permission |
   |---|---|
   |Dataset |admin |
   

* API description: Checks whether the current dataset has lineage associations or other issues. If there are no issues, an empty list is returned, indicating that the dataset can be deleted directly. Otherwise, the user must manually remove lineage associations as indicated in the API response before moving the dataset to the recycle bin.


Note: This API should be used in conjunction with the `Move dataset to recycle bin` API.

<span id="332090dc"></span>
#### Request description

Request URL: `{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/recyclable`

<span id="7f92ba89"></span>
#### Request example

```json
curl --location --request GET '{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/recyclable' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}'
```


<span id="75c41498"></span>
#### Request parameters


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|dataSetId |integer |Yes |123 |Dataset ID |


<span id="19f936a7"></span>
#### Response example


* Response description: Under normal circumstances, the dataset can be deleted directly

   ```json
   {
       "code": "aeolus/ok",
       "data": [],
       "msg": "成功"
   }
   ```
   


<span id="_3-4-移入数据集到回收站"></span>
## 2.2 Move dataset to recycle bin


* Permission requirements

   
   |Resource |Permission |
   |---|---|
   |Dataset |admin |
   

* API description: Moves the dataset to the recycle bin. This is not a permanent deletion.


Note: This API should be used in conjunction with the `Check whether a dataset can be moved to the recycle bin` API.

<span id="00028416"></span>
#### Request description

Request URL: `{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/recycle`

<span id="8514f6b8"></span>
#### Request example

```bash
curl --location --request DELETE '{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/recycle' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}'
```


<span id="e6036738"></span>
#### Request parameters


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|dataSetId |integer |Yes |123 |Dataset ID |


<span id="27a56213"></span>
#### Response example

```json
{
    "code": "aeolus/ok",
    "data": [],
    "msg": "成功"
}
```


<span id="_3-5-从回收站恢复数据集"></span>
## 2.3 Restore dataset from recycle bin


* Permission requirements

   
   |Resource |Permission |
   |---|---|
   |Dataset |admin |
   

* API description: Restores the dataset from the recycle bin

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/53ab1305b1484b6587a523e4858147ef~tplv-goo7wpa0wc-image.image) </span>


<span id="4b79f3b5"></span>
#### Request description

API path: `{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/restore`

<span id="3f30559f"></span>
#### Request example

```bash
curl --location --request PUT '{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/restore' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}'
```


<span id="669a61db"></span>
#### Request parameters


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|dataSetId |integer |Yes |123 |Dataset ID |


<span id="7346fb99"></span>
#### Response example

If `fails` is an empty list, the dataset has been restored successfully

```json
{
    "code": "aeolus/ok",
    "data": {
        "fails": []
    },
    "msg": "成功"
}
```


<span id="_3-6-彻底删除数据集"></span>
## 2.4 Permanently delete dataset


* Permission requirements

   
   |Resource |Permission |
   |---|---|
   |Dataset |admin |
   

* API description: Permanently deletes the dataset, clears the dataset's data and underlying tables, stops synchronization tasks, and so on; only the dataset's metadata is retained

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cebd11199b154b378f812605f626bb49~tplv-goo7wpa0wc-image.image) </span>


<span id="2551330b"></span>
#### Request description

API path: `{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}`

<span id="4694f57e"></span>
#### Request example

```bash
curl --location --request DELETE '{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}'
```


<span id="c6080c57"></span>
#### Request parameters


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|dataSetId |integer |Yes |123 |Dataset ID |


<span id="c359afd7"></span>
#### Response example

If the deletion is successful, the dataset ID is returned

```json
{
    "code": "aeolus/ok",
    "data": [
        "180664"
    ],
    "msg": "成功"
}
```


<span id="_3-7-移动数据集位置-更新文件夹路径"></span>
## 2.5 Move dataset location (update folder path)


* Permission requirements

   
   |Resource |Permission |
   |---|---|
   |Dataset |write |
   |Target folder |write |
   

* Interface description and notes: Moves the specified dataset to a designated folder. This API can be used together with the "Dataset Folder \- Get dataset folder information under a project" API.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/59dd0893f06349688e910b8a905f5c8a~tplv-goo7wpa0wc-image.image) </span>


<span id="0ac165c1"></span>
#### Request description

API path: `{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/folder/move`

<span id="35bf6625"></span>
#### Request example

```bash
curl --location --request PUT '{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/folder' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}' \
--data-raw '{
    "folderId": 2706
}'
```


<span id="0235373a"></span>
#### Request parameters


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|dataSetId |integer |Yes |123 |Dataset ID |
|folderId |integer |Yes |123 |Target folder ID |


<span id="223a707b"></span>
#### Response example

```json
{
    "code": "aeolus/ok",
    "data": "ok",
    "msg": "成功"
}
```
