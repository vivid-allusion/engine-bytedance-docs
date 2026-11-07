---
title: "DescribeHostGroupV2"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/DescribeHostGroupV2"
---

Call the DescribeHostGroupV2 API to obtain host group information, excluding host group heartbeat details and the list of associated collection rules.

<span id=".6K-35rGC6K-05piO"></span>
## Request instructions


* Request method: GET

* Request URL: https://{tls\-endpoint}/DescribeHostGroupV2


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters unique to this API and some common parameters. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="Query"></span>
### Query


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|HostGroupId |String |Yes |`"c7e0e442-19bf-4fb3-b547-5992fb8b****"` |Host group ID. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following table only lists response parameters unique to this API. For more information, see [Response Structure](https://docs.byteplus.com/en/docs/tls/response-message).


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|HostGroupHostsRulesInfo |Object of [HostGroupHostsRulesInfoV2](https://docs.byteplus.com/en/docs/38/83203#hostgrouphostsrulesinfov2) |/ |Host group information list. |


<span id="hostgrouphostsrulesinfov2"></span>
### HostGroupHostsRulesInfoV2


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|HostGroupInfo |Object of [HostGroupInfo](https://docs.byteplus.com/en/docs/38/83203#hostgroupinfo) |/ |Host group information. |


<span id="hostgroupinfo"></span>
### HostGroupInfo


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|HostCount |Integer |`2` |Number of machines. |
|RuleCount |Integer |`1` |The number of bound collection configurations. |
|AutoUpdate |Boolean |`true` |LogCollector installed on the host group server has auto\-upgrade function. You can choose whether to enable it.<br><br><br>* true: TLS checks for upgrades during the specified time period each day. If the upgrade conditions are met, LogCollector is updated automatically without manual intervention.<br><br>* false: (Default) LogCollector does not upgrade automatically. To use a higher version, refer to [Upgrade LogCollector](https://docs.byteplus.com/docs/tls/upgrade_logcollector_on_a_host). |
|CreateTime |String |`2021-08-18 13:32:23` |The creation time of the host group. |
|ModifyTime |String |`2021-08-18 13:32:23` |Time when the host group was modified. |
|HostGroupId |String |`0fd**********` |ID of the host group. |
|HostGroupName |String |`testname` |Name of the host group. |
|HostGroupType |String |`IP` |The type of host group.<br><br><br>* IP: Machine IP.<br><br>* Label: Host identification. |
|UpdateEndTime |String |"02:00" |LogCollector automatic upgrade end time. |
|HostIdentifier |String |`label` |Identifier of the machine. |
|IamProjectName |String |`default` |The IAM project to which the host group belongs. |
|ServiceLogging |Boolean |`true` |Enable Logcollector service log feature.<br><br><br>* true: Enabled.<br><br>* false: (default) Disabled. |
|UpdateStartTime |String |"00:00" |LogCollector automatic upgrade start time.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Only required when AutoUpdate is set to true.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For automatic upgrades, we recommend setting the upgrade time during off\-peak business hours. LogCollector may restart during the upgrade, but no logs will be lost.</div><br> |
|AgentLatestVersion |String |"2.3.4" |The latest version number of LogCollector released by TLS. |
|NormalHeartbeatStatusCount |Integer |`1` |Number of machines with normal heartbeat. |
|AbnormalHeartbeatStatusCount |Integer |`1` |Number of machines with heartbeat exceptions. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
GET https://{tls-endpoint}/DescribeHostGroupV2?&HostGroupId="c7e0e442-19bf-4fb3-b547-5992fb8b****" HTTP/1.1
Content-Type: application/json
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
Content-Type: application/json; charset=utf-8
{
    "HostGroupHostsRulesInfo": {
        "HostGroupInfo": {
            "HostCount": 2,
            "RuleCount": 1,
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
            "UpdateStartTime": "00:00",
            "AgentLatestVersion": "2.3.4",
            "NormalHeartbeatStatusCount": 1,
            "AbnormalHeartbeatStatusCount": 1
        }
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Code

You can visit [Public Error Codes](https://docs.byteplus.com/en/docs/tls/common-error-codes) for more details on error codes.
