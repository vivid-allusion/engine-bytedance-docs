---
title: "Parsing functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/parsing_functions"
---

A User\-Agent (UA) parsing function discards fields of which the parsing results are None. For example, if the parsed device data is `{'city': None, 'level': 'info', 'error': None}`, the fields `city` and `error` are discarded. In this case, the final parsing result is `{'level': 'info'}`.

<span id="ua-parse-device-函数"></span>
## ua_parse_device function

This function parses device information in a UA string.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
ua_parse_device(value=UA string)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value |String |Yes |/ |/ |Specify a UA string to be parsed. |


<span id="函数示例"></span>
### Sample function


* Scenario: The function extracts device information from the `User-Agent` field in a log.

* Transformation rule:

   ```python
   f_set("device",ua_parse_device(v("ua")))
   ```
   

* Sample log:

   ```json
   {
       "ua":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.0.0 Safari/537.36"
   }
   ```
   

* Transformation result:

   ```json
   {
       "ua":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.0.0 Safari/537.36",
       "device": {
           "family": "Mac",
           "brand": "Apple",
           "model": "Mac"
       }
   }
   ```
   


<span id="ua-parse-os-函数"></span>
## ua_parse_os function

This function parses operating system information in a UA string.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
ua_parse_os(value=UA string)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value |String |Yes |/ |/ |Specify a UA string to be parsed. |


<span id="函数示例"></span>
### Sample function


* Scenario: The function extracts operating system information from the `User-Agent` field in a log.

* Transformation rule:

   ```python
   f_set("os",ua_parse_os(v("ua")))
   ```
   

* Sample log:

   ```json
   {
       "ua":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.0.0 Safari/537.36"
   }
   ```
   

* Transformation result:

   ```json
   {
       "ua":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.0.0 Safari/537.36",
       "os": {
           "family":  "Mac OS X",
           "major":  "10",
           "minor":  "15",
           "patch":  "7"
       }
   }
   ```
   


<span id="ua-parse-agent-函数"></span>
## ua_parse_agent function

This function parses browser information in a UA string.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
ua_parse_agent(value=UA string)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value |String |Yes |/ |/ |Specify a UA string to be parsed. |


<span id="函数示例"></span>
### Sample function


* Scenario: The function extracts agent information from the `User-Agent` field in a log.

* Transformation rule:

   ```python
   f_set("agent",ua_parse_agent(v("ua")))
   ```
   

* Sample log:

   ```json
   {
       "ua":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.0.0 Safari/537.36"
   }
   ```
   

* Transformation result:

   ```json
   {
       "ua":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.0.0 Safari/537.36",
       "agent": {
           "family": "Chrome",
           "major": "115",
           "minor": "0",
           "patch": "0"
       }
   }
   ```
