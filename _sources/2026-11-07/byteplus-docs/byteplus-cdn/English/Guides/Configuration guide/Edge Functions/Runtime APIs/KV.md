---
title: "KV"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-EdgeKV-RuntimeAPI"
---

The KV interface is used to manage edge KV data.

<span id="kv-set"></span>
## KV.set()

Adds a key\-value pair to the specified namespace. If the key already exists, this method updates the value of the existing key\-value pair.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you don't have a namespace under your BytePlus account yet, you need to create one using the console or OpenAPI.</div>


On each edge node, for each BytePlus account, `set()` can be called a maximum of once per second for a key in a namespace.

<span id="syntax"></span>
### Syntax

```JavaScript
promise<undefined> KV.set(
    namespace: String, 
    key: String, 
    value: String | ArrayBuffer | ArrayBufferView | ReadableStream, 
    options: Object = {},
)
```


<span id="parameters"></span>
#### Parameters


* namespace: The name of the namespace where the data will be written. You need to create a namespace using the console or OpenAPI.

* key: The key. It can only contain English letters, numbers, hyphens (\-), and underscores (_), with a maximum length of 512 bytes.

* value: The value. One key corresponds to one value. The size of the value should not exceed 128KB.

* option: Optional settings. Only the TTL field is supported, used to set the validity period of the KV data in seconds. After the data expires, the value corresponding to the key will no longer be accessible. The default value is permanent storage.


<span id="return-value"></span>
#### Return value

This interface returns a Promise.


* If the data is added successfully, the Promise is resolved to undefined.

* If the data addition fails, the Promise is rejected.


<span id="example"></span>
### Example

The following example shows adding a piece of data (`name`, `tom`) under the namespace (`people`) and setting this data to expire after 100 seconds.

```JavaScript
await KV.set("people", "name", "tom", {ttl: 100});
```


<span id="kv-get"></span>
## KV.get()

Retrieve the value corresponding to the specified key from the namespace.

<span id="syntax"></span>
### Syntax

```JavaScript
promise<value_type> KV.get(
    namespace: String,
    key: String,
    options: Object = {},
)
```


<span id="parameters"></span>
#### Parameters


* namespace: The name of the namespace to which the data belongs.

* key: The key of the data.

* option: Optional settings. Only the type field is supported, used to specify the format of the return value. Available values include: readableStream, string, arrayBuffer, json. The default value is stream.


<span id="return-value"></span>
#### Return value

This interface returns a Promise.


* If the data is retrieved successfully, the Promise is resolved to the type specified by the type field.

* If the data retrieval fails, the Promise is rejected.


<span id="example"></span>
### Example

The following example demonstrates retrieving the data value with the key 'name' from the namespace ('people') and returning the data value in 'string' format.

```JavaScript
const str = await KV.get("people", "name", {type: 'string'});
```


<span id="kv-delete"></span>
## KV.delete()

Delete the specified key\-value pair from the namespace.

<span id="syntax"></span>
### Syntax

```JavaScript
promise<bool> KV.delete(
    namespace: String,
    key: String,
)
```


<span id="parameters"></span>
#### Parameters


* namespace: The name of the namespace to which the data belongs.

* key: The key of the data.


<span id="return-value"></span>
#### Return value

This interface returns a Promise.


* If the specified key to be deleted exists, the Promise is resolved to true; if the specified key to be deleted does not exist, the Promise is resolved to false.

* If the data deletion fails (due to network issues, rate limiting policies, etc.), the Promise is rejected.


<span id="example"></span>
### Example

The following example demonstrates deleting the data with the key 'name' from the namespace ('people').

```JavaScript
const b = await KV.delete("people", "name");
```
