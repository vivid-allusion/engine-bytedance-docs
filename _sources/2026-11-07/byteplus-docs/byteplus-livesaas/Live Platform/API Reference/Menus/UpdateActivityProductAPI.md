---
title: "UpdateActivityProductAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updateactivityproductapi"
---

Call this API to update the configurations of product cards in a live room.

<span id="Request"></span>
## Requirement

Quota: 120 queries per minute per account

<span id="36bded50"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=UpdateActivityProductAPI&Version=2020-06-01`

* Method: POST


<span id="53aa7d97"></span>
## Request parameters

Not all shared request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="f145b498"></span>
### Query


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateActivityProductAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |


<span id="8cd6fc93"></span>
### Body


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|ActivityId |Long |Yes |`1783981136301234` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|Products |Array of [Products](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivityproductapi#a460b55a) |Yes |`-` |The configurations of product cards. |


<span id="a460b55a"></span>
#### Products


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|`-` |JSON Map |Yes |`-` |The sequence number of the menu for product cards and configurations of product cards. Format: `"Key":"Value"`.<br><br><br>* `"Key"`: The sequence number of the menu for product cards. Get the sequence number by calling [GetActivityMenuAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitymenuapi). For example, if the `GetActivityMenuAPI` response returns a `Location` of `1` for the product card menu, use `"1"` as the `"Key"`.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Ensure this location corresponds to a product card menu, for which the <code>Type</code> value in the <code>GetActivityMenuAPI</code> response is <code>2</code>.   </div><br>   <br><br>* `"Value"`: Configurations of product cards. For more information, see [ProductConfig](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivityproductapi#993adfaa). |


<span id="993adfaa"></span>
##### **ProductConfig**


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|EnableFloating |Boolean |Yes |`false` |Specifies whether to display the product details page on a floating page in the live room after a viewer clicks a product card.<br><br>Valid values:<br><br><br>* `true`: Yes. Display the product details page on a floating page in the live room. Viewers can watch the video and view the product details page at the same time. This configuration takes effect only on mobile devices.<br><br>* `false`: No. Display the product details page on a new page. Viewers cannot watch the video and view the product details page at the same time. |
|EnableUA |Boolean |No |`false` |Specifies whether to enable the direct URL feature. This feature is only available on mobile devices.<br><br>Default value: `false`.<br><br>Valid values:<br><br><br>* `true`: Enables the feature.<br><br>* `false`: Disables the feature. |
|UAAddress |String |No |`Mozilla` |The User Agent for specific environments.<br><br>When a viewer clicks a product card on a platform where the User Agent contains the parameter value, the viewer will be redirected to the direct URL of the product card. However, if a viewer clicks the product card on other platforms, the viewer is redirected to the product URL (RedirectUrl).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter configures only a single environment and is retained for backward compatibility. To configure up to 5 environments, use <code>UAInfo</code> instead.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is required if <code>EnableUA</code> is <code>true</code> and <code>UAInfo</code> is not passed. If both are passed, <code>UAInfo</code> takes precedence.</div><br> |
|UAInfo |Array of [UAInfoMsg](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivityproductapi#3a35fa91) |No |`-` |The list of environments for the direct URL feature. You can configure up to 5 environments. The order of the environments must correspond to the order of the URLs in the `DirectUrls` parameter of each product card.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required if <code>EnableUA</code> is <code>true</code> and <code>UAAddress</code> is not passed. If both are passed, <code>UAInfo</code> takes precedence.</div><br> |
|ProductsPosition |Integer |No |`0` |Specifies where the floating product card is displayed on the viewing page for PCs.<br><br>Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: In the upper\-right corner of the player.<br><br>* `1`: In the upper\-left corner of the player.<br><br>* `2`: In the lower\-left corner of the player.<br><br>* `3`: In the lower\-right corner of the player. |
|DefaultRedirectImage |String |No |`https://example.com` |The URL of the default button image, which corresponds to the **Button image** field on the console.<br><br>The image must be in JPG, GIF, PNG, or BMP format and replaces the default system image. The recommended resolution is 160×60. |
|Product |Array of [Product](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivityproductapi#Product) |Yes |`-` |The configurations of product cards. |


<span id="3a35fa91"></span>
###### **UAInfoMsg**


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|UAName |String |Yes |`TikTokiOSEnv1` |The name of the environment, up to 20 characters. This name labels the corresponding direct URL when you configure product cards. |
|UAAddress |String |Yes |`TikTok` |The User Agent string of the environment, up to 500 characters. When a viewer clicks a product card on a platform where the User Agent contains this value, the viewer will be redirected to the corresponding direct URL of the product card. |


<span id="244cef61"></span>
###### **Product**


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Title |String |Yes |`Dress` |The name of your product, which corresponds to the **Product name** field on the console.<br><br>The value must be 1\-3315 characters in length. |
|Highlight |String |No |`800` |The retail price of your product, which corresponds to the **Retail price** field on the console.<br><br>The value must be 1\-260 characters in length. |
|IntroduceImage |String |No |`www.example.com` |The URL of the product image, which corresponds to the **Product image** field on the console. The image is displayed on the left of the product card.<br><br>Supported formats for the product image: JPG, GIF, PNG, and BMP. |
|RedirectImage |String |No |`www.example.com` |The URL of the button image, which corresponds to the **Button image** field on the console. The image is displayed in the lower\-right corner of the product card. Viewers will be redirected to the product URL or direct URL after clicking the button.<br><br>Supported formats for the button image: JPG, GIF, PNG, and BMP. |
|RedirectUrl |String |No |`www.example.com` |The URL of the product details page, which corresponds to the **Product URL** field on the console. |
|Index |Integer |No |`-` |Deprecated. |
|Id |Long |No |`-` |Deprecated. |
|EnableStatus |Integer |No |`1` |Specifies whether to list the product card. Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: The product card is not listed.<br><br>* `1`: The product card is listed. |
|DirectUrl |String |No |`www.example.com` |The direct URL of the product details page, which corresponds to the **Direct URL** field on the console.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The direct URL only takes effect if the value of <code>EnableUA</code> is <code>true</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter sets only the direct URL of the first environment and is retained for backward compatibility. To set a direct URL for each environment, use <code>DirectUrls</code> instead.</div><br> |
|DirectUrls |Array of String |No |`["www.example.com"]` |The direct URLs of the product details page, which correspond to the direct URL configuration items of the menu (`UAInfo`).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The direct URLs only take effect if the value of <code>EnableUA</code> is <code>true</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The number of <code>DirectUrls</code> should match the number of <code>UAInfo</code> environments:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the number of <code>DirectUrls</code> is greater than the number of <code>UAInfo</code> environments, the extra URLs do not take effect. For example, if you configured 2 UA environments and pass <code>["https://direct_url1", "https://direct_url2", "https://direct_url3"]</code>, then <code>https://direct_url3</code> does not take effect.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the number of <code>DirectUrls</code> is fewer than the number of <code>UAInfo</code> environments, the missing positions are padded with empty strings. For example, if you configured 2 UA environments and pass <code>["https://direct_url1"]</code>, then the direct URL for UA1 is <code>https://direct_url1</code> and the direct URL for UA2 is empty (<code>""</code>).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you do not want to configure a direct URL for a specific UA environment, pass <code>""</code> for the corresponding position. For example, if environments 1 and 3 need a direct URL but environment 2 does not, pass <code>["https://direct_url1", "", "https://direct_url3"]</code>.</div><br> |
|Remark |String |No |`XL` |Additional information about your product, such as clothing size. This parameter corresponds to the **Product description** field on the console.<br><br>The value must be 1\-3315 characters in length. |
|Strikethrough |String |No |`1000` |The list price of your product, which corresponds to the **List price** field on the console.<br><br>The value must be 1\-260 characters in length. |
|TagName |String |No |`Clothing` |The product category, which corresponds to the **Product category** field on the console.<br><br>The value must be 1\-20 characters in length. |
|ExternalProductId |String |No |`20866` |The external product ID. This ID prevents the same product from being added to the same product card menu more than once.<br><br>The value must be 1\-128 characters in length. |


<span id="d57c9da0"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|Status |Boolean |`true` |Indicates whether the product cards were updated successfully.<br><br><br>* `true`: Successful.<br><br>* `false`: Failed. |


<span id="8865deac"></span>
## Samples

<span id="c6eb5b80"></span>
### Sample request

```JSON
POST https://livesaas.byteplusapi.com/?Action=UpdateActivityProductAPI&Version=2020-06-01
{
     "ActivityId":1783981136301234,
     "Products":{
         "1":{
             "EnableFloating":false,
             "EnableUA":true,
             "UAInfo":[
                {
                     "UAName":"MozillaEnv1",
                     "UAAddress":"Mozilla/5.0 (env1)"
                },
                {
                     "UAName":"MozillaEnv2",
                     "UAAddress":"Mozilla/5.0 (env2)"
                }
             ],
             "ProductsPosition":0, 
             "DefaultRedirectImage":"https://example.com",
             "Product":[
                {
                     "Title":"Dress", 
                     "Highlight":"800", 
                     "IntroduceImage":"www.example.com", 
                     "RedirectImage":"www.example.com", 
                     "RedirectUrl":"www.example.com", 
                     "EnableStatus":1,
                     "DirectUrls":[
                        "www.example.com/env1/dress",
                        "www.example.com/env2/dress"
                     ],
                     "Remark":"XL",
                     "Strikethrough":"1000",
                     "TagName":"Clothing",
                     "ExternalProductId": "20866"
                }
            ]
        }
    }
}
```


<span id="da670bbe"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "UpdateActivityProductAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1708782797
    },
    "Result": {
        "Status": true
    }
}
```


<span id="f0c323f3"></span>
## Error codes

For a list of shared error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
