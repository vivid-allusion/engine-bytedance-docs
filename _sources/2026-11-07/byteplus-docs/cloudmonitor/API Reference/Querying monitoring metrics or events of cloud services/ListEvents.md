---
title: "ListEvents"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/ListEvents"
---

Query events that occurred within the specified time period.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

Cloud Monitor implements rate limiting on the ListEvents API to ensure API call stability. Your queries per second (QPS) ‌must not exceed 20‌. Otherwise, requests will be throttled.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=ListEvents&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListEvents&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request descriptions


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListEvents |The name of the API. The API name is `ListEvents`. |
|Version |String |Yes |2018\-01\-01 |The API version. The API version is `2018-01-01`. |
|ID |Array of String |No |["155630285718605\*\*\*\*", "155629834700901\*\*\*\*"] |Event ID. The default value is empty, which means querying all events that occurred within the specified time period. |
|StartTime |Integer |No |1659885000 |The start time of the time range. It is a Unix timestamp (in seconds). This time range only applies to the event occurrence time (HappenTime).<br><br>If the `StartTime` and `EndTime` parameters are not set, the default time range is the last 30 minutes. |
|EndTime |Integer |No |1659890000 |The end time of the time range. It is a Unix timestamp (in seconds). This time range only applies to the event occurrence time (HappenTime).<br><br>If the `StartTime` and `EndTime` parameters are not set, the default time range is the last 30 minutes. |
|Source |Array of String |No |["ecs"] |Event source.<br><br>For example, `ecs` represents Elastic Compute Service, `rds_mysql` represents RDS for MySQL, and `redis` represents Cache for Redis.<br><br>An example value is `["testA", "testB", "testC"]`.<br><br>The default value is empty, which means querying all event sources. |
|EventType |Array of String |No |["ecs:Instance:StateChange"] |Event. Each event is in the `event source:event type:event content` format. An example value is `["testA", "testB", "testC"]`.<br><br>For a list of events of each cloud product, see [Cloud product event overview](https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-events). |
|Region |String |No |cn\-shanghai |ID of the availability zone to which the event belongs. |
|PageSize |Integer |No |30 |The number of rows per page for a pagination query. Default value: 30. Mmaximum value: 1000. |
|PageNumber |Integer |No |1 |The page number for a pagination query. Default value: 1. |
|OrderBy |String |No |HappenTime |Event sorting condition. The only supported condition is `HappenTime`, which means sorting by event occurrence time. |
|Asc |Boolean |No |false |Event sorting method. Available types:<br><br><br>* **true**: Ascending order.<br><br>* **false**: Descending order. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=ListEvents&Version=2018-01-01
Content-Type: application/json
{
    "Asc": true,
    "StartTime": 1659885000,
    "EndTime": 1659890000,
    "EventType": [
        "ecs:Instance:StateChange"
    ],
    "ID": [
        "155630285718605****",
        "155629834700901****"
    ],
    "OrderBy": "HappenTime",
    "PageNumber": 1,
    "PageSize": 30,
    "Region": "cn-shanghai",
    "Source": [
        "ecs"
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Asc |Boolean |false |Event sorting method. |
|Data |Array of [EventOpenAPIVo](https://docs.byteplus.com/en/docs/39/16299#eventopenapivo) |\- |Events that meet the query criteria. |
|OrderBy |String |HappenTime |Sorting condition for returned events. |
|PageSize |Integer |30 |The number of items per page for a pagination query. The default value is 30. |
|PageNumber |Integer |1 |The page number for a pagination query. The default value is 1. |
|TotalCount |Integer |10 |The number of events that meet the criteria. |


<span id="eventopenapivo"></span>
### EventOpenAPIVo


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|ID |String |155630285718605\*\*\*\* |Event ID. |
|HappenTime |Integer |1659886490 |Event occurrence time as a Unix timestamp (in seconds). |
|Source |String |ecs |Event source. |
|EventType |String |ecs:Instance:SystemFailure.Redeploy.Executing |Event. |
|Region |String |cn\-shanghai |ID of the availability zone where the event occurred. |
|Detail |Object of [EventAlias](https://docs.byteplus.com/en/docs/39/16299#eventalias) |\- |Original event content in JSON format. |


<span id="eventalias"></span>
### EventAlias


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |String |1658\*\*\*\*\*4000 |Event ID. The unique identifier of the event. |
|data |JSON Map |\- |Event content. It is a JSON object. The content is determined by the service initiating the event. |
|type |String |ecs:Disk:DiskError.Redeploy.Executing |Event type. It reflects the type of events from the event source. |
|ctime |String |2023\-05\-16T14:23:26+08:00 |Time when the event was generated. |
|source |String |ecs |Event source. The service from which the event is produced. |
|subject |String |ecs:cn\-north\-1:21\*\*\*\*\*53:instance/test\-instanceId\-A/tag/test\-instanceId\-B |Event subject. |
|volcregion |String |cn\-guangzhou |The region where the event was received. |
|specversion |String |1.0 |CloudEvents protocol version. |
|volcaccountid |String |21\*\*\*\*\*53 |Account ID. |
|datacontenttype |String |application/json |The content format of the `data` parameter. Only the application/json format is supported. |
|volcpublishtime |String |2023\-05\-16T14:23:26+08:00 |Time when the event was received. |
|publishTimeStamp |Integer |1684218206 |Timestamp when the event was received. |
|volceventbusname |String |default |Name of the event bus receiving the event. |
|volcresourcename |String |test_resource_name_A |The resource name that received the event. |
|dataencoded |Array of Integer |\- |Byte\-formatted extension parameters. |


<span id="data"></span>
### Data


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |resourceid |Key defined in `data`. |
|value |Any |100\*\*\*\* |Value defined in `data`. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "ListEvents",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": [
            {
                "ID": "155630285718605****",
                "Detail": {
                    "id": "1658*****4000",
                    "type": "ecs:Disk:DiskError.Redeploy.Executing",
                    "ctime": "2023-05-16T14:23:26+08:00",
                    "source": "ecs",
                    "subject": "ecs:cn-north-1:21*****53:instance/test-instanceId-A/tag/test-instanceId-B",
                    "volcregion": "cn-guangzhou",
                    "specversion": "1.0",
                    "volcaccountid": "21*****53",
                    "datacontenttype": "application/json",
                    "volcpublishtime": "2023-05-16T14:23:26+08:00",
                    "publishTimeStamp": 1684218206,
                    "volceventbusname": "default",
                    "volcresourcename": "test_resource_name_A"
                },
                "Region": "cn-shanghai",
                "Source": "ecs",
                "EventType": "ecs:Instance:SystemFailure.Redeploy.Executing",
                "HappenTime": 1659886490
            }
        ],
        "PageSize": 30,
        "PageNumber": 1,
        "TotalCount": 2
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).
