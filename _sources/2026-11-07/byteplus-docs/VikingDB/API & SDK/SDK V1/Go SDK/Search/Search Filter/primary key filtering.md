---
title: "primary key filtering"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/gosdk_primary_key_filtering"
---

You can filter results by primary key in a vector database using the primary key filtering capability.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Primary key filtering is a universal search capability that you can use in<strong>search</strong>Incoming from the relevant interface<strong>PrimaryKeyIn or PrimaryKeyNotIn parameters</strong>To enable scalar filtering capabilities.</div>


<span id="c5cc0071"></span>
# Parameter description


|**parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|
|PrimaryKeyIn |Listor list |No |None |Setting this parameter restricts retrieval to the primary key list.<br><br>Passing in an empty list has the same effect as not passing this parameter. |
|PrimaryKeyNotIn |Listor list |No |None |Setting this parameter will exclude data with primary keys in the specified list from the search results. |


<span id="79a49221"></span>
# Example

```Go
// Call the related operation once during the initialization of the program to get the specified index. 
index, _ := service.GetIndex("go", "goIndex")
```


```Go
filter := map[string]interface{}{
                "op":    "range",
                "field": "f_int64",
                "gt":    10,
        }
searchOpt := vikingdb.NewSearchOptions().SetFilter(filter).SetLimit(5).
                SetPrimaryKeyIn([]interface{}{"1", "2", "3", "4"}).
                SetPrimaryKeyNotIn([]interface{}{"1"}).
                SetRetry(true)
datas, err := index.Search(nil, searchOpt)
        if err != nil {
                panic(err)
        }
        for _, data := range datas {
                fmt.Println(data.Fields, data.Score)
        }
```


<span id="3f52ad81"></span>
## Return value

This Go operation performs the task and returns a List. The properties contained in the DataObject instance are shown in the following table.


|**attribute** |**Description** |
|---|---|
|Id |Primary key id. |
|Fields |The Fields attribute contains the specific data, returned as a map. |
|Score |Indicates the degree to which the found vector matches the input vector. |
