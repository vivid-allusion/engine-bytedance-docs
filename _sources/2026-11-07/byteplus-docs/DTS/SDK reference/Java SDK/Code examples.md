---
title: "Code examples"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/code-examples"
---

This topic introduces how to use the Database Transmission Service (DTS) Java SDK to quickly call APIs for creating data transmission tasks and querying task information.

<span id="SGNnhDAg"></span>
## Prerequisites


1. [Downloading and installing the SDK is completed](https://docs.byteplus.com/en/docs/DTS/downloading_and_instaling_the_sdk)[.](https://docs.byteplus.com/en/docs/DTS/downloading_and_instaling_the_sdk)

2. [Client initialization is completed](https://docs.byteplus.com/en/docs/DTS/Initializing_the_client?type=preview&lang=en)[.](https://docs.byteplus.com/en/docs/DTS/Initializing_the_client?type=preview&lang=en)


<span id="diWAfnPp"></span>
## Create data transmission task

<span id="i0j8oXUT"></span>
### Creating data migration task

```Java
@Test
public void createTransmissionTaskMigrate() {
    String reqStringMigrate = "{\"TaskName\":\"zqh_test_0319_sdk_01\",\"TrafficSpec\":\"Standard\",\"ProjectName\":\"default\",\"Tags\":[],\"ChargeConfig\":{\"ChargeType\":\"PostPaid\"},\"SrcConfig\":{\"EndpointType\":\"Volc_MySQL\",\"VolcMySQLSettings\":{\"RegionSettings\":{\"Region\":\"cn-beijing\"},\"DBInstanceId\":\"mysql-350fc6******\",\"Username\":\"zqh_******\",\"Password\":\"zqh_******\"}},\"DestConfig\":{\"EndpointType\":\"Volc_MySQL\",\"VolcMySQLSettings\":{\"RegionSettings\":{\"Region\":\"cn-beijing\"},\"DBInstanceId\":\"mysql-91d29f14d1e8\",\"Username\":\"ybw_te******\",\"Password\":\"ybw_te******\"}},\"SolutionSettings\":{\"SolutionType\":\"MySQL2MySQL\",\"MySQL2MySQLSettings\":{\"PolicyForPrimaryKeyConflict\":\"Override\",\"IncrTransmissionSettings\":{\"EnableIncr\":true},\"EnableForeignKeyChecks\":false,\"ObjectMappings\":[{\"ObjectType\":\"Database\",\"SrcObjName\":\"zqh_test_0319\",\"DestObjName\":\"zqh_test_0319\",\"MappingList\":[{\"ObjectType\":\"Table\",\"SrcObjName\":\"*\",\"DestObjName\":\"*\",\"ObjectMappingSetting\":{\"ObjectTransTypes\":[\"Meta\",\"Incr\",\"Full\"],\"SetObjectTransType\":true}},{\"ObjectType\":\"View\",\"SrcObjName\":\"*\",\"DestObjName\":\"*\",\"ObjectMappingSetting\":{\"ObjectTransTypes\":[\"Meta\"]}},{\"ObjectType\":\"Trigger\",\"SrcObjName\":\"*\",\"DestObjName\":\"*\",\"ObjectMappingSetting\":{\"ObjectTransTypes\":[\"Meta\"]}},{\"ObjectType\":\"Function\",\"SrcObjName\":\"*\",\"DestObjName\":\"*\",\"ObjectMappingSetting\":{\"ObjectTransTypes\":[\"Meta\"]}},{\"ObjectType\":\"Procedure\",\"SrcObjName\":\"*\",\"DestObjName\":\"*\",\"ObjectMappingSetting\":{\"ObjectTransTypes\":[\"Meta\"]}},{\"ObjectType\":\"Event\",\"SrcObjName\":\"*\",\"DestObjName\":\"*\",\"ObjectMappingSetting\":{\"ObjectTransTypes\":[\"Meta\"]}}],\"ObjectMappingSetting\":{\"ObjectTransTypes\":[\"Meta\",\"Full\",\"Incr\"],\"SetObjectTransType\":true}}],\"EnableTriggerPreMigration\":false,\"EnableTrxRewrite\":false,\"EnableFullTrxPartitionByChunk\":true,\"MetaTransmissionSettings\":{\"EnableMeta\":true},\"ErrorBehaviorSettings\":{\"MaxRetrySeconds\":600},\"FullTransmissionSettings\":{\"EnableFull\":true,\"ExtraConditions\":[]},\"AccountTransmissionSettings\":{\"EnableAccount\":false}}},\"TaskType\":\"DataMigration\"}";
    String reqString = reqStringMigrate;

    CreateTransmissionTaskRequest createTransmissionTaskRequest = jsonUtil.deserialize(reqString, CreateTransmissionTaskRequest.class);
    createTransmissionTaskRequest.getChargeConfig().setOneStep(true);
    try {
        CreateTransmissionTaskResponse response = dtsApi.createTransmissionTask(createTransmissionTaskRequest);
        System.out.println(response);
        this.taskId = response.getTaskId();
    } catch (ApiException e) {
        System.out.println("createTransmissionTask got exception");
        throw new RuntimeException(e);
    }
}
```


<span id="NclZdfxh"></span>
### Create a data subscription task

```Java
@Test
public void createTransmissionTaskSubscribe() {
    String reqStringSubscription = "{\"TaskName\":\"zqh_test_0319_sdk_sub_01\",\"TrafficSpec\":\"Standard\",\"ProjectName\":\"default\",\"Tags\":[],\"ChargeConfig\":{\"ChargeType\":\"PostPaid\"},\"SrcConfig\":{\"EndpointType\":\"Volc_MySQL\",\"VolcMySQLSettings\":{\"RegionSettings\":{\"Region\":\"cn-beijing\"},\"DBInstanceId\":\"mysql-350fc626808b\",\"Username\":\"zqh_******\",\"Password\":\"zqh_******\"}},\"DestConfig\":{\"EndpointType\":\"Volc_RocketMQ\",\"VolcRocketMQSettings\":{\"RegionSettings\":{\"Region\":\"cn-beijing\"},\"InstanceId\":\"rocketmq-cnoeb389de8*****\",\"Topic\":\"zqh_test_0319\",\"Username\":\"WCN1a31TrzxCfllf8kWrBBk5\",\"Password\":\"zgOUp6jt3vhGJF2ptG******\",\"AuthType\":\"PLAIN\"}},\"SolutionSettings\":{\"SolutionType\":\"MySQL2RocketMQ\",\"MySQL2RocketMQSettings\":{\"SubscriptionSettings\":{\"Protocol\":\"CanalJSON\",\"PartitionPolicy\":\"CustomColumn\"},\"MySQLPosition\":{},\"IncrTransmissionSettings\":{\"Statements\":[\"StmtDMLInsert\",\"StmtDMLUpdate\",\"StmtDMLDelete\",\"StmtDDLAll\"],\"EnableIncr\":true},\"ObjectMappings\":[{\"ObjectType\":\"Database\",\"SrcObjName\":\"zqh_test_0319\",\"DestObjName\":\"zqh_test_0319\",\"MappingList\":[{\"ObjectType\":\"Table\",\"SrcObjName\":\"*\",\"DestObjName\":\"*\",\"ObjectMappingSetting\":{\"PartitionColumn\":\"zqh_test_0319_string_field_01\"}}],\"ObjectMappingSetting\":{\"PartitionColumn\":\"zqh_test_0319_string_field_01\"}}],\"ErrorBehaviorSettings\":{\"MaxRetrySeconds\":600},\"ETLSettings\":{\"Script\":\"\"},\"MetaTransmissionSettings\":{\"EnableMeta\":true},\"FullTransmissionSettings\":{\"EnableFull\":false}}},\"TaskType\":\"DataSubscription\"}";
    String reqString = reqStringSubscription;

    CreateTransmissionTaskRequest createTransmissionTaskRequest = jsonUtil.deserialize(reqString, CreateTransmissionTaskRequest.class);
    createTransmissionTaskRequest.getChargeConfig().setOneStep(true);
    try {
        CreateTransmissionTaskResponse response = dtsApi.createTransmissionTask(createTransmissionTaskRequest);
        System.out.println(response);
        this.taskId = response.getTaskId();
    } catch (ApiException e) {
        System.out.println("createTransmissionTask got exception");
        throw new RuntimeException(e);
    }
}
```


<span id="Dm4n3y9w"></span>
### Create a data synchronization task

```Java
@Test
public void createTransmissionTaskSync() {
    String reqStringSync = "{\"TaskName\":\"zqh_test_0319_sdk_sync_01\",\"TrafficSpec\":\"Compact\",\"ProjectName\":\"default\",\"Tags\":[],\"CreateBackwardSyncTask\":false,\"ChargeConfig\":{\"ChargeType\":\"PostPaid\"},\"SrcConfig\":{\"EndpointType\":\"Volc_MySQL\",\"VolcMySQLSettings\":{\"RegionSettings\":{\"Region\":\"cn-beijing\"},\"DBInstanceId\":\"mysql-350fc626808b\",\"Username\":\"zqh_te******\",\"Password\":\"zqh_******\"}},\"DestConfig\":{\"EndpointType\":\"Volc_MySQL\",\"VolcMySQLSettings\":{\"RegionSettings\":{\"Region\":\"cn-beijing\"},\"DBInstanceId\":\"mysql-91d29f1*****\",\"Username\":\"ybw_te******\",\"Password\":\"ybw_te******\"}},\"SolutionSettings\":{\"SolutionType\":\"MySQL2MySQL\",\"MySQL2MySQLSettings\":{\"PolicyForPrimaryKeyConflict\":\"Override\",\"IncrTransmissionSettings\":{\"Statements\":[\"StmtDDLAll\",\"StmtDMLDelete\",\"StmtDMLInsert\",\"StmtDMLUpdate\"],\"EnableIncr\":true},\"EnableForeignKeyChecks\":false,\"ObjectMappings\":[{\"ObjectType\":\"Database\",\"SrcObjName\":\"zqh_test_0319\",\"DestObjName\":\"ybw_test_0601\",\"MappingList\":[{\"ObjectType\":\"Table\",\"SrcObjName\":\"*\",\"DestObjName\":\"*\",\"ObjectMappingSetting\":{\"ObjectTransTypes\":[\"Meta\",\"Incr\",\"Full\"],\"SetObjectTransType\":true,\"PolicyForKeyConflict\":\"TableOverride\"}},{\"ObjectType\":\"View\",\"SrcObjName\":\"*\",\"DestObjName\":\"*\",\"ObjectMappingSetting\":{\"ObjectTransTypes\":[\"Meta\"]}},{\"ObjectType\":\"Function\",\"SrcObjName\":\"*\",\"DestObjName\":\"*\",\"ObjectMappingSetting\":{\"ObjectTransTypes\":[\"Meta\"]}},{\"ObjectType\":\"Procedure\",\"SrcObjName\":\"*\",\"DestObjName\":\"*\",\"ObjectMappingSetting\":{\"ObjectTransTypes\":[\"Meta\"]}},{\"ObjectType\":\"Trigger\",\"SrcObjName\":\"*\",\"DestObjName\":\"*\",\"ObjectMappingSetting\":{\"ObjectTransTypes\":[\"Meta\"]}},{\"ObjectType\":\"Event\",\"SrcObjName\":\"*\",\"DestObjName\":\"*\",\"ObjectMappingSetting\":{\"ObjectTransTypes\":[\"Meta\"]}}],\"ObjectMappingSetting\":{\"ObjectTransTypes\":[\"Meta\",\"Full\",\"Incr\"],\"SetObjectTransType\":true,\"PolicyForKeyConflict\":\"TableOverride\"}}],\"EnableTriggerPreMigration\":false,\"EnableTrxRewrite\":false,\"EnableFullTrxPartitionByChunk\":false,\"MetaTransmissionSettings\":{\"EnableSyncPostMeta\":false,\"EnableMeta\":true},\"ETLSettings\":{\"Script\":\"\"},\"ErrorBehaviorSettings\":{\"MaxRetrySeconds\":600},\"FullTransmissionSettings\":{\"EnableFull\":true,\"ExtraConditions\":[]},\"AccountTransmissionSettings\":{\"EnableAccount\":false}}},\"TaskType\":\"DataSynchronization\"}";
    String reqString = reqStringSync;

    CreateTransmissionTaskRequest createTransmissionTaskRequest = jsonUtil.deserialize(reqString, CreateTransmissionTaskRequest.class);
    createTransmissionTaskRequest.getChargeConfig().setOneStep(true);
    try {
        CreateTransmissionTaskResponse response = dtsApi.createTransmissionTask(createTransmissionTaskRequest);
        System.out.println(response);
        this.taskId = response.getTaskId();
    } catch (ApiException e) {
        System.out.println("createTransmissionTask got exception");
        throw new RuntimeException(e);
    }
}
```


<span id="kiHHmKoc"></span>
## Query data transmission task information

```Java
@Test
public void describeTransmissionTaskInfo() {
    String reqString = String.format("{\"TaskId\":\"%s\"}", this.taskId);
    DescribeTransmissionTaskInfoRequest describeTransmissionTaskInfoRequest = jsonUtil.deserialize(reqString, DescribeTransmissionTaskInfoRequest.class);
    try {
        DescribeTransmissionTaskInfoResponse response = dtsApi.describeTransmissionTaskInfo(describeTransmissionTaskInfoRequest);
        System.out.println(response);
    } catch (ApiException e) {
        throw new RuntimeException(e);
    }
}
```


<span id="iuPxU62d"></span>
## Pause data transmission task

```Java
@Test
public void suspendTransmissionTask() {
    String reqString = String.format("{\"TaskId\":\"%s\"}", this.taskId);
    SuspendTransmissionTaskRequest request = jsonUtil.deserialize(reqString, SuspendTransmissionTaskRequest.class);

    try {
        SuspendTransmissionTaskResponse response = dtsApi.suspendTransmissionTask(request);
        System.out.println(response);
    } catch (ApiException e) {
        throw new RuntimeException(e);
    }
}
```


<span id="u7n0xmnH"></span>
## Start data transmission task

```Java
@Test
public void startTransmissionTask() {
    String reqString = String.format("{\"TaskId\":\"%s\"}", this.taskId);
    StartTransmissionTaskRequest request = jsonUtil.deserialize(reqString, StartTransmissionTaskRequest.class);

    try {
        StartTransmissionTaskResponse response = dtsApi.startTransmissionTask(request);
        System.out.println(response);
    } catch (ApiException e) {
        throw new RuntimeException(e);
    }
}
```


<span id="WnejXAiO"></span>
## Retry data transmission task

```Java
@Test
public void RetryTransmissionTask() {
    String reqString = String.format("{\"TaskId\":\"%s\"}", this.taskId);
    RetryTransmissionTaskRequest request = jsonUtil.deserialize(reqString, RetryTransmissionTaskRequest.class);

    try {
        RetryTransmissionTaskResponse response = dtsApi.retryTransmissionTask(request);
        System.out.println(response);
    } catch (ApiException e) {
        throw new RuntimeException(e);
    }
}
```


<span id="l1hfsE0p"></span>
## Recover data transmission task

```Java
@Test
public void resumeTransmissionTask() {
    String reqString = String.format("{\"TaskId\":\"%s\"}", this.taskId);
    ResumeTransmissionTaskRequest request = jsonUtil.deserialize(reqString, ResumeTransmissionTaskRequest.class);

    try {
        ResumeTransmissionTaskResponse response = dtsApi.resumeTransmissionTask(request);
        System.out.println(response);
    } catch (ApiException e) {
        throw new RuntimeException(e);
    }

}
```


<span id="0wRs0TGE"></span>
## Terminate data transmission task

```Java
@Test
public void stopTransmissionTask() {
    String reqString = String.format("{\"TaskId\":\"%s\"}", this.taskId);
    StopTransmissionTaskRequest request = jsonUtil.deserialize(reqString, StopTransmissionTaskRequest.class);

    try {
        StopTransmissionTaskResponse response = dtsApi.stopTransmissionTask(request);
        System.out.println(response);
    } catch (ApiException e) {
        throw new RuntimeException(e);
    }

}
```


<span id="NmddsLmr"></span>
## Delete data transmission task

```Java
@Test
public void deleteTransmissionTask() {
    String reqString = String.format("{\"TaskId\":\"%s\"}", this.taskId);
    DeleteTransmissionTaskRequest request = jsonUtil.deserialize(reqString, DeleteTransmissionTaskRequest.class);

    try {
        DeleteTransmissionTaskResponse response = dtsApi.deleteTransmissionTask(request);
        System.out.println(response);
    } catch (ApiException e) {
        throw new RuntimeException(e);
    }
}
```


<span id="PUwRGfyD"></span>
## Create pre\-check task

```Java
ApiClient apiClient = new ApiClient();
apiClient.setEndpoint("dts.cn-beijing.byteplusapi.com.cn");
apiClient.setRegion("cn-beijing");
apiClient.setCredentials(Credentials.getCredentials(AK, SK));
dtsApi = new Dts20180101Api(apiClient);

@Test
public void preCheckAsync() {
    String reqString = String.format("{\"TaskID\":\"%s\"}", this.taskId);

    PreCheckAsyncRequest request = jsonUtil.deserialize(reqString, PreCheckAsyncRequest.class);
    try {
        PreCheckAsyncResponse response = dtsApi.preCheckAsync(request);
        System.out.println(response);
    } catch (ApiException e) {
        throw new RuntimeException(e);
    }
}
```


<span id="4Bn7Wd8V"></span>
## Query pre\-check results

```Java
@Test
public void getAsyncPreCheckResult() {
    String reqString = String.format("{\"ID\":\"%s\"}", this.preCheckID);

    GetAsyncPreCheckResultRequest request = jsonUtil.deserialize(reqString, GetAsyncPreCheckResultRequest.class);
    try {
        GetAsyncPreCheckResultResponse response = dtsApi.getAsyncPreCheckResult(request);
        System.out.println(response);
    } catch (ApiException e) {
        throw new RuntimeException(e);
    }
}
```
