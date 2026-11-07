---
title: "ExplainProduct"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/explainproduct"
---

Pins a product to the top of the menu and displays it in a floating window on the viewing page, or restores the product to its original position under the menu and removes it from the floating window display on the viewing page.

<span id="requirements"></span>
## Requirements

Rate limit: 120 requests per minute per account

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://livesaas.byteplusapi.com/?Action=ExplainProduct&Version=2023\-08\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ExplainProduct` |API operation. |
|Version |String |Yes |`2023-08-01` |The version of this API operation. Current version: `2023-08-01`. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|ActivityId |Long |Yes |`17791****71580` |The activity ID of the live room. You can call [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) to get the ID from the response parameter `Id`. |
|ExplainStatus |Integer |Yes |`1` |The operation to perform on the product. Valid values:<br><br><br>* `1`: Pin the product to the top of the menu and display it in a floating window on the viewing page.<br><br>* `2`: Restore the product to its original position under the menu and remove it from the floating window display on the viewing page. |
|ProductId |Long |No |`49**46` |The ID of the product card. You can call [GetActivityProductAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getactivityproductapi) to get the ID from the response parameter `Id`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Pass either <code>ProductId</code> or <code>ExternalProductId</code>. If both are passed, only the <code>ProductId</code> takes effect.</div><br> |
|ExternalProductId |String |No |`your_product_id_12345` |The external product ID, which is unique in each menu for product cards. You can get the ID by calling [GetActivityProductAPI](https://docs.byteplus.com/zh-CN/docs/byteplus-livesaas/docs-getactivityproductapi).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Pass either <code>ProductId</code> or <code>ExternalProductId</code>. If both are passed, only the <code>ProductId</code> takes effect.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you have more than one product with this ID in your live room, the operation will be performed on the product under the leftmost menu for product cards.</div><br> |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Status |Boolean |`true` |Indicates whether the operation is successfully performed. Valid values:<br><br><br>* `true`: Successful.<br><br>* `false`: Failed. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://livesaas.byteplusapi.com/?Action=ExplainProduct&Version=2023-08-01
{
    "ExplainStatus": 1,
    "ActivityId": 17791****71580,
    "ProductId": 49**46,
    "ExternalProductId": "your_product_id_12345"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ExplainProduct",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "Status": true
    }
}
```


<span id="error-codes"></span>
## Error codes

For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).

&nbsp;
