---
title: "APIリクエストの送信"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/send-api-requests-jp"
---

このドキュメントでは、BytePlus CDN APIの呼び出し方法について説明します。

APIリクエストを送信する前に、以下の点を理解する必要があります：


* [リクエスト構造](https://docs.byteplus.com/en/docs/18/35852#5b9d2b92)

* [共通パラメータ](https://docs.byteplus.com/en/docs/18/35852#fe839f95)

* [リクエスト認証](https://docs.byteplus.com/en/docs/18/35852#a5eeecac)

* [署名計算方法](https://docs.byteplus.com/en/docs/18/35852#6d2e1525)


<span id="5b9d2b92"></span>
## リクエスト構造

APIリクエストの構造には以下が含まれます：


* APIサービスアドレス

* 通信プロトコル

* リクエストメソッド

* リクエストパラメータ


<span id="d3d77560"></span>
### APIサービスアドレス

BytePlus CDNのAPIサービスアドレスは `cdn.byteplusapi.com` です。

<span id="e38c1246"></span>
### 通信プロトコル

リクエストの送信には `HTTP` または `HTTPS` プロトコルを使用できます。セキュリティを高めるために `HTTPS` プロトコルの使用をお勧めします。

<span id="27fde477"></span>
### リクエストメソッド

特に指定がない限り、`POST` メソッドを使用してリクエストを送信してください。また、リクエストヘッダーで `Content-Type: application/json` を指定する必要があります。

<span id="bbb5713d"></span>
### リクエストパラメータ

リクエストパラメータには、共通パラメータと各API固有のパラメータが含まれます。

<span id="fe839f95"></span>
## 共通パラメータ

共通パラメータはすべてのAPIリクエストに必要です。共通パラメータがAPIリクエストに含まれていない場合、リクエストは失敗します。以下の表は、クエリ文字列に含める必要がある共通パラメータを示しています。


|パラメータ名 |データ型 |必須 |説明 |例 |
|---|---|---|---|---|
|Action |string |はい |APIの名前を表します。名前は正規表現形式 [a\-zA\-Z]+ に従います。 |`DescribeCdnData` |
|Version |string |はい |APIのバージョンを表します。このパラメータの値は `2021-03-01` です。 |`2021-03-01` |
|X\-Expires |int |いいえ |認証情報に含まれる署名の有効期間を秒単位で表します。デフォルト値は `900` です。 |`900` |


<span id="a5eeecac"></span>
## リクエスト認証

すべてのリクエストには、リクエスト送信者の身元を確認するための認証情報を含める必要があります。認証情報は以下のいずれかの方法で提供できます。方法1を推奨します。

<span id="9359e363"></span>
### （推奨）方法1：リクエストヘッダーに認証情報を含める

リクエストヘッダーに以下のパラメータを含める必要があります：


| **パラメータ名** | **データ型** |**必須** |**説明** |**例** |
|---|---|---|---|---|
|X\-Date |string |はい |UTC時間での署名計算時刻を表します。時間精度は秒単位です。このパラメータについて、以下の点に注意してください：リクエストが到着すると、CDNは到着時刻とX\-Dateの差を計算します。その差がX\-Expiresで指定された時間範囲を超える場合、CDNはリクエストを無効と見なします。したがって、署名を計算する前にシステム時刻を調整することをお勧めします。 |`20210913T081805Z` |
|Authorization |string |はい |このパラメータは認証文字列を表します。このパラメータの擬似コードは以下の通りです：`HMAC-SHA256 Credential = {AccessKey}/{ShortDate}/{Region}/{Service}/{Request}, SignedHeaders={SignedHeaders}, Signature={Signature}`。この擬似コードの説明は以下の通りです：\* 擬似コードの `Signature` パラメータは計算された署名を表します。署名の計算方法については、[署名計算方法](https://docs.byteplus.com/en/docs/18/35852#6d2e1525)を参照してください。\* 擬似コードの他のパラメータの説明については、[擬似コードパラメータの説明](https://docs.byteplus.com/en/docs/18/35852#1d34a18e)を参照してください。 | |


<span id="2a353a38"></span>
### 方法2：クエリ文字列に認証情報を含める

クエリ文字列に以下のクエリパラメータを含める必要があります。


| **パラメータ名** | **データ型** | **パラメータの説明** |**例** |
|---|---|---|---|
|X\-Date |string |UTC時間での署名計算時刻を表します。時間精度は秒単位です。このパラメータについて、以下の点に注意してください：\* リクエストが到着すると、CDNはリクエスト到着時刻と `X-Date` の時間差を計算します。その差が `X-Expires` で指定された時間範囲を超える場合、CDNはリクエストを無効と見なします。したがって、署名を計算する前にシステム時刻を調整することをお勧めします。 |`20210913T081805Z` |
|X\-Algorithm |string |署名計算に使用されるアルゴリズムを表します。このパラメータの値は `HMAC-SHA256` です。 |`HMAC-SHA256` |
|X\-Credential |string |パラメータ値の擬似コードは以下の通りです：`{AccessKey}/{ShortDate}/{Region}/{Service}/{Request}`。`X-Credential` の擬似コードのパラメータの説明については、[擬似コードパラメータの説明](https://docs.byteplus.com/en/docs/18/35852#1d34a18e)を参照してください。 |`AKLTMjI2ODVlYzI3ZGY1NGU4ZjhjYWRjMTlmNTM5OTZkYzE/20210913/singapore/CDN/request` |
|X\-SignedHeaders |string |このパラメータの説明は、[擬似コードパラメータの説明](https://docs.byteplus.com/en/docs/18/35852#1d34a18e)の `SignedHeaders` パラメータと同じです。 |`host;x-content-sha256;x-date` |
|X\-Signature |string |計算された署名を表します。署名の計算方法については、[署名計算方法](https://docs.byteplus.com/en/docs/18/35852#6d2e1525)を参照してください。 | |


<span id="6d2e1525"></span>
## 署名計算方法

このセクションでは主に署名の計算方法について説明します。[擬似コードパラメータの説明](https://docs.byteplus.com/en/docs/18/35852#1d34a18e)はドキュメントの最後に提供されています。


* このセクションの擬似コードで使用される `HMAC` メソッドは、HMAC\-SHA256アルゴリズムを使用します。

* このセクションの擬似コードで使用される `HexEncode` メソッドは、文字列を16進数エンコーディング形式の文字列に変換します。


署名パラメータ `Signature` は、`kSigning` と `StringToSign` パラメータに基づいて計算されます。`Signature` の擬似コードは以下の通りです：

```Plain
Signature = HexEncode(HMAC(kSigning, StringToSign))
```


<span id="ksigning"></span>
### kSigning

`kSigning` は署名の計算に使用されるキーを表します。`kSigning` を計算するには、まず[アカウントのAccess Key Secretを取得し](https://console.byteplus.com/iam/keymanage)、その後、以下の擬似コードを使用して `kSigning` を生成する必要があります。

```Plain
kSecret = <Your Access Key Secret>
kDate = HMAC(kSecret, ShortDate)
kRegion = HMAC(kDate, Region)
kService = HMAC(kRegion, Service)
kSigning = HMAC(kService, "request")
```


`kSigning` の擬似コードのパラメータの説明については、[擬似コードパラメータの説明](https://docs.byteplus.com/en/docs/18/35852#1d34a18e)を参照してください。

<span id="20cd71e8"></span>
### StringToSign

`StringToSign` は、署名の計算に使用される署名文字列を表します。`StringToSign` の擬似コードは以下の通りです：

```Plain
// The Hash function uses the SHA256 algorithm
StringToSign = Algorithm + '\n' + RequestDate + '\n' + CredentialScope + '\n' + HexEncode(Hash(CanonicalRequest))
```


`StringToSign` の擬似コードにおける `Algorithm` と `RequestDate` パラメータの説明については、擬似コードのパラメータの説明を参照してください。`StringToSign` の擬似コードにおける他のパラメータの説明は以下の通りです。

**CredentialScope**

`CredentialScope` は認証情報の範囲を表します。`CredentialScope` の擬似コードは以下の通りです：

```Plain
{ShortDate}/{Region}/{Service}/{Request}
```


`CredentialScope` の擬似コードのパラメータの説明については、[擬似コードパラメータの説明](https://docs.byteplus.com/en/docs/18/35852#1d34a18e)を参照してください。

**CanonicalRequest**

`CanonicalRequest` は正規化されたリクエストを表します。`CanonicalRequest` の擬似コードは以下の通りです：

```Plain
HTTPRequestMethod + '\n' + CanonicalURI + '\n' + CanonicalQueryString + '\n' + CanonicalHeaders + '\n' + SignedHeaders + '\n' + HexEncode(Hash(RequestPayload))
```


`CanonicalRequest` の擬似コードのパラメータの説明は以下の通りです：


* `HTTPRequestMethod`：リクエストメソッドを表します。CDNの場合、このパラメータの値は `POST` です。

* `CanonicalURI`：リクエストのURIを表します。

* `CanonicalQueryString`：正規化されたクエリ文字列を表します。`CanonicalQueryString` の値は以下のルールに従って生成されます：

   * クエリパラメータをパラメータ名の昇順でソートします。

* `CanonicalHeaders`：正規化されたリクエストヘッダーを表します。`CanonicalHeaders` は以下の手順で生成されます：

   * 署名計算に関与するリクエストヘッダーパラメータの名前を小文字に変換します。

   * これらの名前を文字レベルで昇順にソートします。

   * これらのリクエストヘッダーパラメータをキーと値の形式で連結します。キーはリクエストヘッダーパラメータの名前で、値はリクエストヘッダーパラメータの値です。

   * 各リクエストヘッダーパラメータの後に改行（`\n`）を追加します。

* `SignedHeaders`：[擬似コードパラメータの説明](https://docs.byteplus.com/en/docs/18/35852#1d34a18e)を参照してください。

* `HexEncode(Hash(RequestPayload))`：計算された値を表します。この値は、リクエストボディの `payload` の値にSHA256ハッシュアルゴリズムを適用して得られます。


<span id="1d34a18e"></span>
## 擬似コードパラメータの説明

以下の表は、このドキュメントの擬似コードで使用されているパラメータの説明を含んでいます。


|パラメータ名 |データ型 |パラメータの説明 |例 |
|---|---|---|---|
|AccessKey |string |アカウントのアクセスキーIDを表します。[アクセスキーの取得](https://console.byteplus.com/iam/keymanage)を参照してください。 |`AKLTMjI2ODVlYzI3ZGY1NGU4ZjhjYWRjMTlmNTM5OTZkYzE` |
|RequestDate |string |このパラメータは、[リクエスト認証](https://docs.byteplus.com/en/docs/18/35852#a5eeecac)セクションの `X-Date` の定義と同じです。 |`20210913T081805Z` |
|ShortDate |string |このパラメータは `RequestDate` の定義と同じですが、日単位の精度です。 |`20210913` |
|Region |string |このパラメータは署名計算に使用されます。パラメータ値は `singapore` を推奨しますが、任意の空でない文字列でも構いません。 |`singapore` |
|Service |string |CDNのサービス名を表します。このパラメータの値は `CDN` です。 |`CDN` |
|SignedHeaders |string |署名計算に関与するリクエストヘッダーパラメータを表します。複数のリクエストヘッダーパラメータはセミコロン（;）で区切られます。これらのリクエストヘッダーパラメータはパラメータ名に基づいて昇順でソートされます。<br><br>一般的に、`SignedHeaders` の値は `host;x-content-sha256;x-date` です。任意のリクエストヘッダーパラメータを `SignedHeaders` の値として指定することもできます。 |`host;x-content-sha256;x-date` |
|Algorithm |string |署名計算に使用されるアルゴリズムを表します。このパラメータの値は `HMAC-SHA256` です。 |`HMAC-SHA256` |
|Request |string |このパラメータは値が `request` の定数です。 |`request` |


<span id="5b974693"></span>
## リクエスト例

```Plain
POST https://cdn.byteplusapi.com/?Action=DescribeCdnConfig&Version=2021-03-01

// Request Headers
X-Date: 20230116T073702Z
Authorization: HMAC-SHA256 Credential=AKLTMjYxYTZmYWU4ZWYzNGI2NDg8NTUxODE1ZGVhNmIxZmQ/20230116/singapore/CDN/request, SignedHeaders=x-content-sha256;x-date, Signature=5a394ce80456c7cdf989c28bd638807c8ead386eb15dd36e39952f405380aef2
Content-Type: application/json

//Request Body
{
    "Domain": "www.example.com"
}
```
