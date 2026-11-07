---
title: "DescribeIPAccessRule"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeipaccessrule-zh-TW"
---

查詢指定網域名稱空間的 IP 封鎖清單或允許清單。

<span id="07d60fcc"></span>
## 請求

<span id="3eb268f1"></span>
### 詳細資訊


* API 操作：`DescribeIPAccessRule`

* 請求方法：**POST**

* 請求 URL：https://open.byteplusapi.com/?Action=DescribeIPAccessRule&Version=2023\-01\-01

* 配額：每個帳戶每秒最多 10 次查詢


<span id="0c94222a"></span>
### **查詢字串參數**

下表並未包含所有公開參數。完整列表請參見[公開參數](https://docs.byteplus.com/byteplus-media-live/docs/calling-byteplus-medialive-openapi#Common%20request%20parameters)。


|**參數** |**必填** |**資料型別** |**說明** |
|---|---|---|---|
|Action |是 |字串 |API 操作。 |
|Version |是 |字串 |此 API 操作的版本。目前版本：`2023-01-01`。 |


<span id="be600f30"></span>
### Body 參數


|**參數** |**必填** |**資料型別** |**說明** |
|---|---|---|---|
|Vhost |是 |字串 |[網域名稱空間](https://docs.byteplus.com/en/byteplus-media-live/docs/glossary#Vhost)。 |
|Domain |是 |字串 |網域名稱。 |


<span id="4e7cf17f"></span>
### 範例請求

```JSON
POST https://open.byteplusapi.com?Action=DescribeIPAccessRule&Version=2023-01-01
{
    "Vhost": "example",
    "Domain": "example.com"
}
```


<span id="3238ad86"></span>
## 回應

<span id="b1276522"></span>
### 回應結構


|**參數** |**資料型別** |**說明** |
|---|---|---|
|AccessRuleLists |陣列<[AccessRuleLists](https://docs.byteplus.com/docs/byteplus-media-live/docs-describeipaccessrule#f67e0c26)\> |IP 限制規則。 |


<span id="f67e0c26"></span>
#### AccessRuleLists


|**參數** |**資料型別** |**說明** |
|---|---|---|
|Vhost |字串 |網域名稱空間。 |
|Domain |字串 |網域名稱。 |
|IPAccessRule |[IPAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-describeipaccessrule#fcd9863b) |IP 限制規則。 |


<span id="fcd9863b"></span>
#### IPAccessRule


|**參數** |**資料型別** |**說明** |
|---|---|---|
|Type |字串 |存取規則的類型。有效選項包括：<br><br><br>* `allow`：允許清單。僅允許來自允許清單中 IP 位址的請求存取資源。<br><br>* `deny`：封鎖清單。來自封鎖清單中 IP 位址的請求無法存取資源。 |
|Enable |布林值 |配置是否啟用。<br><br><br>* `true`：配置已啟用。<br><br>* `false`：配置已停用。 |
|IPList |陣列 |允許清單或封鎖清單中的 IP 位址列表。 |


<span id="92ffb89a"></span>
### 範例回應

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202306041104200100100232280022D31",
        "Action": "DescribeIPAccessRule",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "IPAccessRuleLists": [
            {
                "Vhost": "example",
                "Domain": "example.com"
                "IPAccessRule": {
                    "Type": "deny",
                    "Enable": true,
                    "IpList": [
                    "192.168.1.1", 
                    "192.168.1.2"
                    ]
                }
            }
        ]
    }
}
```
