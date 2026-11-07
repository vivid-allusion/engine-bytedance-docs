---
title: "UpdateActivityMenuAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updateactivitymenuapi"
---

Call this API to update the menu of a live\-streaming activity.

<span id="Request"></span>
## Request

<span id="Details"></span>
### Details


* API operation: `UpdateActivityMenuAPI`

* Request method: POST

* Request URI: `https://livesaas.byteplusapi.com/?Action=UpdateActivityMenuAPI&Version=2020-06-01`

* Quota: 120 queries per minute per account


<span id="Query string parameters"></span>
### Query string parameters

Not all shared request parameters are included in the following table. For a complete list, see [Shared request parameters](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967).


|**Parameter Name** |**Required** |**Data Type** |**Description** |
|---|---|---|---|
|Action |Yes |String |API operation. |
|Version |Yes |String |The version of this API operation. Current version: `2020-06-01`. |


<span id="Body parameters"></span>
### Body parameters


|**Parameter Name** |**Required** |**Data Type** |**Description** |
|---|---|---|---|
|ActivityId |Yes |Integer |ID of a live\-streaming activity. |
|Menus |Yes |Array |The configuration of the menu. |


<span id="Menu"></span>
#### Menu


|**Parameter Name** |**Required** |**Data Type** |**Description** |
|---|---|---|---|
|Name |Yes |String |Name of the tab. |
|Type |Yes |Integer |Tab type:<br><br><br>* 1: Graphic<br><br>* 2: Card<br><br>* 3: Chat interaction<br><br>* 4: Live content<br><br>* 5: Aggregation Live<br><br>* 6: Interactive Q&A |
|Location |Yes |Integer |The display order of the tab, starting from the left. |


<span id="Sample request"></span>
### Sample request

```JSON
POST https://livesaas.byteplusapi.com/?Action=UpdateActivityMenuAPI&Version=2020-06-01
{
     "ActivityId" :732412312,
     "Menus" : [
        {
             "Name" : "Menu name 1" ,
             "Type" : 2,
             "Location" : 1
        },
        {
             "Name" : "Menu name 2" ,
             "Type" : 2,
             "Location" : 2
        }
    ]
}
```


<span id="Response"></span>
## Response

<span id="Response schema"></span>
### Response schema


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|Status |Boolean |Result of the operation:<br><br><br>* true: Success<br><br>* false: Failure |


<span id="Sample response"></span>
### Sample response

Below is a sample response when the request is successfully handled:

```JSON
{
   "ResponseMetadata" :{
     "RequestId" : "201806041104200100100232280022D30" ,
     "Action" : "UpdateActivityMenuAPI" ,
     "Version" : "2020-06-01" ,
     "Service" : "livesaas" ,
     "Region" : "ap-singapore-1" 
  },
   "Result" : {
       "Status" : true
  }
}
```
