---
title: "ModifyHostGroupsAutoUpdate"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-modifyhostgroupsautoupdate"
---

Call the ModifyHostGroupsAutoUpdate interface to batch modify the LogCollector automatic upgrade configuration of the host group.

<span id="usage-notes"></span>
## Usage notes


* This interface is used for bulk modification of the LogCollector auto\-upgrade configuration of the host group, such as whether to enable auto\-upgrade, start and end time of the upgrade.


<span id="request-syntax"></span>
## Request syntax


* Request Method: **PUT**

* Request URL: **https://tls\-{Region}.bytepluses.com/ModifyHostGroupsAutoUpdate**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|HostGroupIds |Array of String |True |`["4be5e4e3-2a3a-48ba-80a8-4446d7d5****", "c701baeb-559d-46bb-a79d-0faa7b16****"]` |The list of the host groups. |
|AutoUpdate |Boolean |True |`true` |Whether the LogCollector installed on the host group servers has the auto\-upgrade feature enabled.<br><br><br>* true: Torch Log Service will check for upgrades during a designated time each day. If the conditions for an upgrade are met, LogCollector will automatically upgrade itself, eliminating the need for manual operation.<br><br>* false: (default) LogCollector does not auto\-upgrade. If you need to use a higher version of LogCollector, please refer to [Upgrade LogCollector](https://docs.byteplus.com/docs/tls/upgrade_logcollector_on_a_host) for operation.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only LogCollector V1.0.8 and subsequent versions support automatic upgrades.</div><br> |
|UpdateStartTime |String |False |`"00:00"` |The start time of LogCollector's automatic upgrade.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Only needs to be set when AutoUpdate is true.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The auto\-upgrade time is recommended to be set during off\-peak business hours. LogCollector may restart during the auto\-upgrade process, but no logs will be lost.</div><br> |
|UpdateEndTime |String |False |`"02:00"` |The end time of the automatic upgrade for LogCollector. |


<span id="responses"></span>
## Responses

There are no unique return parameters for this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).

<span id="sample-request"></span>
## Sample Request

```json
PUT https://tls-{Region}.bytepluses.com/ModifyHostGroupsAutoUpdate HTTP/1.1
Content-Type: application/json
{
    "HostGroupIds": [
        "4be5e4e3-2a3a-48ba-80a8-4446d7d5****",
        "c701baeb-559d-46bb-a79d-0faa7b16****"
    ],
    "AutoUpdate": true,
    "UpdateStartTime": "00:00",
    "UpdateEndTime": "02:00"
}
```


<span id="sample-response"></span>
## Sample Response

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```


<span id="error-code"></span>
## Error code

The following table lists the error codes related to the interface and business logic. For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |The parameter is invalid. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |


&nbsp;
