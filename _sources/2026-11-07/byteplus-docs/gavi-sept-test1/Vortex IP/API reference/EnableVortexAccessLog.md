---
title: "EnableVortexAccessLog"
product: "Vortex IP"
product_code: "gavi-sept-test1"
source: "https://docs.byteplus.com/en/docs/gavi-sept-test1/EnableVortexAccessLog"
---

Call the EnableVortexAccessLog API to enable access log for Vortex IP.

## **Request parameters**

|Parameter name |Type |Required |Example |Description |
|---|---|---|---|---|
|Action |String |Yes |EnableVortexAccessLog |The action to perform. Value: EnableVortexAccessLog. |
|Version |String |Yes |2020\-04\-01 |API version. The current version is 2020\-04\-01. |
|VortexId |String |Yes |vt\-bp1o94dp5i6ea\*\*\*\* |ID of Vortex IP.<br><br>You can call the [DescribeVortexIPs](https://docs.byteplus.com/en/docs/gavi-sept-test1/DescribeVortexIPs) API to query the ID of Vortex IP. |
|TlsProjectName<br><br> |String |Yes<br><br> |test\-project<br><br> |The name of the access log project.<br><br>The log project name must be unique within the same account and region. |
|TlsTopicName<br><br> |String |Yes<br><br> |test\-topic<br><br> |The name of the access log topic.<br><br><br>* When `TlsTopicName` is set to an existing log topic name, `TlsProjectName` must be set to the corresponding log project name.<br><br>* When `TlsTopicName` is set to a new log topic name, `TlsProjectName` can be set to a new log topic created in the project. |
|EnableTlsTopicIndex |Boolean<br><br> |No |false<br><br> |Specify whether to create log index automatically for a log topic. Values:<br><br><br>* false (default): Do not auto\-create index.<br><br>* true: Auto\-create index. For index parameters created for Vortex IP, see [Managing log service](https://docs.byteplus.com/en/docs/gavi-sept-test1/Managing-log-service). |

## **Response parameters**

|Parameter name |Type |Example |Description |
|---|---|---|---|
|RequestId |String | 2021062415303301022514515207C4\*\*\*\* |The request ID. |
|AccessLogId |String |vtl\-123456\*\*\*\* |The access log ID. |

## **Request example**

```HTTP
GET /?Action=EnableVortexAccessLog&Version=2020-04-01&VortexId=vt-bp1o94dp5i6ea**** HTTP/1.1
Host: open.volcengineapi.com
Service: fasttrack
Region: ap-southeast-1
```

## **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "EnableVortexAccessLog",
        "Version": "2020-04-01",
        "Service": "fasttrack",
        "Region": "ap-southeast-1"
    },
    "Result":{
         "RequestId": "2021062415303301022514515207C4****",
         "AccessLogId":"vtl-123456****"
     }
}
```

## **Error codes**

|**HttpCode** |**Error code** |**Error message** |Description |
|---|---|---|---|
|400 |InvalidTlsTopic.TaggedByOtherService |The specified TLS topic is already occupied by another service. |The specified TLS log topic is occupied by another service. |
||InvalidVortexIP.AccessLogAlreadyEnabled |The access log of the specified VortexIP is already enabled. |Access log is enabled for the specified Vortex IP.​ |
||InvalidVortexIP.InvalidStatus |The specified VortexIP is not in the correct status for the request. |The specified Vortex IP cannot respond to this request due to its status. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |No permission to perform actions on the specified service. |
|404 |InvalidVortexIP.NotFound |The specified VortexIP does not exist. |The specified VortexIP does not exist. |
|412 |TlsServiceNotEnabled |The TLS log service is not enabled for the account. Please enable it first. |TLS is not enabled for the current account. Enable TLS before enabling access log. |
