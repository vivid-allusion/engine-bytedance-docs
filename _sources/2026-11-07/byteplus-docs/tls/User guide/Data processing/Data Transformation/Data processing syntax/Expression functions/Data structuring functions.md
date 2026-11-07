---
title: "Data structuring functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/data_structuring_functions"
---

This topic describes the syntax and format of the data structuring function used in data transformation and offers a typical scenario.

<span id="9d01060b"></span>
## if_json function

This function determines whether a string is in standard JSON format. If the specified string is in standard JSON format, True is returned. Otherwise, False is returned.

<span id="3222a648"></span>
### Function syntax and format

```Python
if_json(value)
```


The following table describes the parameters.


|Parameter |Type |Required |Description |
|---|---|---|---|
|value |String |Yes |Specify a string of which the format is to be determined. |


<span id="ba500931"></span>
### Sample function

The function determines whether a specified string is in valid JSON format.


* Transformation rule:

   ```Python
   f_set("if_json",if_json("{"a":"b"}")
   ```
   

* Log:

   ```JSON
   {
       "key": "value"
   }
   ```
   

* Transformation result:

   ```JSON
   {
       "key": "value",
       "if_json": "True"
   }
   ```
