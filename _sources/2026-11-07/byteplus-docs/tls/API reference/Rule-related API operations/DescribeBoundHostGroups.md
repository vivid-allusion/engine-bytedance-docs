---
title: "DescribeBoundHostGroups"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/DescribeBoundHostGroups"
---

Call the DescribeBoundHostGroups API to retrieve the list of host groups bound to the collection rule.

<span id=".6K-35rGC6K-05piO"></span>
## Request instructions


* Request method: GET

* Request URL: https://{tls\-endpoint}/DescribeBoundHostGroups


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only request parameters unique to this API and some public parameters. For more information, see [Public Parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="Query"></span>
### Query


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|RuleId |String |Yes |`faf6d529-e75e-457f-a23a-9c4203a6dff3xx` |Collection configuration ID. |
|PageNumber |Integer |No |1 |Page number for paginated queries. The default is 1, which means data returns from the first page. |
|PageSize |Integer |No |20 |Page size. The default is 20, with a maximum of 100. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the return parameters specific to this API are listed in the table below For more information, see [Return structure](https://docs.byteplus.com/en/docs/tls/response-message).


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|HostGroupInfos |Array of [HostGroupInfo](https://docs.byteplus.com/en/docs/38/83206#hostgroupinfo) |/ |Information about host groups linked to the collection configuration |
|Total |Integer |100 |Total number of eligible host groups. |


<span id="hostgroupinfo"></span>
### HostGroupInfo


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|AutoUpdate |Boolean |`true` |LogCollector installed on the host group server has auto\-upgrade function. You can choose whether to enable it.<br><br><br>* true: TLS will perform an upgrade check during the specified time slot each day. If upgrade conditions are met, LogCollector upgrades automatically without manual intervention.<br><br>* false: (default) LogCollector will not upgrade automatically. To use a newer version of LogCollector, see [Upgrade LogCollector](https://docs.byteplus.com/docs/tls/upgrade_logcollector_on_a_host). |
|CreateTime |String |`2021-08-18 13:32:23` |The creation time of host group. |
|ModifyTime |String |`2021-08-18 13:32:23` |Time when the host group was modified. |
|HostGroupId |String |`0fd**********` |ID of the host group. |
|HostGroupName |String |`testname` |Name of the host group. |
|HostGroupType |String |`IP` |The type of host group.<br><br><br>* IP: Machine IP.<br><br>* Label: Host identification. |
|UpdateEndTime |String |"02:00" |LogCollector automatic upgrade end time. |
|HostIdentifier |String |`label` |Machine identifier. |
|IamProjectName |String |`default` |The IAM project to which the host group belongs. |
|ServiceLogging |Boolean |`true` |You can choose whether to enable the Logcollector service log.<br><br><br>* true: enable.<br><br>* false: (default) disable. |
|UpdateStartTime |String |"00:00" |LogCollector auto upgrade start time.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Only required when AutoUpdate is set to true.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For automatic upgrades, we recommend that you set it during off\-peak business hours. LogCollector may restart during the upgrade, but no logs will be lost.</div><br> |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
GET https://{tls-endpoint}/DescribeBoundHostGroups?&RuleId=faf6d529-e75e-457f-a23a-9c4203a6dff3xx&PageNumber=1&PageSize=20 HTTP/1.1
Content-Type: application/json
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
Content-Type: application/json; charset=utf-8
{
    "HostGroupInfos": [
        {
            "AutoUpdate": true,
            "CreateTime": "2021-08-18 13:32:23",
            "ModifyTime": "2021-08-18 13:32:23",
            "HostGroupId": "0fd**********",
            "HostGroupName": "testname",
            "HostGroupType": "IP",
            "UpdateEndTime": "02:00",
            "HostIdentifier": "label",
            "IamProjectName": "default",
            "ServiceLogging": true,
            "UpdateStartTime": "00:00"
        }
    ],
    "Total": 100
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Code

You can visit [Public error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes) for more information on error codes.
