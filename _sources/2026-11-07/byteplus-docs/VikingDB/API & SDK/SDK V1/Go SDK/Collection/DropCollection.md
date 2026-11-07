---
title: "DropCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/gosdk_DropCollection"
---

<span id="91d3cb5a"></span>
# Overview

The DropCollection function allows you to permanently delete a specified Collection and all its data. Before you can successfully delete a Collection, you must ensure that all associated indexes have been deleted first.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Deleting a collection permanently deletes all data in the specified collection. Proceed with caution.</div>


* <div data-tips="true" data-tips-type="warning">Before deleting a collection, you must first delete all of its associated indexes.</div>



<span id="81b012b9"></span>
# **request parameters**


|**parameter** |**type** |**Is it required?**  |**parameter description** |
|---|---|---|---|
|collectionName |String |Yes |Specify the name of the Collection to delete.<br><br><br>* The name must begin with a letter, can only contain English letters, numbers, and underscores (_), and cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Collection names cannot be repeated. |


<span id="d51fa3d4"></span>
# Example

<span id="1e11445b"></span>
## Request parameters

```Go
err := service.DropCollection("go")
if err != nil {
    fmt.Println(err.Error())
}
```


<span id="456a3363"></span>
## Return value

A successful call does not return any value.
