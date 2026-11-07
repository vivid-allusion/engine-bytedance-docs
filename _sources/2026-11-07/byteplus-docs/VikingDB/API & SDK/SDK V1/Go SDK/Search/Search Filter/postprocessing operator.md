---
title: "postprocessing operator"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/gosdk_postprocessing_operator"
---

The Postprocessing operator is a post\-retrieval processing capability provided by VikingDB. It is used after the vector recall phase to further filter and optimize candidate data, ensuring that the final search results are more accurate and efficient.

In VikingDB, postprocessing operators can be used to:


* Precise screening of results: Set filtering rules using regular expressions based on business requirements, such as filtering products that contain specific text, to ensure that users get valid search results.

* Data quality improvement: Use regular expressions to check the format of search results, filter data containing special characters, illegal content, or advertising information, and ensure that the returned content is standardized.

* Search Results Equalization: Set frequency limits on specific fields to prevent certain values from appearing too frequently in search results, such as popular brands, popular authors, or overexposure of specific categories, and ensure the diversity and fairness of search results.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Postprocessing operators are general\-purpose search capabilities that you can apply to basic vector search and dense sparse hybrid retrieval.</div>


<span id="e5172b19"></span>
# Parameter description


|**parameter** |**type** |Required |**default value** |**parameter description** |
|---|---|---|---|---|
|PostProcessOps |List\ < map \> |No |*  |List of postprocessing operators. After the vector or scalar recall phase, further filtering is performed on the candidate data, for tasks such as string matching and frequency control. Each operator is a map and is executed serially. Default is empty. See postprocessing operators below for details. |
|PostProcessInputLimit |Int |No |*  |When post_process_ops is set, this parameter specifies the number of candidates to enter the post\-processing phase. The default value is 1000, and the maximum value is min (1600, limit \* 10). |


<span id="8ef68518"></span>
## Postprocessing operators


|Operator |Description |Example |
|---|---|---|
|string_match |Regular expression matching operator. Only for fields of type string.<br><br>For the regular expression syntax, refer to: Syntax |```JSON```<br>```{```<br>```   "op": "string_match",```<br>```   "field": "name",```<br>```   "pattern": "^[0-9A-Za-z_]+$"```<br>```}```<br> |
|string_contain |Keyword matching operator. Only for fields of type string.<br><br>Indicates that the field content contains a pattern. |```JSON```<br>```{```<br>```   "op": "string_contain",```<br>```   "field": "name",```<br>```   "pattern": "bar"```<br>```}```<br> |
|enum_freq_limiter |Frequency operator. Only for fields of type string.<br><br>Used to ensure that the total number of occurrences of a particular value in a recall does not exceed the threshold. |```JSON```<br>```{```<br>```  "op": "enum_freq_limiter",```<br>```  "field": "city"```<br>```  "threshold": 5```<br>```}```<br> |


<span id="87b519a8"></span>
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
searchOpt := vikingdb.NewSearchOptions().SetFilter(filter).SetLimit(15).
                SetPostProcessOps([]map[string]interface{}{
                        {"op": "enum_freq_limiter", "field": "f_string", "threshold": 1},
                        {"op": "string_contain", "field": "f_string", "pattern": "doc2%"},
                }).
                SetPostProcessInputLimit(10).
                SetRetry(true)
datas, err := index.Search(nil, searchOpt)
        if err != nil {
                panic(err)
        }
        for _, data := range datas {
                fmt.Println(data.Fields, data.Score)
        }
```


<span id="d26e5dcf"></span>
## Return value

The Go call performs the above task and returns a `List<dataobject>`. The properties contained in the DataObject instance are shown in the following table.


|Attribute |Description |
|---|---|
|Id |The primary key ID. |
|Fields |The data for the object's fields, returned as a map. |
|Score |Indicates the degree to which the found vector matches the input vector. |
