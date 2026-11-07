---
title: "PromQL operators"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/PromQL-operators"
---

PromQL supports various operators, which enable you to perform secondary processing on time series data. These operators include mathematical operators, boolean operators, comparison operators, logical operators, and other operators. This topic describes PromQL operators.

<span id="KHfGqfbG"></span>
## Mathematical operators

Mathematical operators are relatively simple, including basic addition, subtraction, multiplication, and division. For example, you can use `http_response_size_bytes_sum` to query the total bytes of HTTP responses. If you want to use MB as the unit, you can use the following calculation method:

```Plain Text
http_response_size_bytes_sum /1024/1024
```


The following table shows the mathematical operators that are supported in PromQL.


|**Operator** |**Descriptions** |
|---|---|
|+ |Addition |
|\- |Subtraction |
|\* |Multiplication |
|/ |Division |
|% |Modulo |
|^ |Exponentiation |


<span id=".5q-U6L6D6L-Q566X56ym"></span>
## Comparison operators 

Comparison operators allow you to compare sample values in time series with specified values. For example, you can query the number of requests for each API by using `http_requests_total`. If you want to filter out APIs for which the number of requests exceeds 20, you can use the following PromQL expression to compare the value.

```Plain Text
http_requests_total > 20
```


The following table shows the comparison operators that are supported in PromQL.


|**Operator** |**Descriptions** |
|---|---|
|== |Equal to |
|!= |Not equal to |
|\> |Greater than |
|< |Less than |
|\>= |Greater than or equal to |
|<= |Less than or equal to |
