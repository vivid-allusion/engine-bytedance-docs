---
title: "UpdateWafServiceControl"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/UpdateWafServiceControl"
---

Call the UpdateWafServiceControl interface to modify the protection policy and log service status of the specified domains.

<span id=".6K-35rGC6K-05piO"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=UpdateWafServiceControl&Version=2023\-12\-25


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

<span id="query"></span>
### Query



**Action** <span data-label="purple">string</span> <span data-api-tag="require|hzDDa2">必选</span> `Sample value: UpdateWafServiceControl`

The operation to be performed, values: UpdateWafServiceControl.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|o7iEU7">必选</span> `Sample value: 2023-12-25`

API version, value: 2023\-12\-25.



&nbsp;

<span id="body"></span>
### Body



**BotRepeatEnable** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

Whether to enable the bot statistics protection policy.


* 0: Disabled

* 1: Enabled



**AutoCCEnable** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

Whether to enable the intelligent rate limiting policy.


* 0: Disabled

* 1: Enabled



**BotSequenceEnable** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

Whether the bot behavior map is enabled.


* 0: Disabled

* 1: Enabled



**BotSequenceDefaultAction** <span data-label="purple">integer</span> `Optional` `Sample value: 0`

Set the default action for the bot behavior map policy, effective when BotSequenceEnable = 1. Default is 0 (Observe).


* 0: Observe

* 2: Block

* 6: JS Challenge

* 7: Human Verification



**BotFrequencyEnable** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

Whether to enable the bot rate limiting policy.


* 0: Disabled

* 1: Enabled



**BotDytokenEnable** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

Whether to enable bot dynamic tokens.


* 0: Disabled

* 1: Enabled



**Host** <span data-label="purple">string</span> <span data-api-tag="require|XsFDxA">必选</span> `Sample value: www.example.com`

Domain name to be updated.



**ProjectName** <span data-label="purple">string</span> `Optional` `Sample value: default`

The current project name associated with the resource. Refer to [ListDomain](https://docs.byteplus.com/en/docs/waf/ListDomain) for how to obtain the project name.



**WafEnable** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

Whether to enable the vulnerability protection policy.


* 0: Disabled

* 1: Enabled



**CcEnable** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

Whether to enable the rate limiting policy.


* 0: Disabled

* 1: Enabled



**WhiteEnable** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

Whether to enable the allowlist policy.


* 0: Disabled

* 1: Enabled



**BlackIpEnable** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

Whether to enable the blocklist policy.


* 0: Disabled

* 1: Enabled



**BlackLctEnable** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

Whether to enable the location access control policy.


* 0: Disabled

* 1: Enabled



**WafWhiteReqEnable** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

Whether to enable the request allowlist policy of vulnerability protection.


* 0: Disabled

* 1: Enabled



**WhiteFieldEnable** <span data-label="purple">integer</span> `Optional` `Example value: 1`

Whether to enable the field allowlist policy of vulnerability protection.


* 0: Disabled

* 1: Enabled



**CustomRspEnable** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

Whether to enable custom response block policy.


* 0: Disabled

* 1: Enabled



**SystemBotEnable** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

Whether to enable the managed bot classification policy.


* 0: Disabled

* 1: Enabled



**CustomBotEnable** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

Whether to enale the custom bot classification policy.


* 0: Disabled

* 1: Enabled



**ApiEnable** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

Whether to enbale the API protection policy.


* 0: Disabled

* 1: Enabled



**TamperProofEnable** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

Whether to enbale the Web tamper prevention policy.


* 0: Disabled

* 1: Enabled



**DlpEnable** <span data-label="purple">integer</span> `Optional` `Example value: 1`

Whether to enbale the sensitive information leakage prevention policy.


* 0: Disabled

* 1: Enabled



**TLSEnable** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

Whether to enable Torch Log Service.


* 0: Disabled

* 1: Enabled



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This interface does not have specific response parameters. 

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
POST /?Action=UpdateWafServiceControl&Version=2023-12-25 HTTP/1.1
Host: waf.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20241205T113710Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20241205/byteplus-global/waf/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "BotRepeatEnable": 1,
  "Host": "www.example.com"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20241205193720041155105037441FA1",
    "Action": "UpdateWafServiceControl",
    "Version": "2023-12-25",
    "Service": "waf",
    "Region": "byteplus-global"
  },
  "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can access [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) for more information about error codes.
