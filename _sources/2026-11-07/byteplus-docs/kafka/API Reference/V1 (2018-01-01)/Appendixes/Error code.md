---
title: "Error code"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/Error-code-v1"
---

If the message queue Kafka version of the API is successfully called, the HTTP status code returned should be 2xx. If the status code is other, the interface call failed. You can view the detailed error information contained in the response data segment and see the corresponding solution according to the table below.


|**error code** |**reason** |**workaround** |**HTTP error code** |
|---|---|---|---|
|ErrInternal |An internal error occurred in the system |Please contact technical support |500 |
|ErrInstanceStatus |The state of the instance does not support the corresponding operation |You can try again later. If the retry still fails, you can contact the technical support staff. |500 |
|ErrTopicStatus |The status of the current topic is abnormal |You can try again later. If the retry still fails, you can contact the technical support staff. |500 |
|ErrUserStatus |The current state of the Kafka user is abnormal |You can try again later. If the retry still fails, you can contact the technical support staff. |500 |
|ErrIAASRespFail |IAAS basic service access failed |Infrastructure service access failed, please contact technical support |500 |
|ErrAuthError |Authority judgment failed |Please use the correct permissions to operate the resource. If the error is still returned after troubleshooting, please contact the technical support staff. |400.  |
|ErrResourceNumExceed |Resources have exceeded their limit |Please purchase resources or recreate the instance |400.  |
|ErrParamInvalid |request parameter error |The parameters carried in the request are wrong, please arrange the request parameters on the client side |400.  |
|ErrTopicIsExist |The created topic already exists |The created topic already exists, please change the topic. |400.  |
|ErrUserIsExist |User created already exists |The created User already exists, please replace the User. |400.  |
|ErrInstanceIsExist |The created instance name already exists |The created instance name already exists, please change the instance name |400.  |
|ErrPartitionNumExceed |The current instance has reached the maximum number of partitions allowed to be created |Please purchase partition resources or recreate the instance |400.  |
|ErrInstanceReleaseExistResource |The current instance still has topics that have not been released and cannot be deleted |Please delete the topic resources contained in the instance first, and then delete the instance |400.  |
|ErrTopicNotExist |The requested topic does not exist |Please create a topic first. |404 |
|ErrUserNotExist |The Kafka user requesting access does not exist |Please create a kafka user first. |404 |
|ErrInstanceNotExist |The Kafka instance requesting access does not exist |Please create a kafka instance first |404 |
