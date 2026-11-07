---
title: "dropCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/javasdk_dropCollection"
---

<span id="07d78349"></span>
# Overview

The DropCollection operation permanently deletes a specified Collection. Before you can delete a Collection, you must first delete all associated indexes.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Deleting a collection permanently removes all data in the specified collection. Proceed with caution</div>


* <div data-tips="true" data-tips-type="warning">Before deleting a collection, you must first delete all of its associated indexes.</div>



<span id="5c7af53d"></span>
# **Request Parameters**


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|collectionName |String |Yes |Specify the name of the Collection to delete.<br><br><br>* The name can only contain English letters, numbers, and underscores. It must begin with an English letter and cannot be empty.<br><br>* Length: 1 to 128 characters.<br><br>* Collection names must be unique. |


<span id="9e69bd89"></span>
# Example

<span id="ffcf8878"></span>
## Request

```Java
vikingDBService.dropCollection("javaSDKTest");
```


<span id="c7312d98"></span>
## Return Value

A successful call does not return any information.
