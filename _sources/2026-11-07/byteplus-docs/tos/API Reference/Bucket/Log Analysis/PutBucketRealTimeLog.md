---
title: "PutBucketRealTimeLog"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/PutBucketRealTimeLog"
---

<span id="26b7c938"></span>
## Description

This interface is used to enable the log analysis feature.

<span id="lLQsPnBz"></span>
## **Request syntax**

```TypeScript
PUT /?realtimeLog HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Authorization: authorization string
Date: Fri, 18 Apr 2025 09:11:23 GMT

{
    "RealTimeLogConfiguration": {
        "Role": "TOSLogArchiveTLSRole",
        "AccessLogConfiguration": {
            "UseServiceTopic": true,
            "TTL": 7
        }
    }
}
```


<span id="d6ab091b"></span>
## **Request parameters and headers**

For the public request message headers used by this request, see [Public Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** | ** Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|realtimeLog |Query |String |Yes |\- |A special identifier representing the PutBucketRealTimeLog request. |


<span id="eb585a60"></span>
## **Request body elements**


|**Name** | ** Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|RealTimeLogConfiguration |Container |Yes |\- |Configure real\-time logs. |
|Role |String |Yes |TOSLogArchiveTLSRole |The role name is used to grant Object Storage TOS permission to create resources such as project and topic and to write logs in Log Service TLS. You can use the TOS default role TOSLogArchiveTLSRole.<br><br>Parent Node: RealTimeLogConfiguration |
|AccessLogConfiguration |Container |Yes |\- |Configure log resources.<br><br>Parent Node: RealTimeLogConfiguration |
|UseServiceTopic |Bool |Yes |true |For topics created using the TOS service, only the value `true` is supported.<br><br>Parent Node: AccessLogConfiguration |
|TTL |Integer |No |7 |TLS log retention period, measured in days. The valid range is [0, 3650], with a default value of 7 days.<br><br>Parent Node: AccessLogConfiguration |


<span id="45a6a706"></span>
## **Response headers**

For the public response headers returned by this request, please refer to [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="7e049aba"></span>
## **Response body elements**

There are no message elements in this request response.

<span id="2da50b52"></span>
## **Sample request**

```TypeScript
PUT /?realtimeLog HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 18 Apr 2025 09:11:23 GMT
Authorization: authorization string
Content-Length: 280
{
    "RealTimeLogConfiguration": {
        "Role": "TOSLogArchiveTLSRole",
        "AccessLogConfiguration": {
            "UseServiceTopic": true,
            "TTL": 7
        }
    }
}
```


<span id="ce3905bf"></span>
## **Sample response**

```TypeScript
HTTP/1.1 200 OK
x-tos-id-2: f91b0c03a01300c1-a444cd0        
x-tos-request-id: f91b0c03a01300c1-a444cd0            
Date: Fri, 18 Apr 2025 09:11:23 GMT
server: TosServer
Content-Length: 0
```
