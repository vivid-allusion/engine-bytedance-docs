---
title: "Difference Pattern Statistical Function"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Difference-Pattern-Statistical-Function"
---

This topic describes the syntax of difference pattern statistical functions supported by Torch Log Service and usage examples in common scenarios.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, the machine learning functions are in public beta.</div>


<span id="66167641"></span>
## Function list


|Function |Description |
|---|---|
|pattern_diff |Based on the given field samples and judgment conditions, analyze the set of difference patterns defined by these conditions. |


<span id="4e0fafb1"></span>
## pattern_diff

<span id="df99f2d9"></span>
### Function syntax


* Syntax format

   ```SQL
   pattern_diff(array_char_value, array_char_name, array_numeric_value, array_numeric_name, condition, supportScore,posSampleRatio,negSampleRatio ) 
   ```
   

* Parameter description

   
   |Parameter |Data type |Description |
   |---|---|---|
   |array_char_value |Array |The input column for character data.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>array_char_value</code>and <code>array_numeric_value</code>cannot be empty at the same time.</div><br> |
   |array_char_name |Array |The name of the input column for character data. |
   |array_numeric_value |Array |The input column for numeric data. |
   |array_numeric_name |Array |The name of the input column for numeric data. |
   |condition |String |The conditions for filtering data. If the condition is true, it is a positive sample; if the condition is false, it is a negative sample. |
   |supportScore |Double |The support degree of positive and negative samples during pattern mining. The value range is (0, 1]. |
   |posSampleRatio |Double |The sampling rate of positive samples. The default value is 0.5, which means only 50% of the positive sample set is taken. The value range is (0, 1]. |
   |negSampleRatio |Double |The sampling rate of negative samples. The default value is 0.5, which means only 50% of the negative sample set is taken. The value range is (0, 1]. |
   

* Return value description

   If the input value is null, null will be returned.


<span id="4be71ab8"></span>
### Function example

Query and analysis statements

```SQL
 * | select pattern_diff(array[client_ip], array['client_ip'], array[stamp,value], array['stamp','value' ], ReqSize > 2000, 0.1,0.1,
      0.1) from (select client_ip, stamp,value,ReqSize,RespSize limit 10000)
```
