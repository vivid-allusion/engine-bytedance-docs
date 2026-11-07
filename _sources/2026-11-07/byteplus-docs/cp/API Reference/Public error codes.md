---
title: "Public error codes"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Public_error_codes"
---


|HTTP Status Code |Error code |Error Message |**Descriptions** |
|---|---|---|---|
|400 |InvalidParameter. |The specified parameter %s is invalid. |Indicates that the parameter is invalid, including type errors, invalid length, invalid enumeration values, or does not match regular expression rules. Example: InvalidParameter.Name |
|400 |MissingParameter. |The required parameter %s is missing. |Indicates missing parameters, for example, a required parameter was not provided. Example: MissingParameter.WorkspaceId |
|400 |OperationDenied. |Operation is denied because %s. |Indicates that certain actions are not permitted. For example, when the pipeline run has reached its final state, cancel actions can no longer be performed. |
|401 |Unauthorized. |The request is refused because it lack authorization for %s |Indicates an authentication error, meaning that the service cannot authenticate the request. For example, this may occur due to a signature mismatch, a missing signature, or a missing access key. |
|403 |AccessDenied |You are not authorized to perform this action. |The request failed the IAM permission verification. It is recommended to first check the IAM policies configured by the user and try again. |
|403 |Deleted. |The request is refused because %s is deleted |The resource has been deleted and the request cannot be processed. |
|404 |NotFound. |The specified {parameter} is not found |The specified resource does not exist. Please confirm, change the target resource name, and then try again. |
|409 |AlreadyExists. |Fail to create resource because the field %s already exist. |The resource already exists. Please change the target resource name and try again. |
|500 |InternalError |The request has failed due to an unknown error. |An unknown error occurred during request processing, for example, a backend service timeout or network instability. |
