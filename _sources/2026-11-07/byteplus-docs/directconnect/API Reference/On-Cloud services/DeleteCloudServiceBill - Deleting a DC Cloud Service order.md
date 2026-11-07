---
title: "DeleteCloudServiceBill - Deleting a DC Cloud Service order"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DeleteCloudServiceBill"
---

Call DeleteCloudServiceBill to delete a Direct Connect (DC) Cloud Service order.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Only DC Cloud Service orders in the following statuses can be deleted: **Reviewing**, **Review disapproved, Pending payment, or Suspended**. You can call [DescribeCloudServiceBills](https://docs.byteplus.com/en/docs/directconnect/DescribeCloudServiceBills) to query the order status.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteCloudServiceBill&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String </span><span data-api-tag="require|A2Adug">必选</span> `Example value: DeleteCloudServiceBill`

The interface name. The current API name is `DeleteCloudServiceBill`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|M0WvvP">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**CloudServiceBillId ** <span data-label="purple"> String  </span><span data-api-tag="require|G4dwuY">必选</span> `Example: csb-x890skt8uch28hgu6lds9****`

The order ID of the DC Cloud Service to be deleted.

You can use [DescribeCloudServiceBills](https://docs.byteplus.com/en/docs/directconnect/DescribeCloudServiceBills) to query the order ID of the DC Cloud Service.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DeleteCloudServiceBill&Version=2020-04-01&CloudServiceBillId=csb-x890skt8uch28hgu6lds9**** HTTP/1.1
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
        "Action": "DeleteCloudServiceBill",
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
