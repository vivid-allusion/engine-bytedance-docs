---
title: "UpdateCustomizationViewPermissionAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updatecustomizationviewpermissionapi"
---

Call this API to update the login link for a live activity, enabling you to use your own account system to manage viewing and commenting permissions.

<span id="Request"></span>
## Request

<span id="Details"></span>
### Details


* API operation: `UpdateCustomizationViewPermissionAPI`

* Request method: POST

* Request URI: `https://livesaas.byteplusapi.com/?Action=UpdateCustomizationViewPermissionAPI&Version=2020-06-01`

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
|CustomUrl |Yes |String |The custom login link to your account system. |
|CustomApp |No |String |The name of the custom viewing app. |
|ErrorRedirectUrl |No |String |The URL to redirect to when custom authentication fails. This URL must include the protocol. By default, users are redirected to the default authentication failure page of the live streaming service. |


<span id="Sample request"></span>
### Sample request

```JSON
POST https://livesaas.byteplusapi.com/?Action=UpdateCustomizationViewPermissionAPI&Version=2020-06-01
{
     "ActivityId":123,
     "CustomUrl":"www.example.com" }
```


<span id="Response"></span>
## Response

<span id="Response schema"></span>
### Response schema


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|SecretKey |String |The secret key required to verify viewers against your account system. |


<span id="Sample response"></span>
### Sample response

```JSON
{
   "ResponseMetadata":{
     "RequestId": "201806041104200100100232280022D30",
     "Action":"UpdateCustomizationViewPermissionAPI",
     "Version":"2020-06-01",
     "Service":"livesaas",
     "Region":"ap-singapore-1" 
  },
   "Result":{
       "SecretKey":"qw***" 
  }
}
```
