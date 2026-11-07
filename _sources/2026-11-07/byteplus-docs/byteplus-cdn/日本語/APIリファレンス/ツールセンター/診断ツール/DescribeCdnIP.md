---
title: "DescribeCdnIP"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnIP_jp"
---

指定された1つまたは複数のIPアドレスがBytePlus CDNノードのIPアドレスであるかどうかを照会します。CDNノードにはエッジノードとリージョナルノードが含まれます。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20個のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=DescribeCdnIP&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDescribeCdnIPです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|IPs |String[] |はい |照会対象のIPアドレスリストを示します。リストには最大50個のIPアドレスを含めることができます。 |`["xx.xxx.xxx.102", "xxx.xxx.234.67"]`<br><br> |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|IPs |Object[] |リクエストパラメータ内のIPアドレスリストを示します。 | |
|IP |String |IPアドレスリスト内の1つのIPアドレスを示します。 |`xx.xxx.xxx.102`<br><br> |
|CdnIp |Boolean |該当IPアドレスが特定のCDNエッジノードのIPアドレスであるかどうかを示します。このパラメータには以下の値があります：<br><br>true：該当IPアドレスが特定のCDNエッジノードのIPアドレスであることを示します。<br><br>false：該当IPアドレスがいかなるCDNエッジノードのIPアドレスでもないことを示します。 |`false` |
|ISP |String |該当IPアドレスが属するネットワーク事業者（ISP）を示します。<br><br><br>* `CdnIp`が`false`の場合、このパラメータの値は空（""）です。<br><br>* `CdnIp`が`true`であるが、CDNが該当IPアドレスの属するネットワーク事業者を取得できない場合、このパラメータの値は`DEFAULT`です。 |`DEFAULT` |
|Location |String |該当IPアドレスが属する国または地域を示します。`CdnIp`が`false`の場合、このパラメータの値は空（""）です。<br><br>中国本土に属するIPアドレスの場合：<br><br><br>* 属する市が直轄市の場合、`Location`は区まで正確に示されます。<br><br>* 属する市が直轄市でない場合、`Location`は市まで正確に示されます。 |`United States-Florida-Florida` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeCdnIP&Version=2021-03-01
{
    "IPs": [
        "xxx.xxx.xx.139",
        "xxx.xx.xx.34"
    ]
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "2024101011033668CF51ECED9C5477E3C6",
        "Action": "DescribeCdnIP",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "IPs": [
            {
                "CdnIp": true,
                "IP": "xxx.xxx.xx.139",
                "ISP": "DEFAULT",
                "Location": "Singapore-Singapore-Singapore"
            },
            {
                "CdnIp": false,
                "IP": "xxx.xx.xx.34",
                "ISP": "",
                "Location": ""
            }
        ]
    }
}
```


&nbsp;
