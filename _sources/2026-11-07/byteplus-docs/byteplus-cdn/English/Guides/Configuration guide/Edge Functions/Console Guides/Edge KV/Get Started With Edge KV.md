---
title: "Get Started With Edge KV"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-EdgeKV-overview"
---

This tutorial introduces how to use Edge KV in edge functions based on a simple example scenario.

Edge KV service is a distributed key\-value storage service on BytePlus's global edge nodes. After a key\-value pair is written to Edge KV through the edge function console, OpenAPI, or runtime API, it is automatically synchronized to all edge nodes. Functions can quickly read key\-value pairs located on the same edge node through the runtime API.

<span id="example-scenario"></span>
## Example scenario

Your website supports A/B testing functionality, which can return different versions of web pages based on the user's geolocation. The version switching configuration information is stored in Edge KV. You want to read the version switching configuration information from the function's code. In this tutorial, assume the configuration information is as follows:

```json
{
  "us": "versionA",
  "eu": "versionB",
  "asia": "versionA"
}
```


<span id="steps"></span>
## Steps

You need to complete the following steps to implement the example scenario.


1. Create a namespace.

2. Create a key\-value pair in the namespace.

3. Read the value from the key\-value pair in the function code.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_fba7f0d1456f52bc9f12faf4b4f6651b.jpeg) </span>

<span id="step-1-create-a-namespace"></span>
### Step 1: Create a namespace

Follow these steps to create a namespace.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can only create namespaces using the console or OpenAPI. You cannot create namespaces using the runtime API.</div>



1. Open the [Edge KV](https://console.byteplus.com/cdn/edge-function/list) page.

2. On the **Edge KV** page, click **Create namespace**.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e7fec2fd871da96e5a489b8c0e00afd1.jpeg) </span>

3. In the **Create namespace** dialog box, set the following parameters, then click **Save**.

   
   |Parameter |Description |
   |---|---|
   |Name |Set to `abtest_config`. |
   |Description |Set to `demo`. |
   |Project |Set to `default`. |
   

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_2ecf340d7d2a275d536535588b41cdba.jpeg) </span>


<span id="step-2-create-a-key-value-pair-in-the-namespace"></span>
### Step 2: Create a key\-value pair in the namespace

Follow these steps to create a key\-value pair in the namespace.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can create key\-value pairs using the console, OpenAPI, or runtime API.</div>



1. Open the [Edge KV](https://console.byteplus.com/cdn/edge-function/list) page.

2. Find the `abtest_config` namespace you created, and click on the name of the namespace.

3. Click **Add data**.

4. In the **Add data** dialog box that appears, set the relevant parameters for the data, then click **Save**.

   
   |Parameter |Description |
   |---|---|
   |Key |Set to `config_key`. |
   |Value |Set to the JSON value from the example scenario: `{"us":"versionA","eu":"versionB","asia":"versionA"}`. |
   |TTL |Set to **Never expires**. |
   

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_d1ef1b9b0493e3aa886b12bbeca774b1.jpeg) </span>


<span id="step-3-read-the-value-from-the-key-value-pair-in-the-function-code"></span>
### Step 3: Read the value from the key\-value pair in the function code

Follow these steps to read the value from the key\-value pair in the function code.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can read the value of a key\-value pair using the console, OpenAPI, or runtime API.</div>


In the function code, you call [KV.get()](https://docs.byteplus.com/docs/byteplus-cdn/docs-EdgeKV-RuntimeAPI) to get the value of the key\-value pair.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The debugging environment of edge functions currently does not support running the <a href="https://docs.byteplus.com/docs/byteplus-cdn/docs-EdgeKV-RuntimeAPI">Edge KV runtime API</a>. The Edge KV runtime API can only run in the production environment.</div>


```JavaScript
const config = await KV.get("abtest_config","config_key",{type:"string"});
```
