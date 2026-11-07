---
title: "KV"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-EdgeKV-RuntimeAPI-cn"
---

KV 接口用于管理边缘 KV 的数据。

<span id="kv-set"></span>
## KV.set()

向指定的存储空间添加一个键值对。如果键已存在，该方法更新已有的键值对的值。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如果您的 BytePlus 账号下还没有存储空间，您需要使用控制台或 OpenAPI 创建一个存储空间。</div>


在每个边缘节点上，每个 Byteplus 账号对一个存储空间下的一个键，每秒最多允许调用 1 次 `set()`。

<span id="语法"></span>
### 语法

```JavaScript
promise<undefined> KV.set(
    namespace: String, 
    key: String, 
    value: String | ArrayBuffer | ArrayBufferView | ReadableStream, 
    options: Object = {},
)
```


<span id="参数"></span>
#### 参数


* namespace：数据写入的存储空间的名称。您需要使用控制台或 OpenAPI 创建存储空间。

* key：键。只能包含英文字母、数字、连字符（\-）以及下划线（_），最长支持 512 个字节。

* value：值。一个键对应一个值。值的大小不超过128KB。

* option：可选设置。仅支持 TTL 字段，用于设置 KV 数据的有效时间，单位为秒。数据到期之后，键对应的值将无法被访问。默认值是永久保存。

    &nbsp;


<span id="返回值"></span>
#### 返回值

该接口会返回一个 Promise。


* 如果数据添加成功，Promise 被 resolve 为 undefined。

* 如果数据添加失败，Promise 被 reject。


<span id="示例"></span>
### 示例

以下示例表示在存储空间（`people`）下添加一条数据（`name`, `tom`）并设置该数据在 100 秒后失效。

```JavaScript
await KV.set("people", "name", "tom", {ttl: 100});
```


<span id="kv-get"></span>
## KV.get()

从存储空间获取指定键对应的值。

<span id="语法"></span>
### 语法

```JavaScript
promise<value_type> KV.get(
    namespace: String,
    key: String,
    options: Object = {},
)
```


<span id="参数"></span>
#### 参数


* namespace：数据所属存储空间的名称。

* key：数据的键。

* option：可选设置。仅支持 type 字段，用于指定返回值的格式。可选值包括：readableStream、string、arrayBuffer、json。默认值是 stream。


<span id="返回值"></span>
#### 返回值

该接口会返回一个 Promise。


* 如果数据获取成功，Promise 被 resolve 为 type 所指定的类型。

* 如果数据获取失败，Promise 被 reject。


<span id="3f507764"></span>
### 示例

以下示例表示从存储空间（`people`）中获取数据键为 `name` 的数据值并且以 `string` 格式返回数据值。

```JavaScript
const str = await KV.get("people", "name", {type: 'string'});
```


<span id="kv-delete"></span>
## KV.delete()

从存储空间中删除指定的键值对。

<span id="语法"></span>
### 语法

```JavaScript
promise<bool> KV.delete(
    namespace: String,
    key: String,
)
```


<span id="参数"></span>
#### 参数


* namespace：数据所属存储空间的名称。

* key：数据的键。


<span id="返回值"></span>
#### 返回值

该接口会返回一个 Promise。


* 如果指定删除的键存在，Promise 被 resolve 为 true；如果指定删除的键不存在，Promise 被 resolve 为 false。

* 如果数据删除失败（如网络异常、限流策略等导致失败），Promise 被 reject。


<span id="4e9ae6ec"></span>
### 示例

以下示例表示从存储空间（`people`）中删除键为 `name` 的数据。

```JavaScript
const b = await KV.delete("people", "name");
```
