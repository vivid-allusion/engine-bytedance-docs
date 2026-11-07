---
title: "postprocessing operator"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/javasdk_postprocessing_operator"
---

A postprocessing operator, part of VikingDB's post\-retrieval processing capability, is used after vector recall to further filter and optimize candidate data to ensure that the final search results are more accurate and efficient.

In VikingDB, post\-processing operators can be used to:


* **Precise screening of results**: Set filtering rules through regular matching based on business requirements, such as filtering products that contain certain characteristic text information, to ensure that users get valid search results.

* **Data quality improvement**: Use regular matching to check the format of search results, filter data containing special characters, illegal content or advertising information, ensure that the returned content meets standards, and improve data standardization.

* **Search Results Equalization**: Set frequency limits on specific fields to prevent certain values from occupying too many search results, such as popular brands, popular authors, or overexposure of specific categories, and ensure the diversity and fairness of search results.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Postprocessing operators are general\-purpose search capabilities that you can apply to basic vector search and dense sparse hybrid retrieval.</div>


<span id="00f01f8b"></span>
# Parameter description


|**parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|
|PostProcessOps |List\ < map \> |No |*  |List of postprocessing operators. After the vector or scalar recall phase, further filtering is performed on the candidate data, such as string matching, frequency control, etc. Each operator is a map and is executed serially. Default is empty. See postprocessing operators below for details. |
|PostProcessInputLimit |Int |No |*  |When post_process_ops is set, the number of candidates to enter the post\-processing phase. The default value is 1000, and the maximum value is min (1600, limit \* 10). |


<span id="0704c9d5"></span>
## Postprocessing operator


|Operator |**Description** |Example |
|---|---|---|
|string_match |Regular matching operator. Only for fields of type string.<br><br>For regular matching rules, please refer to: [[Syntax]](https://github.com/google/re2/wiki/syntax) |```JSON```<br>```{```<br>```   "op": "string_match",```<br>```   "field": "name",```<br>```   "pattern": "^[0-9A-Za-z_]+$"```<br>```}```<br> |
|string_contain |Keyword matching operator. Only for fields of type string.<br><br>Indicates that the field content contains a pattern. |```JSON```<br>```{```<br>```   "op": "string_contain",```<br>```   "field": "name",```<br>```   "pattern": "bar"```<br>```}```<br> |
|enum_freq_limiter |Frequency operator. Only for fields of type string.<br><br>Used to ensure that the total number of occurrences of a particular value in a recall does not exceed the specified `threshold` |```JSON```<br>```{```<br>```  "op": "enum_freq_limiter",```<br>```  "field": "city"```<br>```  "threshold": 5```<br>```}```<br> |


<span id="a51d03bc"></span>
# Example

```Java
// Call the related operation once during the initialization of the program to get the specified index. 
Index index = vikingDBService.getIndex("javaSDKTest", "test_index");
```


```Java
Map stringMatchOp = new HashMap<>();
stringMatchOp.put("op", "string_match");
stringMatchOp.put("field", "f_string");
stringMatchOp.put("pattern", ".*doc[4-9]*$");
// Map stringLikeOp = new HashMap<>();
// stringLikeOp.put("op", "string_contain");
// stringLikeOp.put("field", "f_string");
// stringLikeOp.put("pattern", "doc");
Map enumFreqLimitOp = new HashMap<>();
enumFreqLimitOp.put("op", "enum_freq_limiter");
enumFreqLimitOp.put("field", "f_string");
enumFreqLimitOp.put("threshold", 2);
List datas = index.search(new SearchParam()
             .setScalarOrder(new ScalarOrder("f_int64", "asc").build())
             .setOutputFields(Arrays.asList("f_id", "f_string", "f_int64", "f_float32"))
             .setPartition("default")
             .setPostProcessInputLimit(100)
             .setPostProcessOps(Arrays.asList(stringMatchOp, enumFreqLimitOp))
             .setLimit(3)
             .build());
     for (DataObject data : datas) {
            System.out.println(data);
        }
```


<span id="93456e57"></span>
## Return value

A Java call that performs the above task returns a List. The properties contained in the DataObject instance are shown in the following table.


|**attribute** |**Description** |
|---|---|
|ID |The primary key. |
|Fields |The `fields` field in the response contains the specific data, which is a map. |
|Score |Indicates the degree to which the found vector matches the input vector. |
