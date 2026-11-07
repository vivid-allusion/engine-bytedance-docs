---
title: "fetchData (collection)"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/javasdk_fetchData__collection"
---

<span id="e2b0565e"></span>
# Overview

To retrieve specific data objects from a collection, you can use the fetchData method. This reference guide provides the necessary request parameters, Java code examples, and return value specifications to help you query single or multiple data entries by their primary keys. You can query up to 100 records at a time.

After data in the collection is written or deleted, it can be queried in real time.

<span id="2287edee"></span>
# **request parameters**


|**parameter** |**type** |**Required** |**default value** |**parameter description** |
|---|---|---|---|---|
|ID |String, int64,<br><br>List\ < int64 \>,<br><br>List\ < string \> |Yes |*  |A primary key or a list of primary keys. |


<span id="02c993a9"></span>
# Complete example

<span id="b969db9b"></span>
## Request parameters

```Java
// Call getCollection once during program initialization to get the specified collection. 
Collection collection = vikingDBService.getCollection("javaSDKTest");
```


```Java
List ids = new ArrayList<>();
ids.add("11");
ids.add("22");
ids.add("33");
ids.add("44");
List dataObjects = collection.fetchData(ids);
System.out.println(dataObjects);
```


<span id="5f769602"></span>
## Return value

The call returns a DataObject instance or a list of DataObject instances. The properties contained in a DataObject instance are shown in the following table.


|**attribute** |**Description** |
|---|---|
|ID |The primary key. |
|Fields |The fields field in the response contains the specific data as a map. |
