---
title: "Error code"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Error_code"
---

If the API call succeeds, the returned HTTP status code should be 200. Any other code indicates the call failed. You can check the detailed error message in the response data and refer to the following table for the corresponding solution.


|HTTP Code |ErrorCode |ErrorMessage |Specifications |
|---|---|---|---|
|500 |InternalError |The request failed due to some unknown error, exception or failure. |Internal error, contact technical support for assistance. |
|404 |InvalidInstanceId.NotFound |The specified Instance ID does not exist. |The instance name does not exist. Please check and try again. |
|403 |OperationDenied.AccountNotAuthorized |You are not authorized to perform this operation. |The currently logged\-in BytePlus account lacks permission for this operation or resources. Please authorize or switch accounts and try again. |
|403 |OperationDenied.InternetAccessEnabled |Internet access is enabled for the instance. |Public network access is enabled for this instance. It means it is already bound to an EIP. |
|403 |OperationDenied.InternetAccessDisabled |Internet access is disabled for the instance. |This instance does not have public network access enabled, i.e. no EIP is bound. |
|403 |OperationDenied.InvalidInstanceStatus |The operation is not valid for the current status of the instance. |The current instance status does not allow this operation. Usually it is because the instance status is not running. |
|403 |OperationDenied.TaskIsRunning |An operation is currently in progress. Try again later. |The background task is running. Please try again later. |
|400 |InvalidParameter |The specified parameter %s is not valid. |The parameter value %s is invalid. Please refer to the API documentation for correct settings. |
|400 |*UnSupportedConfig* |Unsupported instance configuration, please check. |When creating an instance, the instance specification, disk type, or disk capacity parameters were not configured correctly |
|400 |NotModifiedParameter |The resource was not changed. |The instance configuration has not changed. Please confirm the configuration and try again. |
