---
title: "Comparison Function"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/comparison-function"
---

The comparison function always returns 0 or 1 (UInt8).
The following types can be compared:

* Number
* String and FixedString
* Date
* DateTime

Types within each group can be compared with each other, but types from different groups cannot be compared.
For example, you cannot compare a date with a string. You must use a function to convert a string to a date and vice versa.
Strings are compared byte by byte. A shorter string is smaller than all strings that start with it and contain at least one character.
<span id="等于，a-b和a-b-运算符"></span>
## equals to, a=b and a==b operators
<span id="不等于，a-b和a-b-运算符"></span>
## not equals to, a!=b and a<>b operators
<span id="少-运算符"></span>
## Smaller than, < operator
<span id="大于-运算符"></span>
## Bigger than, > operator
<span id="小于等于-运算符"></span>
## Smaller than or equals to, <= operator
<span id="大于等于-运算符"></span>
## Bigger than or equals to, >= operator
