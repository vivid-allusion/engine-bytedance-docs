---
title: "Date value processing functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/date_value_processing_functions"
---

This topic describes the syntax and format of date value processing functions and offers sample scenarios.

<span id="dt-str-函数"></span>
## dt_str function

This is a time processing function for converting a date and time value into a time string that uses a specified time zone and a specified format.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
dt_str(value, fmt="Target format", tz=None)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value |String |Yes |/ |/ |Specify a date and time value to be converted. |
|fmt |String |No |/ |/ |Specify a format for the time string to be output. |
|tz |String |No |/ |zone list |Specify a time zone used after conversion. Default value: None. |


<span id="函数示例"></span>
### Sample function


* Scenario: After converting the value of the field `time` in a log into a time value, the function outputs the value to the field `dt_str` according to the format specified by the field `fmt`.

* Transformation rule:

   ```python
   f_set("dt_str", dt_str(v("time"), fmt=v("fmt")))
   ```
   

* Sample log:

   ```json
   {
       "time":"2022-12-26 13:03:21",
       "fmt":"%Y/%m/%d %H-%M-%S"
   }
   ```
   

* Transformation result:

   ```json
   {
       "time":"2022-12-26 13:03:21",
       "fmt":"%Y/%m/%d %H-%M-%S",
       "dt_str":"2022/12/26 13-03-21"
   }
   ```
   


<span id="dt-to-timestamp-函数"></span>
## dt_to_timestamp function

This function converts a time field value to a UTC timestamp based on a specified time zone.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
dt_to_timestamp(value, tz=None)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value |String |Yes |/ |/ |Specify a value to be converted. |
|tz |String |No |/ |zone list |Specify a time zone used after conversion. |


<span id="函数示例"></span>
### Sample function


* Scenario: According to the time zone specified by the field `tz`, the function converts the value of the field `time` in a log into a time value, then outputs the value as a UTC timestamp.

* Transformation rule:

   ```python
   f_set("dt_to_timestamp", dt_to_timestamp(v("time"), v("tz")))
   ```
   

* Sample log:

   ```json
   {
       "time":"2022-12-26 13:03:21",
       "tz":"Asia/Shanghai"
   }
   ```
   

* Transformation result:

   ```json
   {
       "time":"2022-12-26 13:03:21",
       "tz":"Asia/Shanghai",
       "dt_to_timestamp":1672031001
   }
   ```
   


<span id="dt-from-timestamp-函数"></span>
## dt_from_timestamp function

This function converts a timestamp field of the time type into a time value according to the specified time zone, then outputs the value as a time string.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
dt_from_timestamp(value, tz=None)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value |Number |Yes |/ |/ |Specify a value to be converted. |
|tz |String |No |/ |zone list |Specify a time zone used after conversion. |


<span id="函数示例"></span>
### Sample function


* Scenario: According to the time zone specified by the field `tz`, the function converts the value of the field `time` in a log into a time value, then outputs the value as a time string.

* Transformation rule:

   ```python
   f_set("dt_from_timestamp", dt_from_timestamp(v("time"), tz=v("tz")))
   ```
   

* Sample log:

   ```json
   {
       "time":"1672057815"
   }
   ```
   

* Transformation result:

   ```json
   {
       "time":"1672057815",
       "dt_from_timestamp":"2022-12-26 20:30:15"
   }
   ```
   


<span id="dt-now-函数"></span>
## dt_now function

This function gets the local time at which transformation is performed.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
dt_now(tz="")
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|tz |String |No |/ |zone list |Specify a time zone used after conversion. |


<span id="函数示例"></span>
### Sample function


* Scenario: This function gets the local time at which transformation is performed according to the time zone specified by the field `tz` in a log, then outputs the time to the field `dt_now`.

* Transformation rule:

   ```python
   f_set("dt_now", dt_now(tz=v("tz")))
   ```
   

* Sample log:

   ```json
   {
       "tz":"Asia/Shanghai"
   }
   ```
   

* Transformation result:

   ```json
   {
       "tz":"Asia/Shanghai",
       "dt_now":"2022-12-27 19:56:31.223646+08:00"
   }
   ```
