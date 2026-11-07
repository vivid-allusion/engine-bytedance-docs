---
title: "primary key filtering"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/javasdk_primary_key_filtering"
---

To refine your vector search results, you can filter them based on a list of primary keys.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Primary key filtering is a universal search capability that you can use in<strong>search</strong>Incoming from the relevant interface<strong>PrimaryKeyIn or PrimaryKeyNotIn parameters</strong>To enable scalar filtering capabilities.</div>


<span id="39a9ae24"></span>
# Parameter description


|**parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|
|PrimaryKeyIn |List< int64 \> or list < string \> |No |None |Setting this parameter restricts retrieval to the primary key list.<br><br>Passing in an empty list has the same effect as not passing this parameter. |
|PrimaryKeyNotIn |List< int64 \> or list < string \> |No |None |Setting this parameter will exclude data with primary keys in the specified list from the search results. |


<span id="b341896a"></span>
# Example

```Java
// Call this operation once during program initialization to get the specified index. 
Index index = vikingDBService.getIndex("javaSDKTest", "test_index");
```


```Java
List outputField = Arrays.asList("f_id", "f_string", "f_int64");
List datas = index.search(new SearchParam()
           .setVectorOrder(new VectorOrder().setVector(DataUtil.genRandomVector(4)).build())
           .setOutputFields(outputField)
           .setPartition("default")
           .setPrimaryKeyIn(Arrays.asList(0, 1, 2, 3, 4, 5))
           .setPrimaryKeyNotIn(Arrays.asList(2, 3))
           .setLimit(20)
           .build());
 System.out.println(datas);
```


<span id="0a0ea4e6"></span>
## Return value

The Java call for the above task returns List. The properties contained in the DataObject instance are shown in the following table.


|**attribute** |**Description** |
|---|---|
|ID |The primary key. |
|Fields |A map containing the data for the returned fields. |
|Score |Indicates the degree to which the found vector matches the input vector. |
