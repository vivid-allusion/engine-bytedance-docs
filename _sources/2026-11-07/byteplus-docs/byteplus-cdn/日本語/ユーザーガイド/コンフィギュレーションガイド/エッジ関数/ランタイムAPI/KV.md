---
title: "KV"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-EdgeKV-RuntimeAPI-jp"
---

KVインターフェースは、エッジKVデータを管理するために使用されます。

<span id="kv-set"></span>
## KV.set()

指定された名前空間にキーと値のペアを追加します。キーがすでに存在する場合は、このメソッドは既存のキーと値のペアの値を更新します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">BytePlusアカウントにまだ名前空間がない場合は、コンソールまたはOpenAPIを使用して作成する必要があります。</div>


各エッジノードにおいて、各BytePlusアカウントに対して、名前空間内の1つのキーに対して`set()`を呼び出せるのは、1秒に1回までです。

<span id="構文"></span>
### 構文

```JavaScript
promise<undefined> KV.set(
    namespace: String, 
    key: String, 
    value: String | ArrayBuffer | ArrayBufferView | ReadableStream, 
    options: Object = {},
)
```


<span id="パラメータ"></span>
#### パラメータ


* namespace: データが書き込まれる名前空間の名前。コンソールまたはOpenAPIを使用して名前空間を作成する必要があります。

* key: キー。英字、数字、ハイフン(\-)、アンダースコア(_)のみを含むことができ、最大長は512バイトです。

* value: 値。1つのキーに1つの値が対応します。値のサイズは128KBを超えてはいけません。

* option: オプション設定。TTLフィールドのみがサポートされており、KVデータの有効期間を秒単位で設定するために使用されます。データが期限切れになると、キーに対応する値にアクセスできなくなります。デフォルト値は永続的な保存です。


<span id="戻り値"></span>
#### 戻り値

このインターフェースはPromiseを返します。


* データが正常に追加された場合、Promiseはundefinedで解決されます。

* データの追加に失敗した場合、Promiseは拒否されます。


<span id="例"></span>
### 例

以下の例は、名前空間（`people`）の下にデータ（`name`、`tom`）を追加し、このデータが100秒後に期限切れになるように設定する方法を示しています。

```JavaScript
await KV.set("people", "name", "tom", {ttl: 100});
```


<span id="kv-get"></span>
## KV.get()

指定されたキーに対応する値を名前空間から取得します。

<span id="構文"></span>
### 構文

```JavaScript
promise<value_type> KV.get(
    namespace: String,
    key: String,
    options: Object = {},
)
```


<span id="パラメータ"></span>
#### パラメータ


* namespace: データが属する名前空間の名前。

* key: データのキー。

* option: オプション設定。typeフィールドのみがサポートされており、戻り値の形式を指定するために使用されます。利用可能な値は以下の通りです：readableStream、string、arrayBuffer、json。デフォルト値はstreamです。


<span id="戻り値"></span>
#### 戻り値

このインターフェースはPromiseを返します。


* データの取得に成功した場合、Promiseはtypeフィールドで指定された型で解決されます。

* データの取得に失敗した場合、Promiseは拒否されます。


<span id="例"></span>
### 例

以下の例は、名前空間（'people'）からキー'name'を持つデータ値を取得し、'string'形式でデータ値を返す方法を示しています。

```JavaScript
const str = await KV.get("people", "name", {type: 'string'});
```


<span id="kv-delete"></span>
## KV.delete()

名前空間から指定されたキーと値のペアを削除します。

<span id="syntax"></span>
### Syntax

```JavaScript
promise<bool> KV.delete(
    namespace: String,
    key: String,
)
```


<span id="パラメータ"></span>
#### パラメータ


* namespace: データが属する名前空間の名前。

* key: データのキー。


<span id="戻り値"></span>
#### 戻り値

このインターフェースはPromiseを返します。


* 削除対象の指定されたキーが存在する場合、Promiseはtrueで解決されます。削除対象の指定されたキーが存在しない場合、Promiseはfalseで解決されます。

* データの削除に失敗した場合（ネットワークの問題、レート制限ポリシーなどにより）、Promiseは拒否されます。


<span id="例"></span>
### 例

以下の例は、名前空間（'people'）からキー'name'を持つデータを削除する方法を示しています。

```JavaScript
const b = await KV.delete("people", "name");
```
