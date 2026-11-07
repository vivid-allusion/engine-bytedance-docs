---
title: "ShopCardDataManager"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/ShopCardDataManager-zh-CN"
---

商品卡片数据的管理类。

<span id="54fa979e"></span>
## 成员函数

<span id="616fe6ee"></span>
### isProductFloating

检查指定商品卡片当前是否为商品浮窗。

```Java
boolean isProductFloating(Product product)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|product |[Product](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#0f642632) |待检查的商品。 |


**返回值**


|**类型** |**接口行为** |
|---|---|
|Boolean |指定商品卡片是否为商品浮窗。<br><br><br>* `true`：为商品浮窗。<br><br>* `false`：不是商品浮窗。 |


<span id="34555868"></span>
### getShopCardDatamap

获取当前商品卡片列表数据。

```Java
Map<String, ProductV2> getShopCardDatamap();
```


**返回值**


|**类型** |**接口行为** |
|---|---|
|Map<String, ProductV2\> |商品卡片数据映射表，键为菜单ID，值为对应的商品卡片数据。 |


<span id="028be9a7"></span>
### getFloatingShopCardItemModels

获取当前商品浮窗列表。

```Java
List<Product> getFloatingShopCardItemModels();
```


**返回值**


|**类型** |**接口行为** |
|---|---|
|List |商品浮窗项列表。 |


&nbsp;
