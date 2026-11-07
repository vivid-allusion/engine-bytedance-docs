---
title: "DescribeHosts"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-describehosts"
---

Call the DescribeHosts interface to view the host list in the specified host group.

<span id="usage-notes"></span>
## Usage notes


1. This interface is used to view the host list in the specified host group. It supports pagination query, fuzzy query by host IP, and query by host heartbeat status.

   The call frequency limit is 20 times/s, and exceeding the frequency limit will report an error ExceedQPSLimit.


<span id="request-syntax"></span>
## Request syntax


* Request Method: **GET**

* Request URL: **https://tls\-{Region}.bytepluses.com/DescribeHosts**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="query"></span>
### Query


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|HostGroupId |String |True |`6622a14b-770f-4171-a385-3b68486f****` |The ID of the host group. |
|Ip |String |False |`127.0.0.1` |The IP address of the host, used as a fuzzy query. |
|HeartbeatStatus |Integer |False |`1` |The status of the host heartbeat. |
|PageNumber |Integer |False |`1` |The page number when paging the query. The default is 1, that is, the return starts from the first page of data. |
|PageSize |Integer |False |`20` |The page size. The default is 20, with a maximum of 100. |


<span id="responses"></span>
## Responses

The table below only lists the return parameters specific to this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).


|Name |Type |Example |Description |
|---|---|---|---|
|Total |Integer |`2` |The total number of the hosts. |
|HostInfos |Array of [HostInfo](https://docs.byteplus.com/en/docs/38/17344#hostinfo) |`/` |The hosts information. |


<span id="hostinfo"></span>
### HostInfo


|Name |Type |Example |Description |
|---|---|---|---|
|Ip |String |`127.0.0.1` |The IP address of the host. |
|HeartbeatStatus |Integer |`1` |The status of the host heartbeat.<br><br><br>* 0: Heartbeat is normal<br><br>* 1: Heartbeat is abnormal. |
|LogCollectorVersion |String |`1.0.11` |The version of LogCollector installed on the host. |


<span id="sample-request"></span>
## Sample Request

```json
GET https://tls-{Region}.bytepluses.com/DescribeHosts?HostGroupId=6622a14b-770f-4171-a385-3b68486f*****PageSize=20 HTTP/1.1
```


<span id="sample-response"></span>
## Sample Response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "Total": 1,
    "HostInfos": [
        {
            "Ip": "127.0.0.1",
            "LogCollectorVersion": "logcollector-1.0.3",
            "HeartbeatStatus": 0
        }
    ]
}
```


<span id="error-code"></span>
## Error code

The following table lists the error codes related to the interface and business logic. For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |The parameter is invalid. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |


&nbsp;
