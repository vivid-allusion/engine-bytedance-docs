---
title: "KV"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-EdgeKV-RuntimeAPI-cn-zh-tw"
---

KV 介面用於管理邊緣 KV 的資料。

<span id="kv-set"></span>
## KV.set()

向指定儲存空間新增一組鍵值對。若鍵已存在，該方法更新既有鍵值對的值。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">若您的 BytePlus 帳號尚未建立儲存空間，需使用控制台或 OpenAPI 建立儲存空間。</div>


每個邊緣節點上，每個 BytePlus 帳號對單一儲存空間內的單一鍵，每秒最多允許呼叫 1 次 `set()`。

<span id="語法"></span>
### 語法

```JavaScript
promise<undefined> KV.set(
    namespace: String, 
    key: String, 
    value: String | ArrayBuffer | ArrayBufferView | ReadableStream, 
    options: Object = {},
)
```


<span id="參數"></span>
#### 參數


* namespace：資料寫入的儲存空間名稱。需使用控制台或 OpenAPI 建立儲存空間。

* key：鍵名。僅可包含英文字母、數字、連字號(\-)及底線(_)，最大長度 512 位元組。

* value：數值。單一鍵對應單一數值，數值大小不得超過 128KB。

* option：可選設定。僅支援 TTL 欄位，用於設定 KV 資料有效期(單位：秒)，到期後將無法存取。預設值為永久保存。


<span id="be4e45c6"></span>
#### 回傳值

此介面回傳一個 Promise：


* 資料新增成功時，Promise 被 resolve 為 undefined

* 資料新增失敗時，Promise 被 reject


<span id="範例"></span>
### 範例

以下範例表示在儲存空間(`people`)新增一筆資料(`name`, `tom`)並設定 100 秒後失效：

```JavaScript
await KV.set("people", "name", "tom", {ttl: 100});
```


<span id="kv-get"></span>
## KV.get()

從儲存空間取得指定鍵對應的數值。

<span id="語法"></span>
### 語法

```JavaScript
promise<value_type> KV.get(
    namespace: String,
    key: String,
    options: Object = {},
)
```


<span id="參數"></span>
#### 參數


* namespace：資料所屬儲存空間名稱

* key：資料鍵名

* option：可選設定。僅支援 type 欄位，指定回傳值格式，可選值：readableStream、string、arrayBuffer、json，預設值為 stream


<span id="回傳值"></span>
#### 回傳值

此介面回傳一個 Promise：


* 資料取得成功時，Promise 被 resolve 為 type 指定類型

* 資料取得失敗時，Promise 被 reject


<span id="3f507764"></span>
### 範例

以下範例表示從儲存空間(`people`)取得鍵名為 `name` 的資料並以 string 格式回傳：

```JavaScript
const str = await KV.get("people", "name", {type: 'string'});
```


<span id="kv-delete"></span>
## KV.delete()

從儲存空間刪除指定鍵值對。

<span id="語法"></span>
### 語法

```JavaScript
promise<bool> KV.delete(
    namespace: String,
    key: String,
)
```


<span id="參數"></span>
#### 參數


* namespace：資料所屬儲存空間名稱

* key：資料鍵名


<span id="回傳值"></span>
#### 回傳值

此介面回傳一個 Promise：


* 指定刪除的鍵存在時，Promise 被 resolve 為 true；不存在時 resolve 為 false

* 資料刪除失敗時(如網路異常或限流策略等因素)，Promise 被 reject


<span id="4e9ae6ec"></span>
### 範例

以下範例表示從儲存空間(`people`)刪除鍵名為 `name` 的資料：

```JavaScript
const b = await KV.delete("people", "name");
```
