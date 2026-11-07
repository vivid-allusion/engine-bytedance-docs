---
title: "Dataset Synchronization Task API"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Dataset_Synchronization_Task_API"
---

<span id="_1-概述"></span>
# 1. Overview

This document introduces the "Open API for dataset synchronization tasks." You will learn how users can use the API to view and update dataset synchronization task settings, submit backtracking tasks for dataset synchronization, and terminate dataset synchronization task instances.

Caution: Before using the APIs described in this document, you must complete the prerequisite steps of integrating JWT\-Token and applying for a Token. Please review the invocation method first. For details, see [Invocation Methods](https://docs.byteplus.com/docs/DataWind/Invocation_Methods).

<span id="_2-接口说明"></span>
# 2. API introduction

<span id="_3-1-查看数据集同步任务设置"></span>
## 2.1 View dataset synchronization task settings


* Permission requirements

   
   |Resource |Permission |
   |---|---|
   |Dataset |read |
   

* API description: View the synchronization task settings of a dataset, including synchronization mode, performance parameters, and more.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b787cdfa422f89081539ce5e73853566.png) </span>


<span id="96b95583"></span>
#### Request description


* Request URL: `{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/syncSettings`


<span id="f3fdf9a6"></span>
#### Request example

```bash
curl --location --request GET '{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/syncSettings' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}'
```


<span id="949b2c62"></span>
#### Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|dataSetId |integer |Yes |123 |Dataset ID |


<span id="66d64b6d"></span>
#### Response parameters


|Parameter |Type |Description |
|---|---|---|
|$.backtrackingConf |object |Dataset backtracking configuration |
|$.backtrackingConf.dateRange |object |Default backtracking period after the dataset is first created |
|$.backtrackingConf.dateRange.endDate |string |Backtracking end time |
|$.backtrackingConf.dateRange.startDate |string |Backtracking start time |
|$.doradoPriority |string |Synchronization job priority |
|$.monitorConf |object |Dataset synchronization monitoring and alert configuration |
|$.paramsConfList |object |Advanced parameters for dataset synchronization<br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b44a495f718516eb63a9582c2b0cb178.png) </span> |
|$.performanceSettings |object |Synchronization performance settings<br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_652ca37eab75a87d2d711222059cc2db.png) </span> |
|$.retryInterval |integer |Retry interval for a single dataset synchronization job failure |
|$.scheduleDay |string |Synchronization schedule \- day |
|$.scheduleTime |string |Synchronization schedule \- hour |
|$.retryNum |integer |Number of retries for a single dataset synchronization job failure |
|$.syncType |integer |Dataset job synchronization type [manual, automatic] |
|$.writePartition |integer |Dataset synchronization data write partition |
|$.ttl |integer |Dataset data retention lifecycle (days) |


<span id="response-example"></span>
#### Response example  

```json
{
    "code": "aeolus/ok",
    "data": {
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
                    "id": 6***,
                    "name": "auto_aeolus_rule_{{dataSetId}}_16***********_dev",
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
    "msg": "成功"
}
```


<span id="_3-2-更新数据集同步任务设置"></span>
## 2.2 Update dataset synchronization task settings


* Permission requirements

   
   |Resource |Permission |
   |---|---|
   |Dataset |write |
   

* API description: The content updated by this API is equivalent to modifying the synchronization configuration section (synchronization frequency) on the dataset details page.

   **This API performs a full update. All configuration information must be provided in the request.** 

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9a55c1a73098eedd2e693c1813fbb7aa.png) </span>


<span id="c2d2c154"></span>
#### Request description


* Request URL: `{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/syncSettings`


<span id="a93326eb"></span>
#### Request example

```bash
curl --location --request PUT '{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/syncSettings' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}' \
--data-raw '{
    "dataTableConf": {
        "ttl": 8
    },
    "syncConf": {
        "syncType": 1,
        "scheduleConf": {
            "frequency": "daily",
            "scheduleDay": "0",
            "scheduleTime": "00:00"
        }
    }
}'
```


<span id="dbc4ef5c"></span>
#### Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|dataSetId |integer |Yes |123 |Dataset ID |
|$.dataTableConf.ttl |integer |Yes |7 |Dataset lifecycle |
|$.syncConf.syncType |integer |Yes |1; 2 |Dataset synchronization scheduling mode [1 for automatic, 2 for manual] |
|$.syncConf.scheduleConf |object |Yes |*  |Synchronization scheduling configuration |
|$.syncConf.scheduleConf.frequency |string |Yes |hourly<br><br>daily<br><br>weekly<br><br>monthly<br><br>every_ten_minutes |When automatic scheduling synchronization is enabled, it can be set to daily, hourly, every ten minutes, monthly, or weekly synchronization. |
|$.syncConf.scheduleConf.scheduleDay |string |Yes |0 |Number of days set for automatic synchronization. Indicates on which day synchronization starts. For daily, 0 means synchronization occurs every day.<br><br>When frequency is set to hourly or every ten minutes<br><br>scheduleDay is at the hour level, that is, synchronization starts at the specified hour. |
|$.syncConf.scheduleConf.scheduleTime |string |Yes |00:00 |Hour set for automatic synchronization, indicating at which hour of the day synchronization starts.<br><br>When frequency is set to hour or minute level,<br><br>scheduleTime is at the minute level, that is, synchronization starts at the specified minute. |


<span id="a22658c5"></span>
#### Response example

```json
{
    "code": "aeolus/ok",
    "data": "{{dataSetId}}",
    "msg": "成功"
}
```


<span id="_3-3-更新数据集同步任务设置-高级设置"></span>
## 2.3 Update dataset synchronization task settings \- advanced settings


* Permission requirements

   
   |Resource |Permission |
   |---|---|
   |Dataset |write |
   

* API description: Update the advanced settings in the dataset synchronization settings, corresponding to the advanced configuration section of the dataset frontend.

   **This API performs a full update. All configuration information must be provided in the request.** 

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_298e4c9259e977bfab25fc18e76064c9.png) </span>


<span id="4dbc9fa8"></span>
#### Request description

Request URL: `{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/syncSettings/advanced`

<span id="354d4b1d"></span>
#### Request example

```bash
curl --location --request PUT '{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/syncSettings/advanced' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}' \
--data-raw '{
    "yarnName": "root.default_hrtech_da_pm",
    "doradoPriority": "normal",
    "retryNum": 3,
    "retryInterval": 5
}'
```


<span id="a28e0ebb"></span>
#### Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|dataSetId |integer |Yes |123 |Dataset ID |
|doradoPriority |integer |Yes |normal<br><br>high<br><br>super_high |Dataset synchronization priority |
|retryNum |integer |Yes |1 |Number of retry attempts for dataset synchronization failure |
|retryInterval |integer |Yes |5 |Retry interval for dataset synchronization failure (minutes) |


<span id="8f0977b2"></span>
#### Response example

```json
{
    "code": "aeolus/ok",
    "data": null,
    "msg": "成功"
}
```


<span id="8f7eef0e"></span>
## 2.4 View dataset synchronization task status information


* Permission requirements

   
   |Resource |Permission |
   |---|---|
   |Dataset |read |
   

* API description: View the list of synchronization tasks for a dataset, including business date, synchronization status, synchronization time, and more.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d96e167ee21d5fa46a8a97b9af85ed5c.png) </span>


<span id="4106757c"></span>
#### Request description


* Request URL:


`{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/syncJob`

<span id="1c630ac2"></span>
#### Request example

```bash
curl --location --request GET '{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/syncJob?startDate=2022-12-13&endDate=2022-12-15&nodeId' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}'
```


<span id="ef35881a"></span>
#### Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|dataSetId |integer |Yes |123 |Dataset ID |
|startDate |string |Yes |2022\-12\-07 |Business date range for synchronization task \- start time |
|endDate |string |Yes |2022\-12\-11 |Business date range for synchronization task \- end time |
|nodeId |string |No |af2f28ea\-f96a\-49f9\-ac99\-7587364df5f4 |Synchronization task list for dimension tables<br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_163bf4acf630e32c37dd0734d2545f6f.png) </span> |


<span id="2ab02681"></span>
#### Response parameters


|Parameter |Type |Description |
|---|---|---|
|bizTime |string |Dataset backtracking configuration |
|bizTimePage |string |Default backtracking period after dataset is created for the first time |
|diagPageUrl |string |Synchronization task diagnostic page URL |
|instanceDurationTime |string |Synchronization duration of the synchronization task instance |
|instanceId |integer |Synchronization task instance ID |
|logPageUrl |string |Synchronization task instance log URL |
|scheduledStartTime |string |Synchronization task instance start time |
|syncEndTime |string |Synchronization task instance end time |
|tableSize |integer |Data size synchronized by the synchronization task instance |
|syncStatus |integer |Synchronization task instance status |


```json
{
    "code": "aeolus/ok",
    "data": {
        "instanceList": [
            {
                "bizTime": "2022-12-15 00:00:00",
                "bizTimePage": "2022-12-15",
                "diagPageUrl": "https://data.bytedanc*.net/dorado/instance-detail/diagnosis?project=cn_756&id=108301911&schedule=2022-12-15%2000%3A00%3A00&pid=756&status=2&instanceId=1324365220&groupName=cn",
                "instanceDurationTime": null,
                "instanceId": 1324365220,
                "instanceSign": "8332ea1af3a3d960**************",
                "logPageUrl": "https://data.bytedanc*.net/dorado/instance-detail/log?project=cn_7**&id=1********&schedule=2022-12-15%2000%3A00%3A00&pid=7**&instanceId=1324365220&groupName=cn",
                "scheduledStartTime": "2022-12-16 00:00:00",
                "syncEndTime": null,
                "syncStartTime": null,
                "syncStatus": 2,
                "syncStatusDescCode": 3,
                "tableSize": "-",
                "taskId": 9178
            },
            {
                "bizTime": "2022-12-14 00:00:00",
                "bizTimePage": "2022-12-14",
                "diagPageUrl": "https://data.bytedanc*.net/dorado/instance-detail/diagnosis?project=cn_756&id=108******&schedule=2022-12-14%2000%3A00%3A00&pid=756&status=4&instanceId=132*******&groupName=cn",
                "instanceDurationTime": 501.0,
                "instanceId": 1322531180,
                "instanceSign": "b1285**************",
                "logPageUrl": "https://data.bytedanc*.net/dorado/instance-detail/log?project=cn_756&id=108******&schedule=2022-12-14%2000%3A00%3A00&pid=756&instanceId=132*******&groupName=cn",
                "scheduledStartTime": "2022-12-15 00:00:00",
                "syncEndTime": "2022-12-15 00:33:29",
                "syncStartTime": "2022-12-15 00:25:08",
                "syncStatus": 4,
                "syncStatusDescCode": 30,
                "tableSize": "56",
                "taskId": 9***
            },
            {
                "bizTime": "2022-12-13 00:00:00",
                "bizTimePage": "2022-12-13",
                "diagPageUrl": "https://data.bytedanc*.net/dorado/instance-detail/diagnosis?project=cn_756&id=108301911&schedule=2022-12-13%2000%3A00%3A00&pid=7**&status=4&instanceId=132*******&groupName=cn",
                "instanceDurationTime": 1197.0,
                "instanceId": 1322222925,
                "instanceSign": "af3a3d960**************",
                "logPageUrl": "https://data.bytedanc*.net/dorado/instance-detail/log?project=cn_756&id=108*******&schedule=2022-12-13%2000%3A00%3A00&pid=7**&instanceId=132*******&groupName=cn",
                "scheduledStartTime": "2022-12-14 00:00:00",
                "syncEndTime": "2022-12-14 12:38:57",
                "syncStartTime": "2022-12-14 12:19:00",
                "syncStatus": 4,
                "syncStatusDescCode": 30,
                "tableSize": "56",
                "taskId": 9178
            }
        ],
        "total": 3
    },
    "msg": "成功"
}
```



* Remarks

   * Definition of example values for dataset task instance status.

      
      |syncStatus values |Instance status |
      |---|---|
      |1 |Not ready |
      |2 |Pending execution |
      |3 |In progress |
      |4 |Success |
      |5 |Failure |
      |6 |Terminated |
      


<span id="_3-5-提交数据集同步任务回溯"></span>
## 2.5 Submit dataset synchronization job backtracking


* Permission requirements

   
   |Resource |Permission |
   |---|---|
   |Dataset |write |
   

* API description and notes: Submit synchronization job instances in batches to perform data backtracking.

   Caution: The selectable range for the backtracking date and time period must be less than or equal to the dataset's data lifecycle (ttl).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f079dc99a05c2b58a7b797f874e4f47a.png) </span>


<span id="6b676290"></span>
#### Request description


* Request URL: `{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/syncJob`


<span id="a9b420d1"></span>
#### Request example

```bash
curl --location --request POST '{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/syncJob' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}' \
--data-raw '{
    "nodeId": "",
    "startDate": "2022-12-07",
    "endDate": "2022-12-11",
    "checkMinMax": true,
    "skipCheck": true,
    "isSpecifyQueue": true,
    "queueName": "root.oryx_aeolus_vip",
    "maxParallelism": 10
}'
```


<span id="ebb25b36"></span>
#### Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|dataSetId |integer |Yes |123 |Dataset ID |
|nodeId |string |No |af2f28ea\-f96a\-49f9\-ac99\-7587364df5f4 |If not specified, the main table data is backtracked by default; if specified, the dimension table data is backtracked. |
|startDate |string |Yes |2022\-12\-07 |Business date range for synchronization task \- backtracking start time |
|endDate |string |Yes |2022\-12\-11 |Business date range for synchronization task \- backtracking end time |
|checkMinMax |bool |No |true |Check whether the synchronization partition range exceeds the limit |
|skipCheck |bool |No |true |Skip dependency check |
|isSpecifyQueue |bool |No |true |Whether to specify queue backtracking (non\-TOB environment) |
|queueName |string |No |root.oryx_aeolus_vip |Specified queue name (non\-TOB environment) |
|maxParallelism |integer |No |10 |The maximum number of instances for the current synchronization task, mainly used for batch backtracking to prevent all backtracking instances from being triggered and executed at the same time.<br><br>Example: If 100 instances are backfilled and the maximum concurrency is set to 50, at most 50 instances will be running simultaneously, while the remaining 50 will be queued for execution. |


<span id="a9e0eac6"></span>
#### Response example

```json
{
    "code": "aeolus/ok",
    "data": "ok",
    "msg": "成功"
}
```


<span id="_3-6-终止数据集同步任务实例"></span>
## 3.6 Terminate dataset synchronization job instances


* Permission requirements

   
   |Resource |Permission |
   |---|---|
   |Dataset |write |
   

* API description and notes: Terminate job instances in batches. Available in version **2.60.0** .

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_30ef481c82bd1209e4c1f3f2ed0064a1.png) </span>


<span id="66be76bf"></span>
#### Request description


* Request URL: `{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/stopSyncJob`


<span id="108bee8b"></span>
#### Request example

```bash
curl --location --request POST '{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/stopSyncJob' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}' \
--data-raw '{
    "instanceList": [
        {
            "id": 226*******, 
            "taskTime": "2023-12-25 00:00:00",
            "sign": ""
        },
        {
            "id": 226*******, 
            "taskTime": "2023-12-24 00:00:00"
        }
     ],
    "nodeId": ""
}'
```


<span id="6436d519"></span>
#### Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|$.nodeId |string |No |af2f28ea\-f96a\-49f9\-ac99\-7587364df5f4 |If not specified, the primary table task instance will be terminated by default; if a value is provided, the dimension table task instance will be terminated. |
|$.instanceList |object |Yes |*  |Scope of instances to terminate |
|$.instanceList.id |string |Yes |2263796858 |The ID of the task instance to terminate. You can obtain the instanceId from the **View dataset synchronization task status API**. |
|$.instanceList.taskTime |string |Yes |2023\-12\-25 00:00:00 |The business date of the task instance to terminate. You can obtain the bizTime from the **View dataset synchronization task status API**. |
|$.instanceList.sign |string |Yes |f2244702cb94ef3d405f60985b421835 |The signature of the synchronization task instance. You can obtain the instanceSign from the **View dataset synchronization task status API**. |


<span id="906f6834"></span>
#### Response example

```json
{
    "code": "aeolus/ok",
    "data": "ok",
    "msg": "成功"
}
```


<span id="58b6ca59"></span>
## 3.7 View details of dataset synchronization job instances


* Permission requirements



|Resource |Permission |
|---|---|
|Dataset |read |



* API description and notes: View detailed information of a job instance by dataset ID and instance ID. Available in version **2.64.0**


<span id="0a44b468"></span>
#### Request description


* Request URL: `{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/instanceInfo`


<span id="61fefcda"></span>
#### Request example

```Bash
curl --location --request POST '{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/instanceInfo' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}' \
--data-raw '{"instance_id_list": [94]}'
```


<span id="76eda9f0"></span>
#### Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|instance_id_list |array |Yes |["2263796858"] |Set of synchronization task instance IDs. You can obtain the instanceId from the **View dataset synchronization task status API**. |


<span id="9815292f"></span>
#### Response parameters


|Name |Type |Description |
|---|---|---|
|id |integer |Synchronization task instance ID |
|*scheduleTaskId* |integer |Synchronization task ID |
|*subTaskId* |integer |Synchronization task output node ID |
|*taskId* |integer |Synchronization task PrepID |
|appExternalId |string |YARN task ID |
|*createTime* |string |Synchronization task instance creation time |
|*taskTime* |string |Synchronization task instance business date |
|startTime |string |Synchronization task instance start time |
|*endTime* |string |Synchronization task instance end time |
|*scheduleTime* |string |Synchronization task instance schedule time |
|*status* |string |Synchronization task instance status |
|*triggerType* |string |Synchronization task instance trigger type. Possible values: SCHEDULED (routine), BACKFILL (backfill). |


<span id="68574510"></span>
#### Response example

```JSON
{
    "code": "aeolus/ok",
    "data": [
        "id": 94,
        "scheduleTaskId": 3,
        "subTaskId": 2,
        "taskId": 1,
        "appExternalId": "application_17***********_****",
        "createTime": "2024-02-23 23:00:00",
        "taskTime": "2024-02-23 20:00:00",
        "startTime": "2024-02-24 00:01:01",
        "endTime": "2024-02-24 00:02:01",
        "scheduleTime": "2024-02-24 00:00:00",
        "status": "SUCCEEDED",
        "triggerType": "BACKFILL"
    ]
    "msg": "成功"
}
```
