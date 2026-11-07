---
title: "GetBucketRealTimeLog"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/GetBucketRealTimeLog"
---

<span id="b2a098a6"></span>
## Description

This interface is used to query log configuration information.

<span id="7328ba78"></span>
## **Request syntax**

```TypeScript
GET /?realtimeLog HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 18 Apr 2025 09:24:13 GMT 
Authorization: authorization string
```


<span id="99d92edf"></span>
## **Request parameters and headers**


|**Name** |**Location** |**Parameter Type** |**Required** |**Example Value** |**Description** |
|---|---|---|---|---|---|
|realtimeLog |Query |String |Yes |\- |Represents the special identifier for the GetBucketRealTimeLog request. |


<span id="8b2cd322"></span>
## **Request body elements**

This request contains no request message elements.

<span id="e8eb9ec6"></span>
## Response headers

This request returns public response message headers, See [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="7c095fff"></span>
## **Response body elements**


|**Name** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|RealTimeLogConfiguration |Container |\- |Real\-Time Log Configuration Information |
|Role |String |TOSLogArchiveTLSRole |Role name, used to grant Object Storage Service (TOS) permissions to create resources such as project, topic, and other resources in Log Service (TLS), and to write logs.<br><br>Parent Node: RealTimeLogConfiguration |
|AccessLogConfiguration |Container |\- |Log resource configuration information.<br><br>Parent Node: RealTimeLogConfiguration |
|UseServiceTopic |Bool |true |Topics created using the TOS service only support the value `true`.<br><br>Parent Node: AccessLogConfiguration |
|TTL |Integer |7 |Log retention period, measured in days. The valid range is [0, 3650], with a default value of 7 days.<br><br>Parent Node: AccessLogConfiguration |
|TLSProjectID |String |5f6fea31\-1409\-4123\-acb4\-fd527883\*\*\*\* |Log project ID.<br><br>Parent Node: AccessLogConfiguration |
|TLSTopicID |String |12219dfd\-3280\-42a1\-8988\-e1dcedfb\*\*\*\* |Log Topic ID.<br><br>Parent Node: AccessLogConfiguration |
|TLSDashboardID |String |8667f329\-d640\-14e2\-bc17\-05f3d49b\*\*\*\* |Log Dashboard ID.<br><br>Parent Node: AccessLogConfiguration |


<span id="4d60b6ec"></span>
## **Sample request**

```TypeScript
GET /?realtimeLog HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 18 Apr 2025 09:24:13 GMT
Authorization: authorization string
```


<span id="15256984"></span>
## **Sample response**

```TypeScript
HTTP/1.1 200 OK 
Date: Fri, 18 Apr 2025 09:24:13 GMT 
Server: TosServer 
x-tos-id-2: 1e89f203jld00006-a444fd0 
x-tos-request-id: 1e89f203b2d00006-a444ed0 
Content-Length: 280
 
{
    "RealTimeLogConfiguration": {
        "Role": "TOSLogArchiveTLSRole",
        "AccessLogConfiguration": {
            "UseServiceTopic": true,
            "TLSProjectID": "b7f78471-8cbd-402b-92fa-845b41f0****",
            "TLSTopicID": "fac89300-7ec3-4a3c-9d9d-f9c0e926****",
            "TLSDashboardID": "a43aac77-ac4b-4968-b422-e52360eb****",
            "TTL": 7
        }
    }
}
```
