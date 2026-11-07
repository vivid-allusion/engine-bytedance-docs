---
title: "Data transformation syntax"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/data_transformation_syntax"
---

Torch Log Service (TLS) Domain Specific Language (DSL) supports more than 40 built\-in functions to implement data transformation jobs.

<span id="语法介绍"></span>
### Syntax introduction

TLS DSL is a log transformation language with Python\-like syntax. In addition to the basic data structure, the syntax rules are orchestrated in the form of function combinations.


|Category |Module |Description |
|---|---|---|
|Data structure |Number, string, and Boolean |TLS DSL supports this module. Strings in the form of`"""` are not supported. |
||list and dictionary |TLS DSL supports this module. |
|Basic syntax |Operators |TLS DSL does not support this module. This module can be supported through functions in an indirect manner. |
||Comments |TLS DSL supports comments starting with number signs ( # ). |
||Variable assignment |TLS DSL does not support this module. This module can be passed through function calls, such as `f_set(xxx, "value")`. |
||Condition evaluation |TLS DSL supports functions with conditional semantics, such as`c_if`, `c_if_else`, and `c_switch`. |
||Loops |TLS DSL does not support this module. |
|Function |define function, lambda |TLS DSL does not support this module. |
||Function calls |You can call functions offered by TLS DSL. |


<span id="函数分类"></span>
### **Function types**

TLS DSL functions are mainly divided into two categories:


* Global processing functions: mainly control flows, receive logs, process logs, and return logs.

* Expression functions: accept parameters with specific data structures and return values after combined calls. You can pass the call result of an expression function as a parameter to a global processing function, thus defining flexible transformation logic.


The following table compares the preceding function categories:


|Function Type |Global Step |Return Value |Log Modification |
|---|---|---|---|
|Global processing functions |Supported |Zero or more logs |Supported |
|Expression functions |Not supported |Specific data structure |Not supported |
