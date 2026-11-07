---
title: "API overview"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/api_overview"
---

This topic summarizes the API interfaces provided by Database Transmission Service (DTS).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In a single region, the API flow control limit of Database Transmission Service (DTS) is 20 times/second, that is, a single BytePlus account can not call a single API interface more than 20 times per second. If this limit is exceeded, the API request fails, and the <code>AccountFlowLimitExceeded</code> error is returned.</div>


<span id=".6K6h6LS5"></span>
## Billing


|API |Description |
|---|---|
|[ModifyInstanceOrder](https://docs.byteplus.com/docs/DTS/ModifyInstanceOrder) |Call the ModifyInstanceOrder API to modify the billing configuration of the task. |


<span id=".5pWw5o2u5Lyg6L6T"></span>
## Data transmission


|API |Description |
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


<span id=".5pWw5o2u6K6i6ZiF77yI5raI6LS557uE566h55CG77yJ"></span>
## Data subscription (consumption group management)


|API |Description |
|---|---|
|[CreateSubscriptionGroup](https://docs.byteplus.com/docs/DTS/createsubscriptiongroup) |Call the CreateSubscriptionGroup API to create a subscription consumer group. |
|[DescribeSubscriptionGroups](https://docs.byteplus.com/docs/DTS/describesubscriptiongroups) |Call the DescribeSubscriptionGroups API to query the subscription consumption group list. |
|[DescribeSubscriptionGroupProgress](https://docs.byteplus.com/docs/DTS/describesubscriptiongroupprogress) |Call the DescribeSubscriptionGroupProgress API to query the progress of the subscription consumer group. |
|[DeleteSubscriptionGroup](https://docs.byteplus.com/docs/DTS/deletesubscriptiongroup) |Call the DeleteSubscriptionGroup API to delete the subscription consumer group. |
|[UpdateSubscriptionGroup](https://docs.byteplus.com/docs/DTS/updatesubscriptiongroup) |Call the UpdateSubscriptionGroup API to modify subscription consumer group name information. |


<span id=".5qCH562-566h55CG"></span>
## Label management


|API |Description |
|---|---|
|[AddTagsToResource](https://docs.byteplus.com/docs/DTS/addtagstoresource) |Call AddTagsToResource to add tags to a task. |
|[DescribeTagsByResource](https://docs.byteplus.com/docs/DTS/describetagsbyresource) |Call DescribeTagsByResource to query the tags of a task. |
|[RemoveTagsFromResource](https://docs.byteplus.com/docs/DTS/removetagsfromresource) |Call the RemoveTagsFromResource API to disassociate the task tag. |


<span id=".5pWw5o2u5qCh6aqM"></span>
## Data verification


|API |Description |
|---|---|
|[CreateValidationTask](https://docs.byteplus.com/en/docs/DTS/createvalidationtask) |Call the CreateValidationTask interface to create a data verification task. |
|[DescribeValidationTaskResult](https://docs.byteplus.com/en/docs/DTS/describevalidationtaskresult) |Call the DescribeValidationTaskResult API to view the data verification result. |
|[DescribeValidationTaskInfo](https://docs.byteplus.com/en/docs/DTS/describevalidationtaskinfo) |Call the DescribeValidationTaskInfo API to view data verification task details. |
|[DescribeValidationTasks](https://docs.byteplus.com/en/docs/DTS/describevalidationtasks) |Call the DescribeValidationTasks interface to query data verification tasks. |
|[DescribeSupportedValidationTypes](https://docs.byteplus.com/en/docs/DTS/describesupportedvalidationtypes) |Call the DescribeSupportedValidationTypes API to view the supported data verification types that can be created. |
|[GetDBTableDiffDetails](https://docs.byteplus.com/en/docs/DTS/getdbtablediffdetails) |Call the GetDBTableDiffDetails API to view the details of different database table data in the data verification task. |
|[ModifyValidationTask](https://docs.byteplus.com/en/docs/DTS/modifyvalidationtask) |Call the ModifyValidationTask API to modify the data verification task. |
|[GenerateValidationResultFile](https://docs.byteplus.com/en/docs/DTS/GenerateValidationResultFile) |Call the GenerateValidationResultFile API to generate diff data. |
|[DownloadValidationTaskResult](https://docs.byteplus.com/en/docs/DTS/DownloadValidationTaskResult) |Call the DownloadValidationTaskResult API to download inconsistent data. |
|[ResumeValidationTask](https://docs.byteplus.com/en/docs/DTS/ResumeValidationTask) |Call the ResumeDataValidationTask API to recover the data verification task. |
|[ResumeValidationTasks](https://docs.byteplus.com/en/docs/DTS/ResumeValidationTasks)    |Call the ResumeDataValidationTasks API to batch recover data verification tasks. |
|[DeleteValidationTask](https://docs.byteplus.com/en/docs/DTS/DeleteValidationTask) |Call the DeleteValidationTask API to delete a data verification task. |
|[DeleteValidationTasks](https://docs.byteplus.com/en/docs/DTS/DeleteValidationTasks) |Call the DeleteValidationTasks API to batch delete verification tasks. |
|[StartValidationTask](https://docs.byteplus.com/en/docs/DTS/StartValidationTask) |Call the StartValidationTask API to start the data verification task. |
|[StartValidationTasks](https://docs.byteplus.com/en/docs/DTS/StartValidationTasks) |Call the StartValidationTasks API to batch start data verification tasks. |
|[RetryValidationTask](https://docs.byteplus.com/en/docs/DTS/RetryValidationTask) |Call the RetryValidationTask API to retry a transmission task. |
|[RetryValidationTasks](https://docs.byteplus.com/en/docs/DTS/RetryValidationTasks) |Call the RetryValidationTasks API to batch retry the task. |
|[SuspendValidationTask](https://docs.byteplus.com/en/docs/DTS/SuspendValidationTask) |Call the SuspendValidationTask API to pause the data verification task. |
|[SuspendValidationTasks](https://docs.byteplus.com/en/docs/DTS/SuspendValidationTasks) |Call the SuspendValidationTasks API to batch pause data verification tasks. |
|[StopValidationTask](https://docs.byteplus.com/en/docs/DTS/StopValidationTask) |Call the StopValidationTask API to terminate a data verification Task. |
|[StopValidationTasks](https://docs.byteplus.com/en/docs/DTS/StopValidationTasks) |Call the StopValidationTasks API to batch terminate verification tasks. |


<span id=".6aKE5qOA5p-l"></span>
## Pre\-check


|API |Description |
|---|---|
|[PreCheckAsync](https://docs.byteplus.com/docs/DTS/precheckasync) |Call the PreCheckAsync API to create and start a pre\-check task for the Database Transmission Service(DTS). |
|[GetAsyncPreCheckResult](https://docs.byteplus.com/docs/DTS/getasyncprecheckresult) |Call the GetAsyncPreCheckResult API to view pre\-check results. |


<span id=".5pWw5o2u5rqQ"></span>
## Data source


|API |Description |
|---|---|
|[CreateDataSource](https://docs.byteplus.com/docs/DTS/createdatasource) |Call the CreateDataSource API to create a data source. |
|[ModifyDataSource](https://docs.byteplus.com/docs/DTS/modifydatasource) |Call the ModifyDataSource API to modify data source information. |
|[ListDataSource](https://docs.byteplus.com/docs/DTS/listdatasource) |Call the ListDataSource API to query the list of data sources. |
|[DescribeDataSource](https://docs.byteplus.com/docs/DTS/describedatasource) |Call the DescribeDataSource API to query the details of a data source. |
|[DeleteDataSource](https://docs.byteplus.com/docs/DTS/deletedatasource) |Call the DeleteDataSource API to delete a data source. |
