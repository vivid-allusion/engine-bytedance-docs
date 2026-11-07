---
title: "CreateActivityAPIV2"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-createactivityapiv2"
---

To programmatically create a live room, you can call the CreateActivityAPIV2 API. This API allows you to create a new live room from scratch, from a pre\-configured template, or by copying an existing live room. Upon successful creation, the API returns a unique activity ID, which you can use with other APIs to manage and customize the live room.

<span id="requirement"></span>
## Requirement

Quota: 120 queries per minute per account

<span id="http-request"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=CreateActivityAPIV2&Version=2020-06-01`

* Method: POST


<span id="request-parameters"></span>
## Request parameters

Not all shared request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters).

<span id="query"></span>
### Query


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`CreateActivityAPIV2` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Set this to `2020-06-01`. |


<span id="body"></span>
### Body


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Name |String |Yes |`Live Room A` |The name of the live room to create, which cannot exceed 1950 characters. |
|LiveTime |Long |No |`1680193976` |The start time of the live stream in Unix timestamp format. Unit: seconds. The time can be accurate to the minute.<br><br>Default value: current time.<br><br>This is the scheduled start time, which may differ from when the live stream actually begins.<br><br>The `LiveTime` must be earlier than the `EndTime`, with a maximum difference of 259,200 (72 hours). |
|IsBeginLiveEnable |Integer |No |`0` |Specifies whether to enforce the scheduled start time. Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: Disables the feature.<br><br>* `1`: Enables the feature. You can only start a live stream after the specified start time. |
|IsAutoEndEnable |Integer |No |`0` |Specifies whether to automatically end the live stream at the specified EndTime. Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: Disables the feature.<br><br>* `1`: Enables the feature.<br><br><br>If you are about to create a live room by copying an existing live room, this configuration of the existing live room will not be copied to the new live room. You can configure whether to enable this feature for the new live room by using this parameter. |
|EndTime |Long |No |`1680293976` |The end time of the live stream in Unix timestamp format. Unit: seconds. The time can be accurate to the minute.<br><br><br>* The `EndTime` must be later than the `LiveTime`, with a maximum difference of 259,200 (72 hours).<br><br>* This parameter is required and valid when the value of `IsAutoEndEnable` is `1`.<br><br>* When copying a live room, this setting is not inherited from the original room. Use this parameter to configure the end time for the new room. |
|LiveMode |Integer |No |`2` |The live stream latency type.<br><br>Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: Ultra\-low or normal latency, matching the type configured in the live room template.<br><br>* `1`: Ultra\-low latency with a latency of 1 to 2 seconds.<br><br>* `2`: Normal latency with a latency of 5 to 10 seconds.<br><br><br>This parameter is ignored if `OldId` is specified. In this case, the new live room has the same latency type as the one configured in the original live room being copied. |
|ViewUrlPath |String |No |`1234` |The viewing page address is formed by appending the `ViewUrlPath` to the base URL (e.g., `https://DomainName/****/`). For example, if the parameter value is `abc`, the viewing page address is `https://DomainName/****/abc`. If not specified, a random value will be generated.<br><br>The length must be within [1, 20] characters. Supported characters include:<br><br><br>* Uppercase letters A–Z<br><br>* Lowercase letters a–z<br><br>* Numbers |
|CoverImage |String |No |`https://tplv-gjr25qtd0-image.image` |The URL of the live room's cover image in landscape mode. If not specified, the default cover image is used.<br><br>Usually, a URL with a protocol header is required as the parameter value. However, if you get the URL of an image uploaded through the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/) (for example, by calling [GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi) to get the URL of a cover image uploaded through the console in a live room), the URL without a protocol header can be used as the parameter value. |
|VerticalCoverImage |String |No |`https://gjr293lqtd0-image.image` |The URL of the live room's cover image in portrait mode. If not specified, the parameter value is the same as that of `CoverImage`.<br><br>Usually, a URL with a protocol header is required as the parameter value. However, if you get the URL of an image uploaded through the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/) (for example, by calling [GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi) to get the URL of a cover image uploaded through the console in a live room), the URL without a protocol header can be used as the parameter value. |
|OldId |Long |No |`17218346****` |The activity ID of an existing live room whose configurations you want to copy to this new live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi).<br><br>This parameter is required if you want to copy the configurations of an existing live room to the new live room. |
|CopyStream |Boolean |No |`true` |Specifies whether to copy the live stream when copying an existing live room.<br><br>Default value: `false`.<br><br>Valid values:<br><br><br>* `true`: Copies the live stream.<br><br>* `false`: Does not copy the live stream. |
|TemplateId |Long |No |`4984658` |The ID of a live room template. The new live room will have the same configurations as the template. You can get the ID by calling [GetAccountTemplateAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getaccounttemplateapi). If this parameter is omitted, the default template is used. If no default template exists, the room is created without a template.<br><br>This parameter is required if you want to create a live room based on a template.<br><br><br>* This parameter is invalid if you set a value of parameter `OldId`.<br><br>* If the template contains a large amount of lucky draw configurations, and you want to copy a live room created based on the template, wait at least 5 minutes after the live room is created before copying it. Otherwise, the lucky draw configurations may not be completely copied. |
|SiteTags |Array of [SiteTags](https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2) |No |`-` |List of category tags in the live room. You can get the supported category tags by calling [ListSiteTagAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listsitetagapiv2).<br><br>If you are about to create a live room by copying an existing live room, the category tag values configured by the existing live room will not be copied to the new live room. You can configure the category tag values for the new live room by using this parameter. |
|TextSiteTags |Array of [TextSiteTags](https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2) |No |`-` |List of text tags in the live room. You can get the supported text tags by calling [ListSiteTagAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listsitetagapiv2).<br><br>If you are about to create a live room by copying an existing live room, the text tag values configured by the existing live room will not be copied to the new live room. You can configure the text tag values for the new live room by using this parameter. |


<span id="sitetags"></span>
#### SiteTags


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Value |String |Yes |1 |The category tag value. |
|Index |Integer |Yes |0 |The index of the category tag, which identifies the display order on the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/). A smaller index value places the tag higher in the display order.<br><br>Value range: [0,19] |


<span id="textsitetags"></span>
#### TextSiteTags


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Value |String |Yes |2 |The text tag value. |
|Index |Integer |Yes |0 |The index of the text tag, which identifies the display order on the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/). A smaller index value places the tag higher in the display order.<br><br>Value range: [0,4] |


<span id="response-parameters"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|ActivityId |Long |`17218312****` |The activity ID of the created live room. |
|ActivityIdStr |String |`-` |Deprecated. |
|Status |Integer |`-` |Deprecated. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```JSON
POST https://livesaas.byteplusapi.com/?Action=CreateActivityAPIV2&Version=2020-06-01 
{ 
    "Name": "Live Room A", 
    "LiveTime": 1680193976,
    "LiveMode": 2    
} 
```


<span id="sample-response"></span>
### Sample response

```JSON
{
  "ResponseMetadata":{
                "RequestId":"2018060411042001001002322800209D2",
                "Action":"CreateActivityAPIV2",
                "Version":"2020-06-01",        
                "Service":"livesaas",
                "Region":"ap-singapore-1"，
                "SystemTime":1656067132
        },
        "Result":{
                "ActivityId":17218312****,
                "ActivityIdStr":"",
                "Status":
        }
}
```


<span id="error-codes"></span>
## Error codes

For a list of shared error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
