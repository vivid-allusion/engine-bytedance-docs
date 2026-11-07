---
title: "GetHotChatAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-gethotchatapi"
---

Call this API to get a list of popular chat messages from a specified live\-streaming activity. A message is considered popular by BytePlus Live if it has received a high number of likes.

<span id="Request"></span>
## Request

<span id="Details"></span>
### Details


* API operation: `GetHotChatAPI`

* Request method: GET

* Request URI: `http://livesaas.byteplusapi.com/?Action=GetHotChatAPI&Version=2020-06-01`

* Quota: 120 queries per minute per account


<span id="Query string parameters"></span>
### Query string parameters

Not all shared request parameters are included in the following table. For a complete list, see [Shared request parameters](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967).


|**Parameter Name** |**Required** |**Data Type** |**Description** |
|---|---|---|---|
|Action |Yes |String |API operation. |
|Version |Yes |String |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Yes |Integer |ID of the live stream activity. |


<span id="Sample request"></span>
### Sample request

```JSON
Get http://livesaas.byteplusapi.com/?Action=GetHotChatAPI&Version=2020-06-01&ActivityId=1231231231
```


<span id="Response"></span>
## Response

<span id="Response schema"></span>
### Response schema


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|ActivityId |Integer |ID of the live stream activity. |
|Data |Array |An array of popular message objects. |


<span id="Chat"></span>
#### Chat


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|ChatId |Integer |ID of the chat message. |
|CreateTime |Integer |The timestamp when the message was sent. |
|TextContent |String |Content of the chat message. |
|User |UserInfo |Information about the sender. |
|IsDelete |Boolean |Whether the chat message has been deleted:<br><br><br>* true: Deleted<br><br>* false: Not deleted |
|LikeCount |Integer |The number of likes this chat message has received. |
|IsPresenter |Boolean |Whether the message is sent by the host:<br><br><br>* true: Sent by the host<br><br>* false: Sent by the viewer |
|reviewStatus |Integer |Review status of the chat message:<br><br><br>* 0: No review required<br><br>* 1: Pending review<br><br>* 2: Approved |


<span id="UserInfo"></span>
#### UserInfo


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|UserId |Integer |ID of the sender. |
|Nickname |String |Nickname of the sender. |


<span id="Sample response"></span>
### Sample response

The following is a sample response for a successful request:

```JSON
{
     "ResponseMetadata" :{
         "RequestId" : "202201201826170101501312091D1C09D2" ,
         "Action" : "GetHotChatAPI" ,
         "Version" : "2020-06-01" ,
         "Service" : "livesaas" ,
         "Region" : "ap-singapore-1" 
    },
     "Result" :{
         "Data" :[
            {
                 "ChatId" :31823336, 
                 "CreateTime" :1591860377, 
                 "TextContent" : "Hello!" , 
                 "User" :{
                     "Nickname" : "111" ,          
                     "UserId" :16690***048647 
                },
                 "IsDelete" :true, 
                 "LikeCount" :3, 
                 "IsPresenter" :false, 
                 "reviewStatus" :0 
            }
        ]
    }
}
```
