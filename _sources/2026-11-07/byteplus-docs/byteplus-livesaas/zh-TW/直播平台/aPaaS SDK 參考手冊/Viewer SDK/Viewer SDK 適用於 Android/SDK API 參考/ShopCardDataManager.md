---
title: "ShopCardDataManager"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/shopcarddatamanager-zh-TW"
---

商店卡片資料的管理類別。

<span id="54fa979e"></span>
## 成員函式

<span id="616fe6ee"></span>
### isProductFloating

檢查特定商品卡片目前是否為浮動商品卡片。

```Java
boolean isProductFloating(Product product)
```


**輸入參數**


|**名稱** |**型別** |**說明** |
|---|---|---|
|product |[Product](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#0f642632) |要檢查的商品。 |


**回傳值**


|**型別** |**說明** |
|---|---|
|Boolean |特定商品卡片是否為浮動商品卡片。<br><br><br>* `true`：為浮動商品卡片。<br><br>* `false`：不是浮動商品卡片。 |


<span id="34555868"></span>
### getShopCardDatamap

取得目前商店卡片列表資料。

```Java
Map<String, ProductV2> getShopCardDatamap();
```


**回傳值**


|**型別** |**說明** |
|---|---|
|Map<String, ProductV2\> |商店卡片資料映射表，鍵值為菜單 ID，值為對應的商店卡片資料。 |


<span id="028be9a7"></span>
### getFloatingShopCardItemModels

取得目前浮動商店卡片列表。

```Java
List<Product> getFloatingShopCardItemModels();
```


**回傳值**


|**型別** |**說明** |
|---|---|
|List |浮動商店卡片項目列表。 |


&nbsp;
