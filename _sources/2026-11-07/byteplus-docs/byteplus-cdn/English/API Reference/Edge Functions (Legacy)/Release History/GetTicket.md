---
title: "GetTicket"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-GetTicket"
---

This interface is used to retrieve the details of a release record based on the function ID and release ticket ID.

## Limits

Request Throttling: You can send a maximum of 20 requests per second.

## Usage

* Request Method: **GET**

* Request URL: **https://cdn.byteplusapi.com/?Action=GetTicket&Version=2021\-03\-01**

## Request Parameters

### Query Parameters

|  <br><br>Name<br><br>  |  <br><br>Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Example Value<br><br>  |
|---|---|---|---|---|
|  <br><br>Action<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the API.<br><br>  |  <br><br>GetTicket<br><br>  |
|  <br><br>Version<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The version of the API.<br><br>  |  <br><br>2021\-03\-01<br><br>  |
|  <br><br>FunctionId<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The function ID<br><br>  |  <br><br>3gyz993\*\*\*\*<br><br>  |
|  <br><br>TicketId<br><br>  |  <br><br>Int64<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The release record ID<br><br>  |  <br><br>28<br><br>  |

## Response Parameters

|  <br><br>Name<br><br>  |  <br><br>Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Example Value<br><br>  |
|---|---|---|---|
|  <br><br>Ticket<br><br>  |  <br><br>Ticket<br><br>  |  <br><br>Release record details<br><br>  |  <br><br>See the explanation below<br><br>  |

**Ticket**

|  <br><br>Name<br><br>  |  <br><br>Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Example Value<br><br>  |
|---|---|---|---|
|  <br><br>Id<br><br>  |  <br><br>Int64<br><br>  |  <br><br>The release record ID<br><br>  |  <br><br>1<br><br>  |
|  <br><br>FunctionId<br><br>  |  <br><br>String<br><br>  |  <br><br>The function ID<br><br>  |  <br><br>3gyz993\*\*\*\*<br><br>  |
|  <br><br>Content<br><br>  |  <br><br>String<br><br>  |  <br><br>The content of the release record<br><br>  |  <br><br>{\"current_traffics\":[{\"version_tag\":\"1.0.1\"}],\"origin_traffics\":[]}<br><br>  |
|  <br><br>Description<br><br>  |  <br><br>String<br><br>  |  <br><br>Description<br><br>  |  <br><br>this is a sparrow<br><br>  |
|  <br><br>Creator<br><br>  |  <br><br>String<br><br>  |  <br><br>Creator<br><br>  |  <br><br>zhangsan<br><br>  |
|  <br><br>CreateTime<br><br>  |  <br><br>Int64<br><br>  |  <br><br>Creation time<br><br>  |  <br><br>1638326159<br><br>  |
|  <br><br>UpdateTime<br><br>  |  <br><br>Int64<br><br>  |  <br><br>Update time<br><br>  |  <br><br>1638326159<br><br>  |

## Examples

### Sample Request

```HTTP
GET https://cdn.byteplusapi.com/?Action=GetTicket&Version=2021-03-01
&FunctionId=3gyz993****
&TicketId=133
```

### Sample Response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2022011310531001022511001100*****",
        "Action": "GetTicket",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Tickets":
         {
            "Id": 133,
            "FunctionId": "3gyz993****",
            "Content": "{\"current_traffics\":[{\"version_tag\":\"1.0.1\"}],\"origin_traffics\":[]}",
            "Description": "test publish",
            "Creator": "****",
            "CreateTime": 1640077698,
            "UpdateTime": 1640077759
        }
    }
}
```
