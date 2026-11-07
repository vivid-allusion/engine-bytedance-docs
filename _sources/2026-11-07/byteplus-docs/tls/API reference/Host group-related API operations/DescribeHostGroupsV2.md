---
title: "DescribeHostGroupsV2"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/DescribeHostGroupsV2"
---

Call the DescribeHostGroupsV2 API to retrieve all host group information, excluding group heartbeat status and the list of associated collection rules.

Supports paginated queries and fuzzy searches by host group name or host group ID, but only one criterion can be provided for each query.

<span id=".6K-35rGC6K-05piO"></span>
## Request instructions


* Request method: GET

* Request URL: https://{tls\-endpoint}/DescribeHostGroupsV2


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists request parameters specific to this API and some common parameters. For more information, see [Public parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="Query"></span>
### Query


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|HostGroupId |String |No |`6622a14b-770f-4171-a385-3b68486f****` |ID of the host group; supports fuzzy search. |
|HostGroupName |String |No |`mgn1` |Host group name; supports fuzzy search. |
|AutoUpdate |Boolean |No |true |Whether the auto upgrade feature is enabled.<br><br><br>* true: Enabled<br><br>* false: Disabled. |
|HostIdentifier |String |No |`test` |Host group identifier. |
|IamProjectName |String |No |default |The access control project name identifies the IAM project to which the host group belongs. The default value is `default`. |
|ServiceLogging |Boolean |No |true |Service log feature enabled.<br><br><br>* true: Enable<br><br>* false: Disable. |
|PageNumber |Integer |No |1 |Page number for pagination queries. Default is 1, meaning data will be returned starting from the first page. |
|PageSize |Integer |No |20 |Maximum number of host groups returned per page for pagination queries. Default value is `20`. |
|Hidden |Boolean |No |true |Hide host groups in dedicated resources<br><br><br>* `true`: Hide<br><br>* `false`: Do not hide |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Return parameters

The following table lists only the unique return parameters for this API. For more information, see [Return structure](https://docs.byteplus.com/en/docs/tls/response-message).


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|HostGroupHostsRulesInfos |Array of [HostGroupHostsRulesInfoV2](https://docs.byteplus.com/en/docs/38/83204#hostgrouphostsrulesinfov2) |/ |Host group information list. |
|Total |Integer |100 |Total number of eligible host groups |


<span id="hostgrouphostsrulesinfov2"></span>
### HostGroupHostsRulesInfoV2


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|HostGroupInfo |Object of [HostGroupInfo](https://docs.byteplus.com/en/docs/38/83204#hostgroupinfo) |/ |Host group information. |


<span id="hostgroupinfo"></span>
### HostGroupInfo


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|HostCount |Integer |`2` |Number of machines. |
|RuleCount |Integer |`1` |Number of bound collection configurations. |
|AutoUpdate |Boolean |`true` |LogCollector installed on the host group server has auto\-upgrade function. You can choose whether to enable it.<br><br><br>* true: TLS checks for upgrades during the specified period each day. If the conditions are met, LogCollector upgrades automatically without manual intervention.<br><br>* false: (default) LogCollector does not upgrade automatically. To use a newer version, refer to [Upgrade LogCollector](https://docs.byteplus.com/docs/tls/upgrade_logcollector_on_a_host). |
|CreateTime |String |`2021-08-18 13:32:23` |Host group creation time. |
|ModifyTime |String |`2021-08-18 13:32:23` |Host group modification time. |
|HostGroupId |String |`0fd**********` |Host group ID. |
|HostGroupName |String |`testname` |Name of the host group. |
|HostGroupType |String |`IP` |The type of host group.<br><br><br>* IP: Machine IP.<br><br>* Label: Host identification. |
|UpdateEndTime |String |"02:00" |End time of LogCollector auto upgrade. |
|HostIdentifier |String |`label` |Machine identifier. |
|IamProjectName |String |`default` |The IAM project to which the host group belongs. |
|ServiceLogging |Boolean |`true` |Enable Logcollector service log functionality.<br><br><br>* true: enabled.<br><br>* false: (default) disabled. |
|UpdateStartTime |String |"00:00" |Start time of LogCollector auto upgrade.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Required only when AutoUpdate is set to true.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For automatic upgrades, we recommend that you set it during off\-peak business hours. LogCollector may restart during the upgrade, but no logs will be lost.</div><br> |
|AgentLatestVersion |String |"2.3.4" |Latest version number of LogCollector released by TLS |
|NormalHeartbeatStatusCount |Integer |`1` |Number of machines with normal heartbeat. |
|AbnormalHeartbeatStatusCount |Integer |`1` |Number of machines with heartbeat anomalies. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
GET https://{tls-endpoint}/DescribeHostGroupsV2?&HostGroupId=6622a14b-770f-4171-a385-3b68486f****&HostGroupName=mgn1&AutoUpdate=true&HostIdentifier=test&IamProjectName=default&ServiceLogging=true&PageNumber=1&PageSize=20&Hidden=true HTTP/1.1
Content-Type: application/json
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
Content-Type: application/json; charset=utf-8
{
    "HostGroupHostsRulesInfos": [
        {
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
    ],
    "Total": 100
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Code

You can visit [Common Error Codes](https://docs.byteplus.com/en/docs/tls/common-error-codes) for more information.
