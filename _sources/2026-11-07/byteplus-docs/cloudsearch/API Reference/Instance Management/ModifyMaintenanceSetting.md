---
title: "ModifyMaintenanceSetting"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/ModifyMaintenanceSetting"
---

Call ModifyMaintenanceSetting to change the maintenance window and days for instance.

<span id="1442b4b5"></span>
## Background information

To enhance the stability of instances, the back\-end system performs maintenance operations on instances from time to time. The default maintenance window is from 02:00 to 06:00 every morning. You can set the maintenance window during off\-peak hours based on your business patterns. This helps minimize the impact of maintenance on your business.

During the maintenance window on each specified day, the operations and maintenance (O&M) personnel from BytePlus may perform necessary maintenance tasks on your instance. The maintenance days and window you configure indicate that you are aware of and prepared for the potential cluster upgrades and maintenance activities within those periods.

<span id="938e61cd"></span>
## Request Description


* Request method: POST

* Request URL: /?Action=ModifyMaintenanceSetting&Version=2023\-01\-01 HTTP/1.1


<span id="a8f6080c"></span>
## Request parameters

<span id="8157c93a"></span>
### Query


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`ModifyMaintenanceSetting` |The action that you want to perform. Value: `ModifyMaintenanceSetting`. |
|Version |String |Yes |`2023-01-01` |The version of the API. Value: `2023-01-01`. |


<span id="4f0bf180"></span>
### Body


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |o\-00k\*\*\*o718 |The ID of the instance for which you want to change the maintenance window and days. |
|MaintenanceTime |String |Yes |02:00\-04:00 |The UTC time period within a day, during which maintenance activities are allowed. |
|MaintenanceDay |Array of String |No |[<br><br>"MONDAY",<br><br>"TUESDAY",<br><br>"WEDNESDAY",<br><br>"THURSDAY",<br><br>"FRIDAY",<br><br>"SATURDAY"<br><br>] |The list of days within a week, during which maintenance activities are allowed. |


<span id="ddf51e80"></span>
## Response parameters


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Status |String |SUCCESSFUL |Whether the request is successful or failed. |
|Message |String | |The message returned. |


<span id="9c301ef1"></span>
## Sample request

```HTTP
POST https://open.ap-southeast-1.byteplusapi.com/?Action=ModifyMaintenanceSetting&Version=2023-01-01
Content-Type: application/json
X-Date: 20231003T104027Z
Authorization: HMAC-SHA256 
Credential=AKLTMjI2ODVlYzI3ZGY1NGU4ZjhjYWRjMTlmNTM5OTZ****/20231003/ap-southeast-1/ESCloud/request, SignedHeaders=content-type;host;x-date, Signature=88dd0a9ea555d8609ec83eb46054b52f6cd4f79b8d5094fa784c66fa3f2b****
{
    "InstanceId": "o-00k***o718",
    "MaintenanceTime": "02:00-04:00",
    "MaintenanceDay": [
        "MONDAY",
        "TUESDAY"
    ]
}
```


<span id="94fb34f3"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20231020151****008268DFA182854",
        "Action": "ModifyMaintenanceSetting",
        "Version": "2023-01-01",
        "Service": "ESCloud",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Status": "SUCCESSFUL",
        "Message": ""
    }
}
```
