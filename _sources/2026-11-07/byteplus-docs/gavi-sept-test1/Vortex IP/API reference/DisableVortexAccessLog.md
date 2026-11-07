---
title: "DisableVortexAccessLog"
product: "Vortex IP"
product_code: "gavi-sept-test1"
source: "https://docs.byteplus.com/en/docs/gavi-sept-test1/DisableVortexAccessLog"
---

Call the DisableVortexAccessLog interface to disable access log for Vortex IP.

## **Request parameters**

|Parameter name |Type |Required |Example |Description |
|---|---|---|---|---|
|Action |String |Yes |DisableVortexAccessLog |The action to perform. Value: DisableVortexAccessLog. |
|Version |String |Yes |2020\-04\-01 |The API version. The current version is 2020\-04\-01. |
|VortexId |String |Yes |vt\-bp1o94dp5i6ea\*\*\*\* |The ID of the Vortex IP.<br><br>You can call the [DescribeVortexIPs](https://docs.byteplus.com/en/docs/gavi-sept-test1/DescribeVortexIPs) API to query the Vortex IP ID. |

## **Response parameters**

|Parameter name |Type |Example |Description |
|---|---|---|---|
|RequestId |String | 2021062415303301022514515207C4\*\*\*\* |The request ID. |

## **Request example**

```HTTP
GET /?Action=DisableVortexAccessLog&Version=2020-04-01&VortexId=vt-bp1o94dp5i6ea**** HTTP/1.1
Host: open.volcengineapi.com
Service: fasttrack
Region: ap-southeast-1
```

## **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DisableVortexAccessLog",
        "Version": "2020-04-01",
        "Service": "fasttrack",
        "Region": "ap-southeast-1"
    },
    "Result":{
         "RequestId": "2021062415303301022514515207C4****"
     }
}
```

## **Error codes**

|**HttpCode** |**Error code** |**Error message** |Description |
|---|---|---|---|
|400 |InvalidVortexIP.AccessLogNotEnabled |The access log of the specified VortexIP is not enabled. |Access log is not enabled for the specified Vortex IP.​ |
||InvalidVortexIP.InvalidStatus |The specified VortexIP is not in the correct status for the request. |The specified Vortex IP cannot respond to this request due to its status. |
|404 |InvalidVortexIP.NotFound |The specified VortexIP does not exist. |The specified VortexIP does not exist. |
