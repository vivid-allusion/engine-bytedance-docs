---
title: "GetFunction"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/GetFunction_jp"
---

指定された関数の詳細情報を取得します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20リクエストまで送信可能です。

<span id="リクエストの説明"></span>
## リクエストの説明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=GetFunction&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API 名称。現在のAPIの名前は `GetFunction` です。 |
|Version |String |はい |API バージョン。現在のAPIのバージョンは `2021-03-01` です。 |
|FunctionId |String |はい |関数ID。[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-jp)を呼び出して関数IDを取得できます。 |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |タイプ |説明 |例 |
|---|---|---|---|
|AccountIdentity |Long |BytePlus アカウントID。 |`20****` |
|UserIdentity |Long |このパラメータには実質的な意味はありません。このパラメータを無視してください。 | |
|Domain |String[] |関数に関連つけられたドメイン。 |`["example.com"]` |
|Name |String |関数の名前。 |`hello-ve` |
|ClazzName |String |このパラメータには実質的な意味はありません。このパラメータを無視してください。 | |
|BindingType |Integer |このパラメータには実質的な意味はありません。このパラメータを無視してください。 | |
|FunctionId |String |関数のID。 |`3gyz993****` |
|Status |Integer |関数のステータス。<br><br><br>* 100：実行中<br><br>* 400：未関連付け<br><br>* 500：設定中 |`100` |
|IsPublish |Boolean |このパラメータには実質的な意味はありません。このパラメータを無視してください。 | |
|IsFullPublish |Boolean |このパラメータには実質的な意味はありません。このパラメータを無視してください。 | |
|CodeType |String |このパラメータには実質的な意味はありません。このパラメータを無視してください。 | |
|Creator |String |関数を作成したユーザー名。 |`example` |
|CreateTime |Long |作成日時。Unixタイムスタンプ（秒）形式。 |`1638326159` |
|UpdateTime |Long |更新日時。Unixタイムスタンプ（秒）形式。 |`1638326159` |
|Remark |String |関数の備考。 |`this is a test` |
|ProjectName |String |関数が属するプロジェクトの名前。 |`default` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```HTTP
GET  https://cdn.byteplusapi.com?Action=GetFunction&Version=2021-03-01&FunctionId=bc36dc7c58e942f0b9f125d186df****
```


<span id="レスポンス例"></span>
### レスポンス例

```json

{
    "ResponseMetadata": {
        "RequestId": "202404220913431B87E7D87928AD8F48BE",
        "Action": "GetFunction",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Function": {
            "AccountIdentity": 300000****,
            "UserIdentity": 0,
            "Domain": [
                "test.example.com"
            ],
            "Name": "test",
            "ClazzName": "Free",
            "BindingType": 0,
            "FunctionId": "bc36dc7c58e942f0b9f125d186df****",
            "Status": 400,
            "IsPublish": true,
            "IsFullPublish": true,
            "CodeType": "js",
            "Creator": "test_user",
            "CreateTime": 1713776330,
            "UpdateTime": 1713776330,
            "Remark": "",
            "ProjectName": "default"
        }
    }
}
```


&nbsp;
