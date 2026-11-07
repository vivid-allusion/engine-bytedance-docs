---
title: "Externally Triggered Data Synchronization Tasks"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Externally_Triggered_Data_Synchronization_Tasks"
---

<span id="_1-概述"></span>
# 1. Overview

The product provides OpenAPI interfaces for external users to trigger visual modeling or dataset synchronization tasks.

Caution: Before using the interfaces described in this document, make sure to understand the invocation method. For details, see [Invocation Methods](https://docs.byteplus.com/docs/DataWind/Invocation_Methods).

<span id="_2-操作步骤"></span>
# 2. Error code set

<span id="_2-1-数据集"></span>
## 2.1 Dataset

```Plain
{ 
  "code": "aeolus/ok", 
  "message": "成功"
}

{ 
  "code": "aeolus/openapiClient/tokenERROR", 
  "message": "token不正确" 
}

{ 
  "code": "prep/openAPI/tokenExpired", 
  "message": "token已过期" 
}


```


<span id="_2-2-可视化建模"></span>
## 2.2 Visual modeling

```Plain
{ 
  "code": "prep/ok", 
  "message": "成功"
}

{ 
  "code": "prep/openAPI/tokenError", 
  "message": "token不正确" 
}

{ 
  "code": "prep/openAPI/tokenExpired", 
  "message": "token已过期" 
}


```


<span id="_2-数据集-openapi-接口"></span>
# 3. Dataset OpenAPI interfaces

<span id="_2-1-查询数据集同步配置接口"></span>
## 3.1 Query dataset synchronization configuration interface

**URL**

/aeolus/api/v3/open/dataFactory/dataSetSyncSettings

**HTTP method**: GET


* **Request description:** 



|Parameter |Type |Required or not |Description |Example |
|---|---|---|---|---|
|Authorization |String |Yes |JWT Token |Bearer xxx |



* **Request parameters**



|Parameter |Type |Required or not |Description |Example |
|---|---|---|---|---|
|appId |Long |Yes |Project ID |123 |
|dataSetId |Long |Yes |Dataset ID |102 |



* **Common response parameters**



|Parameter |Type |Description |Example |
|---|---|---|---|
|code |String |Return code |ok |
|msg |String |Return code description |Success |
|data |Object |Business data |See response parameters for the Object schema |



* **Response parameters**



|Parameter |Type |Description |Example value |
|---|---|---|---|
|syncType |Integer |Synchronization type<br><br>0 \- Automatic synchronization<br><br>1 \- Scheduled synchronization<br><br>2 \- Pause synchronization |0 |
|frequency |String |Synchronization frequency<br><br>hourly<br><br>daily<br><br>weekly<br><br>monthly |daily |
|scheduleDay |String |Scheduled run date |0 |
|scheduleTime |String |Scheduled run time |00:00 |
|ttl |Integer |Data lifecycle |7 |


**scheduleDay/scheduleTime examples and descriptions:** 


* **hourly:** 


Example: scheduleDay: "10,17", scheduleTime: "9"

Description: Synchronizes at 10:09 and 17:09 every day


* **daily**


Example: scheduleTime: "03:03"

Description: Synchronizes at 03:03 every day


* **weekly**


Example: scheduleDay: "2,3", scheduleTime: "03:03"

Description: Synchronizes at 03:03 every Tuesday and Wednesday


* **monthly**


Example: scheduleDay: "11,17", scheduleTime: "03:03"

Description: Synchronizes at 03:03 on the 11th and 17th of every month

<span id="_2-2-触发数据同步接口"></span>
## 3.2 Trigger data synchronization interface

**URL：** /aeolus/api/v3/open/dataFactory/createSyncJob

**HTTP method**: POST

*Content\-Type* : application/json


* **Request description**



|Parameter |Type |Required or not |Description |Example |
|---|---|---|---|---|
|Authorization |String |Yes |JWT Token |Bearer xxx |



* **Request parameters**



|Parameter |Type |Required or not |Description |Example |
|---|---|---|---|---|
|appId |Long |Yes |Project ID |8 |
|dataSetId |Long |Yes |Dataset ID |102 |
|startDate |String |Yes |Start business date |2021\-02\-06 02 |
|endDate |String |Yes |End business date |2021\-02\-06 03 |



* **Request example**


```Plain
{"appId":555327,"dataSetId":164381,"startDate":"2021-01-05 03","endDate":"2021-02-06 02"}
```


**startDate/endDate format description:** 

Except for hourly scheduling frequency, the format is yyyy\-MM\-dd, for example, 2021\-02\-04

When the scheduling frequency is hourly, the format is yyyy\-MM\-dd HH, for example, 2021\-02\-04 18

**Caution:**  The synchronization time range cannot exceed the dataset's lifecycle range (ttl)

The dataset lifecycle (ttl) can be obtained through the interface /aeolus/api/v3/open/dataFactory/dataSetSyncSettings


* **Common response parameters**



|Parameter |Type |Description |Example |
|---|---|---|---|
|code |String |Return code |ok |
|msg |String |Return code description |Success |
|data |String |Whether successful |ok |


<span id="_2-3-查询数据集实例接口"></span>
## 3.3 Query dataset instance interface

**URL**：/aeolus/api/v3/open/dataFactory/dataSetSyncInfoAllPage

**HTTP method:**  GET


* **Request description**



|Parameter |Type |Required or not |Description |Example value |
|---|---|---|---|---|
|Authorization |String |Yes |JWT Token |Bearer xxx |



* **Request parameters**



|Parameter |Type |Required or not |Description |Example value |
|---|---|---|---|---|
|appId |Long |Yes |Project ID |8 |
|dataSetId |Long |Yes |Dataset ID |102 |
|startDate |String |Yes |Start business date |2021\-02\-06 02 |
|endDate |String |Yes |End business date |2021\-02\-06 03 |


**startDate/endDate format description:** 

Except for hourly scheduling frequency, the format is yyyy\-MM\-dd, for example, 2021\-02\-04

When the scheduling frequency is hourly, the format is yyyy\-MM\-dd HH, for example, 2021\-02\-04 18


* **Common response parameters**



|Parameter |Type |Description |Example value |
|---|---|---|---|
|code |String |Return code |ok |
|msg |String |Return code description |Success |
|data |Object |Business data |See response parameters for the Object schema |



* **Response parameters**



|Parameter |Type |Description |Example value |
|---|---|---|---|
|total |Integer |Number of instances |8 |
|instanceList |List |Instance list |*  |



* **Instance**



|Parameter |Type |Description |Example value |
|---|---|---|---|
|instanceId |Long |Instance ID |424769294 |
|bizTime |String |Business date |2021\-02\-07 16:00:00 |
|syncStatus |Intger |Sync status |4 \- Run succeeded |
|scheduledStartTime |String |Scheduled time |2021\-02\-06 00:30:00 |
|syncStartTime |String |Synchronization start time |2021\-02\-06 01:30:09 |
|syncEndTime |String |Synchronization end time |2021\-02\-06 01:33:00 |
|instanceDurationTime |Long |Duration (unit: seconds) |193 |


**syncStatus description:** 

1 \- Not ready

2 \- Waiting for execution

3 \- Running

4 \- Run succeeded

5 \- Run failed

6 \- Terminated

7 \- Termination state (will retry)

<span id="_2-4-停止实例同步接口"></span>
## 3.4 Stop instance synchronization interface

**URL**：/aeolus/api/v3/open/dataFactory/stopSyncJob

**HTTP method**: POST

*Content\-Type* : application/json


* **Request description**



|Parameter |Type |Required or not |Description |Example |
|---|---|---|---|---|
|Authorization |String |Yes |JWT Token |Bearer xxx |



* **Request parameters**



|Parameter |Type |Required or not |Description |Example |
|---|---|---|---|---|
|appId |Long |Yes |Project ID |8 |
|dataSetId |Long |Yes |Dataset ID |102 |
|startDate |String |Yes |Start business date |2021\-02\-06 02 |
|endDate |String |Yes |End business date |2021\-02\-06 03 |



* **Request example**


```Plain
{"appId":555327,"dataSetId":164381,"startDate":"2021-02-06 00","endDate":"2021-02-06 01"}

```


**startDate/endDate format description:** 

Except for hourly scheduling frequency, the format is yyyy\-MM\-dd, for example, 2021\-02\-04

When the scheduling frequency is hourly, the format is yyyy\-MM\-dd HH, for example, 2021\-02\-04 18


* **Common response parameters**



|Parameter |Type |Description |Example |
|---|---|---|---|
|code |String |Return code |ok |
|msg |String |Return code description |Success |
|data |String |Success |ok |


<span id="_3-可视化建模-openapi-接口"></span>
# 4. Visual modeling OpenAPI interfaces

<span id="_3-1-查询可执行子任务接口"></span>
## 4.1 Query executable subtask interface

**URL**：/aeolus/prep/userOpenAPI/v1/task/subTasksForExecute

**HTTP method**: GET


* **Request description**



|Parameter |Type |Required |Description |Example value |
|---|---|---|---|---|
|Authorization |String |Yes |JWT Token |Bearer xxx |



* **Request parameters**



|Parameter |Type |Required |Description |Example value |
|---|---|---|---|---|
|taskId |Long |Yes |Visual modeling task ID |15 |



* **Common response parameters**



|Parameter |Type |Description |Example value |
|---|---|---|---|
|code |String |Return code |prep/ok |
|msg |String |Return code description |Success |
|data |List |Business data |See Object Schema in response parameters |



* **Response parameters**



|Parameter |Type |Description |Example value |
|---|---|---|---|
|id |String |Return code |prep/ok |
|outputNodeId |String |Output node ID |Load_1609849563808 |
|dateType |String |Output node type |hive/click_house |
|clusterName |String |Cluster name |rangers |
|dbName |String |Database name |demo_db |
|tableName |String |Table name |demo_tbl |
|scheduleConf |ScheduleConf |Scheduling configuration |*  |
|ctime |String |Creation time |2021\-01\-05 20:26:31 |
|mtime |String |Modification time |2021\-02\-04 19:12:43 |



* **ScheduleConf**



|Parameter |Type |Description |Example value |
|---|---|---|---|
|scheduleType |Integer |Scheduling type:<br><br>0 \- Manual scheduling<br><br>1 \- Periodic execution |0 |
|scheduleFrequency |String |Scheduling frequency:<br><br>hourly<br><br>daily<br><br>weekly<br><br>monthly |daily |
|scheduleTimeSettings |Array |Scheduling time settings |For hourly tasks: to schedule at 00:05 and 05:05 every day, use<br><br>["0,5", "5"] |


scheduleTimeSettings examples and descriptions:


* **hourly:** 


Example: ["0,5", "5"]

Description: Executes at 00:05 and 05:05 every day


* **daily**


Example: ["18:12"]

Description: Executes at 18:12 every day


* **weekly**


Example: ["1,3", "18:12"]

Description: Executes at 18:12 every Monday and Wednesday


* **monthly**


Example: ["1,3", "18:12"]

Description: Executes at 18:12 on the 1st and 3rd of every month

<span id="_3-2-执行子任务接口"></span>
## 4.2 Execute subtask API interface

**URL**：/aeolus/prep/userOpenAPI/v1/task/execute

**HTTP method**: POST

*Content\-Type* : application/json


* **Request description**



|Parameter |Type |Required |Description |Example value |
|---|---|---|---|---|
|Authorization |String |Yes |JWT Token |Bearer xxx |



* **Request parameters**



|Parameter |Type |Required |Description |Example value |
|---|---|---|---|---|
|taskId |Long |Yes |Visual modeling task ID |15 |
|nodeKeys |Array[String] |Yes |Output node ID \- outputNodeId |["Load_1610032647355"] |
|startTime |String |Yes |Start business time |2021\-02\-04 |
|endTime |String |Yes |End business time |2021\-02\-05 |



* **Request example**


```Plain
{"taskId":1104,"nodeKeys":["Load_1609849563808"],"startTime":"2021-02-04","endTime":"2021-02-04"}
```


**startTime/endTime format description:** 

Except when the scheduling frequency is hourly, the format is yyyy\-MM\-dd, for example, 2021\-02\-04

When the scheduling frequency is hourly, the format is yyyy\-MM\-dd HH, for example, 2021\-02\-04 18


* **Common response parameters**



|Parameter |Type |Description |Example value |
|---|---|---|---|
|code |String |Return code |prep/ok |
|msg |String |Return code description |Success |
|data |Boolean |Success |true |


<span id="_3-3-查询任务实例接口"></span>
## 4.3 Query task instance API interface

**URL**：/aeolus/prep/userOpenAPI/v1/task/subTaskInfoList

HTTP method: GET


* **Request description**



|Parameter |Type |Required |Description |Example value |
|---|---|---|---|---|
|Authorization |String |Yes |JWT Token |Bearer xxx |



* **Request parameters**



|Parameter |Type |Required |Description |Example value |
|---|---|---|---|---|
|taskId |Long |Yes |Visual modeling task ID |15 |
|pageNo |Long |No |Page number |1 |
|pageSize |Long |No |Page size |20 |
|startTaskTime |String |No |Start business date |2021\-01\-31 |
|endTaskTime |String |No |End business date |2021\-02\-06 |
|insStatus |String |No |Execution status |default: All<br><br>succeed: Execution succeeded<br><br>failed: Execution failed<br><br>running: Running<br><br>aborted: Terminated |


**Note:**  If startTaskTime/endTaskTime is not specified, startTaskTime will be set to the current time minus 7 days, and endTaskTime will be set to the current time


* **Common response parameters**



|Parameter |Type |Description |Example value |
|---|---|---|---|
|code |String |Return code |prep/ok |
|msg |String |Return code description |Success |
|data |Object |Business data |See Object Schema in response parameters |



* **Response parameters**



|Parameter |Type |Description |Example value |
|---|---|---|---|
|total |Integer |Number of instances |8 |
|list |List |Instance list |*  |



* **Instance**



|Parameter |Type |Description |Example value |
|---|---|---|---|
|id |Long |Instance ID |424769294 |
|taskTimeFormat |String |Business date |2021\-02\-05 00:00 |
|status |Integer |Execution status |4 \- Execution succeeded |
|scheduleRunTime |String |Scheduled execution time |2021\-02\-06 01:30:00 |
|startTime |String |Execution start time |2021\-02\-06 01:30:09 |
|endTime |String |Execution end time |2021\-02\-06 01:33:00 |
|consumeTime |String |Duration |2m 51s |
|node |Node |Output node |See Node Schema in the table below |



* **Node**



|Parameter |Type |Description |Example value |
|---|---|---|---|
|nodeKey |String |Output node ID |Load_1609851218834 |
|nodeName |String |Output node name |Output_1 |



* **Status description:** 


1 \- Not ready

2 \- Waiting to execute

3 \- Running

4 \- Run succeeded

5 \- Run failed

6 \- Terminated

7 \- Termination status (will retry)

<span id="_3-4-终止任务实例接口"></span>
## 4.4 Terminate task instance API interface

**URL**：/aeolus/prep/userOpenAPI/v1/instance/batch/stop

**HTTP method**: POST

*Content\-Type* : application/json


* **Request description**



|Parameter |Type |Required |Description |Example value |
|---|---|---|---|---|
|Authorization |String |Yes |JWT Token |Bearer xxx |



* **Request parameters**



|Parameter |Type |Required |Description |Example value |
|---|---|---|---|---|
|appId |Long |Yes |Project ID |8 |
|taskId |Long |Yes |Visual modeling task ID |15 |
|instances |List |Instance list |Instance list |[{"id":424769297}]} |



* **Instance**



|Parameter |Type |Description |Example value |
|---|---|---|---|
|id |Long |Instance ID |424769294 |



* **Request example**


```Plain
{"appId":555327,"taskId":1105,"instances":[{"id":424769297}]
```



* **Common response parameters**



|Parameter |Type |Description |Example value |
|---|---|---|---|
|code |String |Return code |prep/ok |
|msg |String |Return code description |Success |
|data |Boolean |Success |true |
