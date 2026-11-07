---
title: "Error Code"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/Error-Code-v2"
---

If the API call is successful, the HTTP status code returned should be 200. If the status code is other, the interface call failed. You can view the detailed error information contained in the response data segment and see the corresponding solution according to the following table.


|**HTTP status code** |**ErrorCode** |**ErrorMessage** |**Product documentation** |
|---|---|---|---|
|500 |InternalError |The request failed due to some unknown error, exception or failure. |Internal error, please contact technical support to troubleshoot. |
|500 |ServiceBusy |The service is busy. Try again later. |The service is busy, please try again later. |
|400 |InvalidParameter. |The specified parameter% s is not valid. |The parameter value is invalid, please refer to the API documentation to set the correct parameters. |
|400 |InvalidTopicName. AlreadyExists |The specified topic name already exists. |Topic name already exists, please replace it with a new one. |
|400 |InvalidUserName. AlreadyExists |The specified user name already exists. |The SASL username already exists, please replace it with a new one. |
|400 |InvalidGroupId. AlreadyExists |The specified Group ID already exists. |The Group ID already exists, please replace it with a new Group ID. |
|400 |QuotaExceeded. PartitionNumber |The number of partitions exceeds the limit. |The number of partitions exceeds the upper limit, please buy more partitions by upgrading the instance specification. |
|400 |QuotaExceeded. UserNumber |The number of users exceeds the limit. |The number of SASL users exceeds the upper limit, please delete the idle user before creating the user. |
|400 |QuotaExceeded. GroupNumber |The number of groups exceeds the limit. |The number of Groups exceeds the upper limit, please delete the idle Group and try again. |
|400 |OperationDenied. InvalidRequest |The request that you specified is not valid. |The request is abnormal, please check and try again. Possible reasons include: invalid request structure, mismatch of Kafka version numbers, etc. If the retry still fails to call successfully, please contact technical support. |
|400 |OperationDenied. ChargeTypeIsPrepaid |It's forbidden to release a prepaid instance within validity period. |Deleting instances during the contract period is not supported. |
|400 |OperationDenied. SSLCertificationOutOfDate |The SSL certification used is out of date. Please contact customer service to update the certification first. |The SSL certificate used by the instance has expired, please contact customer service to replace the certificate. |
|403 |OperationDenied. AccountNotAuthorized |You are not authorized to perform this operation. |The currently logged in Byteplus Engine account does not have permissions for related operations or resources. Please authorize or switch accounts and try again. |
|403 |OperationDenied. InvalidInstanceStatus |The operation is not valid for the current status of the instance. |The current instance state does not allow this operation, usually because the instance state is not running. |
|403 |OperationDenied. InvalidTopicStatus |The operation is not valid for the current status of the topic. |The current topic state does not allow this operation. |
|403 |OperationDenied. InstanceNotEmpty |The instance that you tried to delete is not empty. |The instance you expect to delete is not empty. Please delete all resources in the instance and try again. |
|403 |OperationDenied. GroupNotEmpty |The group is not empty. |Group is not empty, please stop all consumers in the Group and try again. |
|403 |OperationDenied. TaskIsRunning |An operation is currently in progress. Try again later. |The background task is running, please try again later. |
|404 |InvalidInstanceId. NotFound |The specified Instance ID does not exist. |The instance name does not exist, please check and try again. |
|404 |InvalidTopicName. NotFound |The specified topic does not exist. |Topic does not exist, please check and try again. |
|404 |InvalidUserName. NotFound |The specified user name already exists. |The SASL user does not exist, please check and try again. |
|404 |InvalidMeaasgeOffset |There is no message returned. |There are no messages matching the query criteria, please check the Offset or query time and try again. |
