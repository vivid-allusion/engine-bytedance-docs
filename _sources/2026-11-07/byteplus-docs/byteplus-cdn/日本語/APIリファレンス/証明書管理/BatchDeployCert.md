---
title: "BatchDeployCert"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/BatchDeployCert_jp"
---

指定された証明書を1つ以上のドメイン名に関連付けます。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：毎秒最大20のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=BatchDeployCert&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はBatchDeployCertです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Domain |String |はい |`CertId` に関連付ける必要があるドメイン名のリストを表します。リストには最大 50 のドメイン名を含めることができます。複数のドメイン名はコンマ（,）で区切ります。<br><br>リスト内のドメイン名が証明書の SAN フィールドにない場合、そのドメイン名を証明書に関連付けることはできません。 |`www.example.com,img.example.com` |
|CertId |String |はい |関連付ける証明書の ID を表します。 |`cert-c195f679cecb4f34tj23dd8c54e6c0a2` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|DeployResult |Object[] |各ドメイン名の関連付け結果を表します。 | |
|Domain |String |`Domain` 内のドメイン名を表します。 |`www.example.com` |
|Status |String |関連付けが成功したかどうかを示します。このパラメーターには次の値があります：<br><br><br>* `success`：関連付けが成功したことを示します。<br><br>* `fail`：関連付けが失敗したことを示します。失敗の理由は `ErrorMsg` パラメーターで説明されています。 |`success` |
|ErrorMsg |String |関連付けが失敗した理由を示します。`Status` が `success` の場合、このパラメーターの値は空（""）です。 |`some error` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=BatchDeployCert&Version=2021-03-01
{
    "Domain": "www.example.com,docs.example.com",
    "CertId": "cert-a4827a17f0964010a199e74f6e6b6a52"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "2025091106370814AF152ABDC20800D531",
        "Action": "BatchDeployCert",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DeployResult": [
            {
                "Domain": "www.example.com",
                "ErrorMsg": "",
                "Status": "success"
            },
            {
                "Domain": "docs.example.com",
                "ErrorMsg": "",
                "Status": "success"
            }
        ]
    }
}
```


&nbsp;
