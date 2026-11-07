---
title: "Overview"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/overview"
---

To improve ease of use and scalability and meet the needs of more business scenarios, Database Transmission Service (DTS) provides OpenAPI\-SDK. After installing the SDK locally, you can develop based on the OpenAPI provided by Database Transmission Service (DTS).

<span id=".c2RrLeWIl-ihqA=="></span>
## SDK list

Database Transmission Service (DTS) currently provides SDKs in Python and Go. Details are as follows:


|**Language** |**Download URL** |**User guide** |
|---|---|---|
|Python |[DTS Python SDK](https://github.com/volcengine/volc-sdk-python/tree/main/volcengine/example/dts) |[Python SDK](https://docs.byteplus.com/en/docs/DTS/downloading_and_installing_an_sdk) |
|Go |[DTS Go SDK](https://github.com/volcengine/volc-sdk-golang/tree/main/service) |[Go SDK](https://docs.byteplus.com/en/docs/DTS/Downloading_and_installing_the_SDK) |
|Java |[DTS Java SDK](https://github.com/volcengine/volcengine-java-sdk/tree/master/volcengine-java-sdk-dts) |[Java SDK](https://docs.byteplus.com/en/docs/DTS/java_sdk) |


<span id=".Z28tc2RrLeaUr-aMgeeahC1vcGVuYXBpLeaOpeWPow=="></span>
## OpenAPI interfaces supported by Go SDK

<span id=".5pWw5o2u5Lyg6L6T"></span>
### Data transmission


|Interface name |Description |
|---|---|
|[CreateTransmissionTask](https://docs.byteplus.com/en/docs/DTS/CreateTransmissionTask) |Call the CreateTransmissionTask API to create a DTS task. |
|[DescribeTransmissionTaskProgress](https://docs.byteplus.com/en/docs/DTS/describetransmissiontaskprogress) |Call the DescribeTransmissionTaskProgress API to query transmission task progress. |
|[StopTransmissionTasks](https://docs.byteplus.com/en/docs/DTS/StopTransmissionTasks) |Call the StopTransmissionTasks API to batch terminate transmission tasks. |
|[DeleteTransmissionTasks](https://docs.byteplus.com/en/docs/DTS/DeleteTransmissionTasks) |Call the DeleteTransmissionTasks API to batch delete transmission tasks |
|[ResumeTransmissionTasks](https://docs.byteplus.com/en/docs/DTS/ResumeTransmissionTasks) |Call the ResumeTransmissionTasks API to batch recover paused transmission tasks. |
|[StartTransmissionTasks](https://docs.byteplus.com/en/docs/DTS/StartTransmissionTasks) |Call the StartTransmissionTasks to batch start transmission tasks. |
|[RetryTransmissionTasks](https://docs.byteplus.com/en/docs/DTS/RetryTransmissionTasks) |Call the RetryTransmissionTasks API to batch retry failed transmission tasks. |
|[SuspendTransmissionTasks](https://docs.byteplus.com/en/docs/DTS/SuspendTransmissionTasks) |Call the SuspendTransmissionTasks API to batch pause transmission tasks. |
|[DescribeTransmissionTaskInfo](https://docs.byteplus.com/en/docs/DTS/describetransmissiontaskinfo) |Call the DescribeTransmissionTaskInfo API to view the transmission task details. |
|[DeleteTransmissionTask](https://docs.byteplus.com/en/docs/DTS/DeleteTransmissionTask) |Call the DeleteTransmissionTask API to delete a transmission task |
|[RetryTransmissionTask](https://docs.byteplus.com/en/docs/DTS/RetryTransmissionTask) |Call the RetryTransmissionTask API to retry a transmission task. |
|[StopTransmissionTask](https://docs.byteplus.com/en/docs/DTS/StopTransmissionTask) |Call the StopTransmissionTask API to terminate a transmission task. |
|[StartTransmissionTask](https://docs.byteplus.com/en/docs/DTS/StartTransmissionTask) |Call StartTransmissionTask API to start the transmission task. |
|[SuspendTransmissionTask](https://docs.byteplus.com/en/docs/DTS/SuspendTransmissionTask) |Call the SuspendTransmissionTask API to pause the transmission task. |
|[ModifyTransmissionTask](https://docs.byteplus.com/en/docs/DTS/modifytransmissiontask) |Call the ModifyTransmissionTask API to modify the transmission task. |
|[DescribeTransmissionTasks](https://docs.byteplus.com/en/docs/DTS/describetransmissiontasks) |Call the DescribeTransmissionTasks API to view the transmission task list. |
|[ResumeTransmissionTask](https://docs.byteplus.com/en/docs/DTS/ResumeTransmissionTask) |Call the ResumeTransmissionTask API to recover failed transmission tasks. |
|[SetBiSyncDDLSource](https://docs.byteplus.com/en/docs/DTS/SetBiSyncDDLSource) |Call the SetBiSyncDDLSource API to switch the DDL synchronization direction of the bidirectional synchronization task. |


&nbsp;

<span id=".5pWw5o2u5qCh6aqM"></span>
### Data verification


|Interface name |Description |
|---|---|
|[CreateTransmissionTask](https://docs.byteplus.com/docs/DTS/CreateTransmissionTask) |Call the CreateTransmissionTask API to create a DTS task. |
|[DescribeTransmissionTaskProgress](https://docs.byteplus.com/docs/DTS/describetransmissiontaskprogress) |Call the DescribeTransmissionTaskProgress API to query transmission task progress. |
|[DescribeTransmissionTasks](https://docs.byteplus.com/docs/DTS/describetransmissiontasks) |Call the DescribeTransmissionTasks API to view the transmission task list. |
|[DescribeTransmissionTaskInfo](https://docs.byteplus.com/docs/DTS/describetransmissiontaskinfo) |Call the DescribeTransmissionTaskInfo API to view the transmission task details. |
|[StartTransmissionTask](https://docs.byteplus.com/docs/DTS/StartTransmissionTask) |Call StartTransmissionTask API to start the transmission task. |
|[ResumeTransmissionTask](https://docs.byteplus.com/docs/DTS/ResumeTransmissionTask) |Call the ResumeTransmissionTask API to recover failed transmission tasks. |
|[StartTransmissionTasks](https://docs.byteplus.com/docs/DTS/StartTransmissionTasks) |Call the StartTransmissionTasks to batch start transmission tasks. |
|[ResumeTransmissionTasks](https://docs.byteplus.com/docs/DTS/ResumeTransmissionTasks) |Call the ResumeTransmissionTasks API to batch recover paused transmission tasks. |
|[DeleteTransmissionTask](https://docs.byteplus.com/docs/DTS/DeleteTransmissionTask) |Call the DeleteTransmissionTask API to delete a transmission task |
|[DeleteTransmissionTasks](https://docs.byteplus.com/docs/DTS/DeleteTransmissionTasks) |Call the DeleteTransmissionTasks API to batch delete transmission tasks |
|[ModifyTransmissionTask](https://docs.byteplus.com/docs/DTS/modifytransmissiontask) |Call the ModifyTransmissionTask API to modify the transmission task. |
|[RetryTransmissionTask](https://docs.byteplus.com/docs/DTS/RetryTransmissionTask) |Call the RetryTransmissionTask API to retry a transmission task. |
|[RetryTransmissionTasks](https://docs.byteplus.com/docs/DTS/RetryTransmissionTasks) |Call the RetryTransmissionTasks API to batch retry failed transmission tasks. |
|[SuspendTransmissionTask](https://docs.byteplus.com/docs/DTS/SuspendTransmissionTask) |Call the SuspendTransmissionTask API to pause the transmission task. |
|[SuspendTransmissionTasks](https://docs.byteplus.com/docs/DTS/SuspendTransmissionTasks) |Call the SuspendTransmissionTasks API to batch pause transmission tasks. |
|[StopTransmissionTask](https://docs.byteplus.com/docs/DTS/StopTransmissionTask) |Call the StopTransmissionTask API to terminate a transmission task. |
|[StopTransmissionTasks](https://docs.byteplus.com/docs/DTS/StopTransmissionTasks) |Call the StopTransmissionTasks API to batch terminate transmission tasks. |
|[SpawnSwimmingLane](https://docs.byteplus.com/docs/DTS/SpawnSwimmingLane) |Call SpawnSwimmingLane API to configure latency isolation. |


&nbsp;

<span id=".5pWw5o2u6K6i6ZiF"></span>
### Data subscription


|Interface name |Description |
|---|---|
|[CreateSubscriptionGroup](https://docs.byteplus.com/en/docs/DTS/createsubscriptiongroup) |Call the CreateSubscriptionGroup API to create a subscription consumer group. |
|[DescribeSubscriptionGroupProgress](https://docs.byteplus.com/en/docs/DTS/describesubscriptiongroupprogress) |Call the DescribeSubscriptionGroupProgress API to query the progress of the subscription consumer group. |
|[DeleteSubscriptionGroup](https://docs.byteplus.com/en/docs/DTS/deletesubscriptiongroup) |Call the DeleteSubscriptionGroup API to delete the subscription consumer group. |
|[UpdateSubscriptionGroup](https://docs.byteplus.com/en/docs/DTS/updatesubscriptiongroup) |Call the UpdateSubscriptionGroup API to modify subscription consumer group name information. |
|[DescribeSubscriptionGroups](https://docs.byteplus.com/en/docs/DTS/describesubscriptiongroups) |Call the DescribeSubscriptionGroups API to query the subscription consumption group list. |
|[DescribeSubscriptionGroup](https://docs.byteplus.com/en/docs/DTS/describesubscriptiongroup) |Call the DescribeSubscriptionGroup API to query the subscription consumer group. |


&nbsp;

<span id=".6aKE5qOA5p-l"></span>
### Pre\-check


|Interface name |Description |
|---|---|
|[GetAsyncPreCheckResult](https://docs.byteplus.com/en/docs/DTS/getasyncprecheckresult) |Call the GetAsyncPreCheckResult API to view pre\-check results. |
|[PreCheckAsync](https://docs.byteplus.com/en/docs/DTS/precheckasync) |Call the PreCheckAsync API to create and start a pre\-check task for the Database Transmission Service(DTS). |


&nbsp;

<span id=".cHl0aG9uLXNkay3mlK_mjIHnmoQtb3BlbmFwaS3mjqXlj6M="></span>
## OpenAPI interfaces supported by python sdk

<span id=".5pWw5o2u5Lyg6L6T"></span>
### Data transmission


|Interface name |Description |
|---|---|
|[CreateTransmissionTask](https://docs.byteplus.com/en/docs/DTS/CreateTransmissionTask) |Call the CreateTransmissionTask API to create a DTS task. |
|[StartTransmissionTask](https://docs.byteplus.com/en/docs/DTS/StartTransmissionTask) |Call StartTransmissionTask API to start the transmission task. |
|[StopTransmissionTask](https://docs.byteplus.com/en/docs/DTS/StopTransmissionTask) |Call the StopTransmissionTask API to terminate a transmission task. |
|[SuspendTransmissionTask](https://docs.byteplus.com/en/docs/DTS/SuspendTransmissionTask) |Call the SuspendTransmissionTask API to pause the transmission task. |
|[ResumeTransmissionTask](https://docs.byteplus.com/en/docs/DTS/ResumeTransmissionTask) |Call the ResumeTransmissionTask API to recover failed transmission tasks. |
|[RetryTransmissionTask](https://docs.byteplus.com/en/docs/DTS/RetryTransmissionTask) |Call the RetryTransmissionTask API to retry a transmission task. |
|[DeleteTransmissionTask](https://docs.byteplus.com/en/docs/DTS/DeleteTransmissionTask) |Call the DeleteTransmissionTask API to delete a transmission task |
|[ModifyTransmissionTask](https://docs.byteplus.com/en/docs/DTS/modifytransmissiontask) |Call the ModifyTransmissionTask API to modify the transmission task. |
|[DescribeTransmissionTaskProgress](https://docs.byteplus.com/en/docs/DTS/describetransmissiontaskprogress) |Call the DescribeTransmissionTaskProgress API to query transmission task progress. |
|[DescribeTransmissionTaskInfo](https://docs.byteplus.com/en/docs/DTS/describetransmissiontaskinfo) |Call the DescribeTransmissionTaskInfo API to view the transmission task details. |
|[DescribeTransmissionTasks](https://docs.byteplus.com/en/docs/DTS/describetransmissiontasks) |Call the DescribeTransmissionTasks API to view the transmission task list. |


&nbsp;

<span id=".6aKE5qOA5p-l"></span>
### Pre\-check


|Interface name |Description |
|---|---|
|[GetAsyncPreCheckResult](https://docs.byteplus.com/en/docs/DTS/getasyncprecheckresult) |Call the GetAsyncPreCheckResult API to view pre\-check results. |
|[PreCheckAsync](https://docs.byteplus.com/en/docs/DTS/precheckasync) |Call the PreCheckAsync API to create and start a pre\-check task for the Database Transmission Service(DTS). |


&nbsp;
