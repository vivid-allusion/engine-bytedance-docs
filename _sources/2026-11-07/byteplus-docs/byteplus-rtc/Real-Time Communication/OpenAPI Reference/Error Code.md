---
title: "Error Code"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70426"
---

If the call to OpenAPI fails, you will see the error code and error message in the corresponding result. The following is the error code, and the corresponding instructions and processing methods:


|Error code |Description |Suggestion |
|---|---|---|
|`InvalidParameter.TaskAlreadyExists` |The task already exists |Do not create a task repeatedly |
|`InvalidParameter.StartTimeAfterEndTime` |the start time of querying is later than end time |Modify request parameters |
|`InvalidParameter.OutofTimeRange` |The time range length of the query request exceeded the limit |Modify the time range of the query |
|`InvalidParameter.InvalidRtmpAddress` |The push stream address is not valid |Please confirm the address |
|`InvalidParameter.IllegalRoomID` |Illegal roomId |RoomId format is wrong. Please fill in the correct room ID |
|`InvalidParameter.BodyIsEmpty` |Request content is empty |Please fill in the request parameters |
|`InvalidParameter.Unmarshal` |Request parsing failed |Please fill in the correct parameter format |
|`InvalidParameter.EmptyAccountId` |`AccountId` is empty |Please fill in `AccountId` |
|`InvalidParameter.NotExistAppId` |`AppId` does not exist |Please check your `AppId` |
|`InvalidParameter.IllegalAppId` |`AppId` is not legal |Please check `AppId` |
|`InvalidParameter.IllegalTo` |Username of the client is not legal |Please check the username of the client |
|`InvalidParameter.IllegalFrom` |Username of the server is not legal |Please check the username of the server |
|`InvalidParameter.SizeOverLimit` |Message size exceeds limit |Please reduce the size of message |
|`InvalidParameter.UserCountOverLimit` |The number of users receiving messages exceeds the limit |Please reduce the number of users receiving messages |
|`InvalidParameter.ErrorActiveTaskNotFound` |The task doesn't exist or has stopped |Fill in right `TaskId` |
|`FlowLimitExceeded.TaskNumberOverLimit` |The number of tasks exceeds the limit |The error code doesn`t take effect now \| |
|`FlowLimitExceeded.QPSOverLimit` |Qps exceeded the limit |Do not make requests too frequently |
|`AccessDenied.RecordNotEnabled` |The recording function is not enabled. |Please enable this function on the console |
|`AccessDenied.NoPermissionForApp` |This AccountID doesn't have the permission to operate this AppId |Please use correct AccountID |
|`AccessDenied.ServiceNotEnabled` |Service is not enabled |Please enable the required service in the console |
|`InternalError.GenerateTokenFailed` |Failed to generate token |Please contact Technical Support for details |
|`InternalError.GetAutoTriggerPolicyFailed` |Failed to get automatic recording configuration |Please contact Technical Support for details |
|`InternalError.GetRecordPolicyFailed` |Failed to get the parameter configuration of recording |Please contact Technical Support for details |
|`InternalError.DBCheckTaskExistFailed` |Failed to determine whether this task exists in the database |Please contact Technical Support for details |
|`InternalError.DBCreateTaskFailed` |Failed to create task in database |Please contact Technical Support for details |
|`InternalError.DBReadTaskFailed` |Failed to read task information from database |Please contact Technical Support for details |
|`InternalError.DBUpdateTaskFailed` |Failed to update task information in the database |Please contact Technical Support for details |
|`InternalError.UnknownInternalError` |Unknown internal error |Please contact Technical Support for details |
|`InternalError.TaskRepeat` |Unknown internal error |Please do not repeat requests, or change `TaskId` |
|`InternalError.Unknown` |System failure |Please contact technical support for details |
|`InternalError.DB` |Failed to query Server database. |Please contact technical support for details |
|`InternalError.Executor` |Failed to stop task at server |Please try again |
|`InternalError.ReachRateLimit` |Reach rate limit |Do not make requests too frequently |
|`InternalError.Parallel` |Operate the same task concurrently |Do not request concurrently |
|`InternalError.RPC` |`RPC` call failed |Please reinitiate request |
|`InternalError.NotFound` |Can`t find RTM Edge \| Please reinitiate request \| | |
|`InternalError.UserNotFound` |User receiving message is not found |Re\-initiate request if the user is in room |
|`InternalError.RoomNotFound` |Room not found |Re\-request if room already exists |
|`InternalError.Marshal` |Fail to serialize |Please reinitiate request |
|`InternalError.SendToEdge` |Fail to push to `RTM Edge` |Please reinitiate request |
|`InternalError.Redis` |Fail to read and write `Redis` |Please reinitiate request |
|`InternalError.TaskNotReady` |The task has been submitted but hasn't started running yet |Please contact Technical Support for more information |
|`InternalError.InvalidMeta` |Parameters in the task is invalid |Please contact Technical Support for more information |
|`InternalError.TaskControlError` |There is an error when the task is processed |Please contact Technical Support for more information |
|`InternalError.NotifyConnectionRefused` |Internal connection has been refused |Please contact Technical Support for more information |
|`InternalError.LockContention` |Lock contention times out |Please contact Technical Support for more information |
|`InternalError.ServerError` |Server is error |Please contact Technical Support for more information |
|`ErrorParameter.AppId` |Wrong `AppId`. |Make sure `AppId` is filled in correctly |
|`ErrorParameter.MaxRecordSecond` |`MaxRecordSecond` is wrong |Please fill in the correct value |
|`MissingParameter.NoAppId` |No `AppId` is filled in |Please fill in `AppId` |
|`MissingParameter.NoAccount` |Account ID is not filled in |Please fill in the account ID |
|`MissingParameter.NoAction` |Missing action |Action is not filled in. Please fill in the correct interface name |
|`MissingParameter.NoVersion` |Missing version |Version is not filled in, please fill in the correct interface version |
|`Unauthorized` |The `AppId` filled does not match with the `AppId` under the account ID |Please verify that the `AppId` and account ID are correct |
|`UnknownVersion` |Unknown `Version` |Please reset `version` to `2020-12-01` |
|`UnknownAction` |Unknown `Action` |Please, check if `Action`is defined in Open API |
|`PartialSuccess` |Part of users receive messages successfully |Re\-initiate request if you are sure all users are in the room |
|`UpdateError.UpdateSingleStreamRecordNotSupported` |Update of single\-stream recording is not supported |Update of single\-stream recording is currently not supported. Please do not initiate a update request to a single\-stream recording task. |
|`UpdateError.CurrentLayoutNotSupported` |Update of mixed\-stream recording in the current layout mode is not supported |Please check the layout mode you have set. Only the custom layout mode supports updating a mixed\-stream recording task. |
|`UpdateError.UpdatePushSingleStreamNotSupported` |Update of pushing single\-stream to CDN is not supported |Update of pushing single\-stream to CDN is currently not supported. Please do not initiate a update request to a single\-stream task. |
