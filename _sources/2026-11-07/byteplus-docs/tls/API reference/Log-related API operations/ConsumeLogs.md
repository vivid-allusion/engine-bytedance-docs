---
title: "ConsumeLogs"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-consumelogs"
---

Call the ConsumeLogs interface to consume the logs.

## Usage notes

* The ConsumeLogs interface consumes the logs of the specified topic shard through the cursor and quantity .

* The Content\-Type of the ConsumeLogs interface response message is application/x\-protobuf, that is, PB format data is returned in the response information. For the PB format of the log service, please refer to [Data encoding method](https://docs.byteplus.com/en/docs/tls/data-encoding-method).

* The call frequency limit of the ConsumeLogs interface is 100 times/s. If the frequency limit is exceeded, an ExceedQPSLimit error will be reported; the traffic limit for each call is 5MiB. If the traffic limit is exceeded, an ExceedRateLimit error will be reported.

* When the number of LogGroups within the specified cursor range exceeds 1000, this call will return `NextCursor`. You can continue to consume by calling the ConsumeLogs interface until the interface reads the `EndCursor` value.

## Request syntax

* Request Method: **POST**

* Request URL: **https://tls\-{Region}.bytepluses.com/ConsumeLogs**

## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

### Query

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|TopicId |String |True |`c7e0e442-19bf-4fb3-b547-5992fb8b****` |The ID of the topic. |
|ShardId |Integer |True |`0` |The ID of the shard. You can obtain the shard list of the specified topic through the DescribeShards interface. |

### Body

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Cursor |String |True |`MT*****` |The cursor refers to the starting point from which data is read. |
|EndCursor |String |False |`MT*****` |The end cursor indicates where to stop reading data, similar to a destination. If `EndCursor` is empty, then no end is set. |
|LogGroupCount |Integer |False |`1000` |The maximum number of loggroups to return. The maximum value is 1000. |
|Compression |String |False |`lz4` |The compression format of the returned data. It can be set as:<br><br><br>* lz4: The compression format is lz4.<br><br>* zlib: The compression format is zlib.<br><br> <br><br>   If consuming logs through Windows SDK, only the zlib compression format is supported. |

## Responses

There are no unique return parameters for this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).

## Sample Request

```json
GET https://tls-{Region}.bytepluses.com/ConsumeLogs?TopicId=c13f36aa-3131-41c7-9862-c1fa5d0****&ShardId=0 
Content-Type: application/json
{
    "Cursor": "MC0wLTAwMD****",
    "EndCursor": "MC0wLTA****",
    "LogGroupCount": 100,
    "Compression": "lz4"
}
```

## Sample Response

```json
HTTP/1.1 200 OK
Content-Type: application/x-protobuf
X-Tls-Cursor: MC0w****
X-Tls-Count: 30
```

## Error code

The following table lists the error codes related to the interface and business logic. For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).

|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |The parameter is invalid. |
|400 |InvalidCursor |specified Cursor is invalid. |The cursor is invalid. |
|404 |TopicNotExist |TopicNotExist |The topic does not exist. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |
