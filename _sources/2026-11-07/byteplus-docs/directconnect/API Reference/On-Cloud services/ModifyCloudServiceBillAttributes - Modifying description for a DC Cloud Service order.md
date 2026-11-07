---
title: "ModifyCloudServiceBillAttributes - Modifying description for a DC Cloud Service order"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/ModifyCloudServiceBillAttributes"
---

Call ModifyCloudServiceBillAttributes to modify the description of a Direct Connect (DC) Cloud Service order.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyCloudServiceBillAttributes&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">String</span> <span data-api-tag="require|d_PaeG">必选</span> `Example: ModifyCloudServiceBillAttributes`

The interface name. The current API name is `ModifyCloudServiceBillAttributes`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|iY9R3G">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**CloudServiceBillId** <span data-label="purple">String</span> <span data-api-tag="require|1iqoG7">必选</span> `Example: csb-x890skt8uch28hgu6lds9****`

The order ID of the DC Cloud Service to be modified.

You can call [DescribeCloudServiceBills](https://docs.byteplus.com/en/docs/directconnect/DescribeCloudServiceBills) to query the order ID of the DC Cloud Service.



**Description ** <span data-label="purple"> String  </span>`optional` `Example: This is a description.`

The description of the DC Cloud Service.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), spaces ( ), underscores (_), hyphens (\-), equals signs (=), commas (,), Chinese commas (，), and Chinese periods (。).

* Must be 0 to 255 characters.

* If left blank, the original configuration remains.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=ModifyCloudServiceBillAttributes&Version=2020-04-01&CloudServiceBillId=csb-x890skt8uch28hgu6lds9****&Description=This is a description. HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyCloudServiceBillAttributes",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-north-1"
    },
"Result": {
        "RequestId": "202111161611080102121461940900****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).
