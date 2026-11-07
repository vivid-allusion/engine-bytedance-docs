---
title: "ListMediasAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listmediasapi"
---

Call this API to get information about videos on the playback list of a specific live\-streaming activity. This API supports pagination and allows you to retrieve details such as video ID, name, duration, and online status.

<span id="Request"></span>
## Request

<span id="Details"></span>
### Details


* API operation: `ListMediasAPI`

* Request method: GET

* Request URI: `http://livesaas.byteplusapi.com/?Action=ListMediasAPI&Version=2020-06-01`

* Quota: 120 queries per minute per account


<span id="Query string parameters"></span>
### Query string parameters

Not all shared request parameters are included in the following table. For a complete list, see [Shared request parameters](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967).


|**Parameter Name** |**Required** |**Data Type** |**Description** |
|---|---|---|---|
|Action |Yes |String |API operation. |
|Version |Yes |String |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Yes |Integer |ID of a live\-streaming activity. |
|IsNeedTotalCount |No |Boolean |Whether to return the total number of videos on the playback list. |
|PageNo |Yes |Integer |The page number of the results to return. When you specify this parameter, the results are paginated. |
|PageItemCount |Yes |Integer |The number of results to return per page. |
|Name |No |String |If you specify this field, BytePlus Live returns all videos with names that contain the specified string. |
|Vid |No |String |If you specify this parameter, BytePlus Live returns the video with the specified Vid. |


<span id="Sample request"></span>
### Sample request

```JSON
Get http://livesaas.byteplusapi.com/?Action=ListMediasAPI&Version=2020-06-01&ActivityId=1231231231&PageNo=1&PageItemCount=10
```


<span id="Response"></span>
## Response

<span id="Response schema"></span>
### Response schema


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|PageNo |Integer |Page number. |
|PageItemCount |Integer |The number of results on each page. |
|TotalItemCount |Integer |The total number of videos on the playback list. |
|Medias |Array |Information about the videos. |


<span id="Media"></span>
#### Media


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|MediaId |String |ID of the video on the playback list. You can use this information when calling UpdateMediaOnlineStatusAPI. |
|Name |String |Name of the video. |
|Duration |Integer |Duration of the video (in seconds). |
|SourceType |Integer |Video source:<br><br><br>* 1: Uploaded video file<br><br>* 2: Recorded playback |
|OnlineStatus |Integer |Status of the video:<br><br><br>* 1: Online<br><br>* 2: Offline |
|Vid |String |ID of the video in the media library. |
|CreateTime |Integer |Timestamp when you release the video by calling `UpdateMediaOnlineStatusAPI` . |
|CoverImage |String |Cover image of the playback. |


<span id="Sample response"></span>
### Sample response

```JSON
{
    "ResponseMetadata":{
        "RequestId":"202201201826170101501312091D1C09D2",
        "Action":"ListMediasAPI",
        "Version":"2020-06-01",
        "Service":"livesaas",
        "Region":"ap-singapore-1"
    },
    "Result":{
        "Medias":[
            {
                "MediaId":1,
                "Name":"example",
                "Duration":111,
                "SourceType":1,
                "OnlineStatus":0,
                "vid":"idexample",
                "CreateTime":1541154433671,
                "CoverImage": "//p-example.e.org/example.img"
            }
        ],
        "TotalItemCount":1,
        "PageNo":1,
        "PageItemCount":10           
    }
}
```
