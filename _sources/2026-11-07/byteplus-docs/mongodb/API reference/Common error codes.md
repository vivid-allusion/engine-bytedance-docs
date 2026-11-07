---
title: "Common error codes"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/error-code"
---

This topic summarizes the common error codes that may occur in Document Database for MongoDB.


|Error code |Description |HTTP code |
|---|---|---|
|DuplicateKey |The operation is not allowed due to the %s parameter input duplicate values. |400 |
|Forbidden.Authentication |The operation is not allowed because the account is not authenticated with a real name. |400 |
|InstanceIsNotRunning |The specified instance is not running. |400 |
|InstanceLBNotFound |The specified network resource LB of the current instance does not exist. |404 |
|InstanceNotFound |The specified instance does not exist. |404 |
|InstanceOrderCreateFailed |Failed to create instance order. |400 |
|InstanceOrderNotFound |The specified instance order does not exist. |404 |
|InstanceStatusNotMatch |The specified instance status does not match. |400 |
|InstanceStorageSpaceTooSmall |The specified StorageSpace cannot be less than %sGB. |400 |
|InsufficientBalance |The operation is not allowed due to insufficient balance in your account. |400 |
|InternalError |The request processing failed with some unknown error, exception, or failure. |500 |
|InvalidAllowListId.NotFound |The specified AllowList does not exist. |400 |
|InvalidAllowListIPList.InvalidIPList |The specified IPList is invalid. |400 |
|InvalidAllowListIPList.IPDuplictae |The specified IPList contains duplicate IP addresses. |400 |
|InvalidAllowListName.Duplicate |The specified AllowList already exists. |400 |
|InvalidIdempotency |The specified request contains invalid idempotency. |409 |
|InvalidInstance.AlreadyExists |The specified instance already exists. |400 |
|InvalidInstanceOrder.AlreadyExists |The specified instance order already exists. |400 |
|InvalidNetWork.NotFound |The operation is not allowed due to unready network resources. |400 |
|InvalidOperator |The operation is not allowed. |400 |
|InvalidParameter |The specified parameter %s is invalid. |400 |
|InvalidParameter.AllowListDescMalformed |Length cannot exceed 200. |400 |
|InvalidParameter.AllowListNameMalformed |Must be 1 to 128 characters in length, and must start with a letter or a Chinese character, and can only contain letters, digits, hyphens (\-), underscores(_) and Chinese characters. |400 |
|InvalidParameter.Format |The specified input parameter format is invalid. |400 |
|InvalidParameter.NotSupport |The specified %s parameter is not supported yet. |400 |
|MissingParameter |The operation is not allowed due to the %s parameter is missing. |400 |
|NamedResourceNotFound |The specified resource {{S1}} {{S2}} does not exist. |400 |
|NoAvailableNodePool |The node pool is unavailable. |400 |
|NodePoolNotExist |The node pool does not exist. |400 |
|OperationDenied |The operation is denied. |400 |
|OperationDenied.AccountAlreadyExists |The operation is not allowed due to the account %s@%s already exists. |400 |
|OperationDenied.AccountNotExist |The operation is not allowed due to the account %s does not exist. |400 |
|OperationDenied.AccountRoleNotExist |The operation is not allowed due to the role %s does not exist. |400 |
|OperationDenied.AllowListIdInuse |The operation is not allowed due to the specified AllowList associated with the instance. |400 |
|OperationDenied.AllowListStatus |The operation is not allowed due to the specified instance %s is not in %v status. |400 |
|OperationDenied.ApplyInstanceNumConflict |The input value for ApplyInstanceNum is %s, but there are %v instances associated with this AllowList. |400 |
|OperationDenied.BackupJobExists |The operation is not allowed due to a backup job is already being processed. |400 |
|OperationDenied.DNSAlreadyExist |The operation is not allowed due to the specified domain name already exists. |400 |
|OperationDenied.ExistCreatingOrder |The operation is not allowed due to an instance order is already being processed. |400 |
|OperationDenied.InstanceClosed |The operation is not allowed due to the instance is closed. |400 |
|OperationDenied.InstanceLockMode |The operation is not allowed due to the instance is locked. |403 |
|OperationDenied.InstanceMaintaining |The operation is not allowed due to the instance is being maintained. |400 |
|OperationDenied.InstancePrepaid |The operation is not allowed due to the instance charge type is prepaid. |400 |
|OperationDenied.InstanceStatus |The operation is not allowed due to the instance status does not match. |400 |
|OperationDenied.InsufficientIp |The operation is not allowed due to insufficient IP address in the target subnet. |400 |
|OperationDenied.MgrBusy |The operation is not allowed due to service busy or existing running jobs. |400 |
|OperationDenied.MongodbServiceError |The operation is not permitted due to MongoDB service error: %v. |400 |
|OperationDenied.NetworkTypeInvalid |The operation is not allowed due to two network types are selected simultaneously. |400 |
|OperationDenied.NetworkTypeMissing |The operation is not allowed due to no network type is selected. |400 |
|OperationDenied.NotBindEip |The operation is not allowed due to the connection address does not associated with EIP. |403 |
|OperationDenied.NotFoundSubnetId |The operation is not allowed due to the Subnet ID does not exist. |403 |
|OperationDenied.PrivateNetworkNotEnable |The operation is not allowed due to the private network is not enabled. |403 |
|OperationDenied.PublicNetworkEndpointNotDelete |The operation is not allowed due to the public network endpoint is not deleted. |403 |
|OperationDenied.ResourceSoldOut |The operation is not allowed because the specified available zone has been sold out. |400 |
|OperationDenied.ScaleWithPublicNetworkOpen |The operation is not allowed due to scaling down Mongos nodes still associated with public networks, disassociate %s first. |400 |
|OperationDenied.UnsupportedAccount |The operation is not allowed due to the %s parameter can only be changed by admin account. |400 |
|OperationDenied.UnsupportedDBVersion |The operation is not allowed due to the DB version %s is unavailable in the specified region. |403 |
|OperationDenied.UnsupportedNetworkType |The operation is not allowed due to the current instance does not support NetworkType %s. |400 |
|OperationUnsupported |The operation is not supported by the specified instance. |400 |
|ProjectNotFound |The specified project does not exist. |404 |
|QuotaExceeded |The %s has exceeded quota %s. |400 |
|QuotaExceeded.AllowList |AllowLists in the region cannot exceed %v. |400 |
|QuotaExceeded.AllowListAssociation |The operation is not allowed due to the AllowList exceeds the association limit. |400 |
|QuotaExceeded.AllowListIP |The number of IP addresses in the AllowList cannot exceed %v. |400 |
|QuotaExceeded.CreateInstance |The operation is not allowed due to the instance quota is insufficient. |400 |
|QuotaExceeded.InstanceAllowList |The operation is not allowed due to the instance exceeds the association limit. |400 |
|QuotaExceeded.InstanceAllowListIP |The number of IP addresses in the AllowList associated with the specified instance exceeds the limit. |400 |
|ResourceAZSoldOut |The operation is not allowed due to the specified available zone %s is sold out. |400 |
|ResourceNotEnough |The operation is not allowed due to insufficient resources. |400 |
|ResourceNotFound |The instance resource does not exist. |400 |
|ResourceScaleSoldOut |The operation is not allowed due to the specified available zone %s is sold out. |400 |
|ScheduleError |Failed to schedule resources. |400 |
|ServiceUnavailable |The request failed due to a temporary server failure. |503 |
|Timeout |The specified operation times out. |400 |
|UnsupportedParameter |The specified %s parameter is not supported. |400 |
|VpcIDNotFound |The specified VpcID does not exist. |404 |
|OperationDenied.InstanceStatusExclusive |The operation is not allowed due to the instance being in %s status. |400 |
|InstanceParamTeplateNumExceedLimit |The operation is not allowed due to the number of parameter templates that can be created exceeds the limit. |400 |
|OperationDenied.InstanceHasRunningEvent |The operation is not allowed due to the instance having running event(s). |400 |


文档变更记录


|时间 |meego |变更说明 |
|---|---|---|
|20241212 |5289066786 |3.12.1版本，新增OperationDenied.InstanceHasRunningEvent错误码 |
|20241212 |飞书多维表格/Vw1BbtKivaFqpmsCdXJcrAObnIl |3.9.2/3.10.2版本新增InstanceParamTeplateNumExceedLimit错误码 |
|20241212 |飞书多维表格/Vw1BbtKivaFqpmsCdXJcrAObnIl |3.8.2版本新增OperationDenied.InstanceStatusExclusive错误码 |
|20240813 |4171910002 |3.6.2版本新增账号管理功能，增加4个账号相关错误码 |
|20240730 |4872228550 |3.6.2版本新增一个对外错误码NamedResourceNotFound |
|202240723 |7790960 |3.6.2版本，产品名称需由【DocumentDB for MongoDB】改为【Document Database for MongoDB】 |
|20240614 |4654693521 |根据api扫描优化建议，增加公共错误码文档，首版发布 |
