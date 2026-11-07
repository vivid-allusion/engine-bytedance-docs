---
title: "primary key filtering"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/pysdk_primary_key_filtering"
---

You can filter results by primary key in a vector database using its primary key filtering capability.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Primary key filtering is a universal search capability that you can enable by passing the <strong>primary_key_in</strong> or <strong>primary_key_not_in</strong> parameters in the relevant search method. To refine your vector search results, you can use primary key filtering to include or exclude specific vectors based on their IDs.</div>


<span id="0d7beee9"></span>
# Parameter description


|**parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|
|primary_key_in |List< int64 \> or list < string \> |No |None |Setting this parameter restricts retrieval to the primary key list.<br><br>Passing in an empty list has the same effect as not passing this parameter. |
|primary_key_not_in |List< int64 \> or list < string \> |No |None |Setting this parameter will exclude data with primary keys in the specified list from the search results. |


<span id="e9cc92b7"></span>
# Example

```Python
# Retrieve the specified index. This method only needs to be called once during program initialization
index = vikingdb_service.get_index("example_text", "example_index_text")
```


```Python
datas = index.search(order=None, limit=5, primary_key_in=[1, 2, 3, 4, 5, 6, 7, 8, 9, 10], primary_key_not_in=[1])
    for data in datas:
        print(data.id, data.fields, data.score)
    print("========================")

datas = index.search_by_id(id=2, limit=5, output_fields=["f_id", 'f_vector'],  primary_key_in=[1, 2, 3, 4, 5, 6, 7, 8, 9, 10], primary_key_not_in=[1])
    for data in datas:
        print(data.id, data.fields, data.score)
    print("========================")

datas = index.search_by_vector(vector=[0,0,0,0], limit=10, primary_key_in=[1, 2, 3, 4, 5, 6, 7, 8, 9, 10], primary_key_not_in=[5, 6, 7, 8, 9, 10])
    for data in datas:
        print(data.id, data.fields, data.score)
    print("========================")
```
