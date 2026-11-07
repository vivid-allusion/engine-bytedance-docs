---
title: "postprocessing operator"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/pysdk_postprocessing_operator"
---

The Postprocessing operator is a post\-retrieval feature in VikingDB that refines search results after the initial vector recall. You can use it to further filter and optimize the candidate data, ensuring the final results are more accurate, relevant, and diverse. This document explains the available operators, their parameters, and provides code examples for implementation.

In VikingDB, postprocessing operators can be used to:


* **Precise screening of results**: Set filtering rules with regular expressions based on business requirements, such as filtering products that contain specific text patterns, to ensure that users get valid search results.

* **Data quality improvement**: Use regular expressions to check the format of search results, filter out data containing special characters, illegal content, or advertising information, and ensure that the returned content meets standards.

* **Search Results Equalization**: Set frequency limits on specific fields to prevent certain values from appearing too frequently in search results, such as popular brands, popular authors, or overexposure of specific categories, and ensure the diversity and fairness of search results.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Postprocessing operators are general\-purpose search capabilities that you can apply to<strong>basic vector search</strong> and<strong>dense\-sparse hybrid retrieval</strong></div>


<span id="27209846"></span>
# Parameter description


|**parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|
|post_process_ops |List\ < map \> |No |*  |List of postprocessing operators. After the vector or scalar recall phase, the candidate data is further filtered, such as string matching, frequency control, etc. Each operator is a map and is executed serially. Default is empty. See postprocessing operators below for details. |
|post_process_input_limit |Int |No |*  |When post_process_ops is set, the number of candidates to enter the post\-processing phase. The default value is 1000, and the maximum value is min (1600, limit \* 10). |


<span id="68cf84c7"></span>
## Postprocessing operator


|Operator |**Description** |Example |
|---|---|---|
|string_match |Regular expression operator. Only for fields of type string.<br><br>For regular expression syntax, please refer to: [Syntax](https://github.com/google/re2/wiki/syntax) |```JSON```<br>```{```<br>```   "op": "string_match",```<br>```   "field": "name",```<br>```   "pattern": "^[0-9A-Za-z_]+$"```<br>```}```<br> |
|string_contain |Keyword matching operator. Only for fields of type string.<br><br>Checks if the field's content contains the specified pattern. |```JSON```<br>```{```<br>```   "op": "string_contain",```<br>```   "field": "name",```<br>```   "pattern": "bar"```<br>```}```<br> |
|enum_freq_limiter |Frequency operator. Only for fields of type string.<br><br>Used to ensure that the total number of occurrences of a particular value in the recall results does not exceed `threshold` times. |```JSON```<br>```{```<br>```  "op": "enum_freq_limiter",```<br>```  "field": "city"```<br>```  "threshold": 5```<br>```}```<br> |


<span id="614201b9"></span>
# Example

```Python
# Retrieve the specified index; call once during program initialization, no need to call repeatedly
index = vikingdb_service.get_index("example_text", "example_index_text")
```


```Python
datas = index.search(order=None, limit=5, post_process_input_limit=5,
                         post_process_ops=[
                             {'op': 'string_like', 'field':'f_string', 'pattern':'%doc9%'},
                             {'op': 'enum_freq_limiter', 'field':'f_string', 'threshold': 1}
                         ])
for data in datas:
        print(data.id, data.fields, data.score)
```
