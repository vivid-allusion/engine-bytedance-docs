---
title: "GetActivityProductAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getactivityproductapi"
---

Call this API to retrieve the configurations of product cards displayed in a specific live room.

<span id="Request"></span>
## Requirement

Quota: 120 queries per minute per account

<span id="ecda79a5"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=GetActivityProductAPI&Version=2020-06-01`

* Method: GET


<span id="8387d019"></span>
## Request parameters

Not all shared request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="Query string parameters"></span>
### Query


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetActivityProductAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Long |Yes |`1783981136301234` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |


<span id="Sample request"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|`-` |JSON Map |`-` |A JSON map where keys are the sequence numbers of product card menus and values are the corresponding configurations. Format: `"Key":"Value"`.<br><br><br>* `"Key"`: The sequence number of the menu for product cards, which is the same as the `Location` value from the [GetActivityMenuAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitymenuapi) response. For example, if the `Location` value is `1` for the menu for product cards, then the `"Key"` value is `1`.<br><br>* `"Value"`: Configurations of product cards. For more information, see [ProductConfig](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityproductapi#d514de4f). |


<span id="d514de4f"></span>
### ProductConfig


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|EnableFloating |Boolean |`false` |Indicates whether a floating page is opened in the live room to display the product details page after viewers click a product card.<br><br><br>* `true`: Displays the product details page on a floating page in the live room. Viewers can watch the video and view the product details page at the same time. This configuration takes effect only on mobile devices.<br><br>* `false`: Displays the product details page on a new page. Viewers cannot watch the video and view the product details page at the same time. |
|EnableUA |Boolean |`false` |Indicates whether the direct URL feature is enabled. This feature is only available on mobile devices.<br><br><br>* `true`: Enabled.<br><br>* `false`: Disabled. |
|UAAddress |String |`Mozilla` |Specifies a User\-Agent string for matching specific client environments.<br><br>When a viewer clicks a product card on a platform where the User Agent contains the parameter value, the viewer will be redirected to the direct URL of the product card.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter takes effect only when <code>EnableUA</code> is <code>true</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If both <code>UAAddress</code> and <code>UAInfo.UAAddress</code> have values, <code>UAInfo.UAAddress</code> takes effect.</div><br> |
|UAInfo |Array of [UAInfoMsg](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityproductapi#e22e1601) |`-` |The list of environments configured for the direct URL feature. Up to 5 environments can be configured. The order of the environments corresponds to the order of the URLs in the `DirectUrls` parameter of each product card.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter takes effect only when <code>EnableUA</code> is <code>true</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If both <code>UAAddress</code> and <code>UAInfo.UAAddress</code> have values, <code>UAInfo.UAAddress</code> takes effect.</div><br> |
|ProductsPosition |Integer |`0` |Indicates where the floating product card is displayed on the desktop viewing page.<br><br><br>* `0`: In the upper\-right corner of the player.<br><br>* `1`: In the upper\-left corner of the player.<br><br>* `2`: In the lower\-left corner of the player.<br><br>* `3`: In the lower\-right corner of the player. |
|DefaultRedirectImage |String |`www.example.com` |The URL of the default button image, which corresponds to the **Button image** field on the console. |
|Product |Array of [Product](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityproductapi#0a61e327) |`-` |The configurations of product cards. |


<span id="e22e1601"></span>
#### UAInfoMsg


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|UAName |String |`Env1` |The name of the environment, which corresponds to the environment name configured in the **User Agent for specific environments** field on the console.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Legacy single\-environment configurations are named <code>Env1</code>.</div><br> |
|UAAddress |String |`Mozilla/5.0 (env1)` |The User\-Agent string of the environment. When a viewer clicks a product card on a platform where the User Agent contains this value, the viewer will be redirected to the corresponding direct URL of the product card. |


<span id="0a61e327"></span>
#### Product


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|Title |String |`Dress` |The name of your product, which corresponds to the **Product name** field on the console. |
|Highlight |String |`800` |The retail price of your product, which corresponds to the **Retail price** field on the console. |
|IntroduceImage |String |`www.example.com` |The URL of the product image, which corresponds to the **Product image** field on the console. The image is displayed on the left of the product card. |
|RedirectImage |String |`www.example.com` |The URL of the button image, which corresponds to the **Button image** field on the console. The image is displayed in the lower\-right corner of the product card. Viewers will be redirected to the product URL or direct URL after clicking the button. |
|RedirectUrl |String |`www.example.com` |The URL of the product details page, which corresponds to the **Product URL** field on the console. |
|Index |Integer |`-` |Deprecated. |
|Id |Long |`20867` |The ID of the product card. |
|EnableStatus |Integer |`1` |Indicates whether the product card is listed.<br><br><br>* `0`: Unlisted.<br><br>* `1`: Listed. |
|Remark |String |`7-day unconditional return policy` |The additional information of your product, such as the clothing size. This parameter corresponds to the **Product description** field on the console. |
|Strikethrough |String |`1000` |The list price of your product, which corresponds to the **List price** field on the console. |
|DirectUrl |String |`www.example.com` |The direct URL of the product details page, which corresponds to the **Direct URL** field on the console.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter returns only the direct URL of the first environment. To get the direct URLs of all configured environments, use <code>DirectUrls</code>.</div><br> |
|DirectUrls |Array of String |`["https://www.direct_url1", "", "https://www.direct_url3"]` |The direct URLs of the product details page, which correspond to the **Direct URL** fields on the console.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter has a value only when <code>EnableUA</code> is <code>true</code>. It returns up to 5 direct URLs, one for each environment in the <code>UAInfo</code> list, in the same order as the configured environments.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Empty positions are returned as empty strings to preserve alignment with <code>UAInfo</code>.</div><br> |
|FloatingStatus |Integer |`1` |Indicates whether the product card is displayed in a floating window.<br><br><br>* `1`: Displayed in a floating window.<br><br>* Other values: Not displayed in a floating window. |
|TagName |String |`Clothing` |The product category, which corresponds to the **Product category** field on the console. |
|ExternalProductId |String |`20866` |The external product ID. This ID prevents the same product from being added to the product card menu more than once. |


<span id="20349dad"></span>
## Samples

<span id="3675694e"></span>
### Sample request

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetActivityProductAPI&Version=2020-06-01&ActivityId=1783981136301234
```


<span id="39032423"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "GetActivityProductAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1708786019
    },
    "Result": {
        "1": {
            "EnableFloating": false,
            "Product": [
                {
                    "Title": "Dress",
                    "Highlight": "800",
                    "IntroduceImage": "www.example.com",
                    "RedirectImage": "www.example.com",
                    "RedirectUrl": "www.example.com",
                    "Index": 0,
                    "Id": 20867,
                    "EnableStatus": 1,
                    "Strikethrough": "1000",
                    "DirectUrl": "www.example.com/env1/dress",
                    "DirectUrls": [
                        "www.example.com/env1/dress",
                        "www.example.com/env2/dress"
                    ],
                    "Remark": "7-day unconditional return policy",
                    "FloatingStatus": 1,                    
                    "TagName": "Clothing",
                    "ExternalProductId": "20866"
                }
            ],
            "EnableUA": true,
            "UAAddress": "Mozilla/5.0 (env1)",
            "UAInfo": [
                {
                    "UAName": "Env1",
                    "UAAddress": "Mozilla/5.0 (env1)"
                },
                {
                    "UAName": "Env2",
                    "UAAddress": "Mozilla/5.0 (env2)"
                }
            ],
            "ProductsPosition": 0,
            "DefaultRedirectImage": ""            
        }
    }
}
```


<span id="35b66db0"></span>
## Error codes

For a list of shared error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
