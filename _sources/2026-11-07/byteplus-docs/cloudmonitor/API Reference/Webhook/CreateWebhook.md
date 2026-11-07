---
title: "CreateWebhook"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/CreateWebhook"
---

Create an alert callback.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Cloud Monitor is deployed across multiple regions worldwide to deliver more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/cloudmonitor/Service_address) topic to choose an access point that is optimal for the region of your services.


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=CreateWebhook&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateWebhook&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |CreateWebhook |The name of the API. The API name is `CreateWebhook`. |
|Version |String |Yes |2018\-01\-01 |The API version. The current API version is `2018-01-01`. |
|Name |String |Yes |webhook\-demo |Webhook name.<br><br><br>* Its length must not exceed 512 bytes.<br><br>* Duplicate names are not allowed. |
|Type |String |Yes |lark |Webhook type. Values:<br><br><br>* **custom**: Custom Webhook<br><br>* **wecom**: WeCom Webhook<br><br>* **lark**: Feishu Webhook<br><br>* **dingtalk**: DingTalk Webhook |
|Url |String |Yes |https://open.larkoffice.com/open\-apis/bot/v2/hook/xxxx |Webhook address.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Enter a publicly accessible address that is not longer than 1000 bytes.</div><br> |
|Token |String |No |2131daxxxxx2das |The token used for Webhook authentication. Supported scenarios include:<br><br><br>* Being used as the signature verification key for Feishu or DingTalk.<br><br>* Being included in the request payload to report the defined Webhook content. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=CreateWebhook&Version=2018-01-01
Content-Type: application/json
{
    "Name": "webhook-demo",
    "Token": "2131daxxxxx2das",
    "Type": "lark",
    "Url": "https://open.larkoffice.com/open-apis/bot/v2/hook/xxxx",
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Data |Array of String |["155255269369\*\*\*\*\*\*"] |Webhook ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Env": "",
        "Action": "CreateWebhook",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": [
            ""
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).
