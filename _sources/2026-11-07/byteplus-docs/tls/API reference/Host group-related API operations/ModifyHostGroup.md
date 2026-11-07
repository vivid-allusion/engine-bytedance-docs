---
title: "ModifyHostGroup"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-modifyhostgroup"
---

Call the ModifyHostGroup interface to modify the host group.

<span id="usage-notes"></span>
## Usage notes

The call frequency limit is 20 times/s, and exceeding the frequency limit will report an error ExceedQPSLimit.

<span id="request-syntax"></span>
## Request syntax


* Request Method: **PUT**

* Request URL: **https://tls\-{Region}.bytepluses.com/ModifyHostGroup**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|HostGroupId |String |True |`0f********` |The ID of the host group. |
|HostGroupName |String |False |`mgn1` |The name of the host group. Please refer to the [Resource Naming limit](https://docs.byteplus.com/docs/tls/Limits#resource-naming-limit) for the naming rules. |
|HostGroupType |String |False |`IP` |The types of the host groups. Including:<br><br><br>* IP: The IP address of the host. At this point, you need to set the IP address list through the `HostIpList` parameter.<br><br>* Label: The custom identifier. At this point, you need to set the custom identifier through the `HostIdentifier` parameter. |
|HostIpList |Array of String |False |`["192.168.0.1", "127.0.0.1"]` |The list of the host IP addresses.<br><br>Required when `HostGroupType` is `IP`. |
|HostIdentifier |String |False |`hostlable` |The custom identifier.<br><br>Required when `HostGroupType` is `Label`. |
|AutoUpdate |Boolean |False |`true` |Whether the LogCollector installed on the host group servers has the auto\-upgrade feature enabled.<br><br><br>* true: Torch Log Service will check for upgrades during a designated time each day. If the conditions for an upgrade are met, LogCollector will automatically upgrade itself, eliminating the need for manual operation.<br><br>* false: (default) LogCollector does not auto\-upgrade. If you need to use a higher version of LogCollector, please refer to [Upgrade LogCollector](https://docs.byteplus.com/docs/tls/upgrade_logcollector_on_a_host) for operation.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only LogCollector V1.0.8 and subsequent versions support automatic upgrades.</div><br> |
|UpdateStartTime |String |False |`"00:00"` |The start time of LogCollector automatic upgrade.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Only needs to be set when AutoUpdate is true.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The automatic upgrade time is recommended to be set during the off\-peak period of the business. LogCollector may be restarted during the automatic upgrade process, but logs will not be lost.</div><br> |
|UpdateEndTime |String |False |`"02:00"` |The end time of the automatic upgrade for LogCollector. |
|ServiceLogging |Boolean |False |`true` |Whether to enable the Logcollector service log function.<br><br><br>* true: Enable<br><br>* false: (Default) Disable. |


<span id="responses"></span>
## Responses

There are no unique return parameters for this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).

<span id="sample-request"></span>
## Sample Request

```json
PUT https://tls-{Region}.bytepluses.com/ModifyHostGroup HTTP/1.1
Content-Type: application/json
{
    "HostGroupId": "662**********",
    "HostGroupName": "mgn1",
    "HostGroupType": "IP",
    "HostIpList": [
        "192.168.0.1",
        "127.0.0.1"
    ],
    "AutoUpdate": true,
    "UpdateStartTime": "00:00",
    "UpdateEndTime": "02:00",
    "ServiceLogging": true
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
|400 |HostIpQuotaExceed |Host Ip Quota Exceeded |Exceeded host IP limit. |
|404 |HostGroupNotExist |HostGroup %s does not exist |The host group does not exist. |
|409 |HostIdentifierAlreadyExist |HostIdentifier %s already exist |The identifier already exists. |
|409 |HostGroupAlreadyExist |HostGroup %s already exist |The host group already exists. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |


&nbsp;
