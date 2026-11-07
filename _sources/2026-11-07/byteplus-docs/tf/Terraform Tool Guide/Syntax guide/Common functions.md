---
title: "Common functions"
product: "Terraform"
product_code: "tf"
source: "https://docs.byteplus.com/en/docs/tf/Common-functions"
---

This article introduces the common functions you may encounter when using Terraform. For more types of functions, please refer to [the Terraform official website](https://www.terraform.io/language/functions).

<span id=".5pWw5YC85Ye95pWw"></span>
## Numeric functions


|Function |Description |Example Value |Result |
|---|---|---|---|
|abs |Returns the absolute value. |abs(\-1024) |1024 |
|ceil |Returns the closest whole number that is greater than or equal to the given value. |ceil(5.5) |6 |
|floor |Returns the closest whole number that is less than or equal to the given value. |floor(4.5) |4 |
|log |Calculates the logarithm. |log(16,2) |4 |
|pow |Calculates an exponent by raising the first argument to the power of the second argument. |pow(3,2) |9 |
|max |Returns the maximum value. |max(10,50,3) |50 |
|min |Returns the minimum value. |min(10,50,3) |3 |


<span id=".5a2X56ym5Liy5Ye95pWw"></span>
## String functions


|Function |Description |Example Value |Result |
|---|---|---|---|
|chomp |Removes newline characters at the end of a string. |chomp("hello\n") |"hello" |
|format |Formats strings. |format("Hello, %s!", "abc") |"Hello, abc!" |
|lower |Converts all letters in a string to lowercase. |lower("HELLO") |"hello" |
|upper |Converts all letters in a string to uppercase. |upper("hello") |"HELLO" |
|replace |Replaces a specified character in a string. |replace("1+2+3", "+","\-") |"1\-2\-3" |
|join |Concatenates the elements in a list to a string using the specified delimiter. |join(",", "one","two","three"]) |"one,two,three" |
|split |Splits a list into strings using the specified delimiter. |split(", ","One,Two,Three") |["One","Two","Three"] |
|substr |Extracts a substring from the specified string using an offset and length. |substr("hello world!",0,3) |hell |


<span id=".6ZuG5ZCI5Ye95pWw"></span>
## Collection functions


|Function |Description |Example Value |Result |
|---|---|---|---|
|element |Gets the value of an element in a list by the index of the element. |element(["One","Two","Three"],2) |Three |
|index |Gets the index of an element in a list by the value of the element. If the element value does not exist, this function returns an error. |index(["a","b","c"],"b") |1 |
|lookup |Retrieve the value of the specified key from the list. If the key does not exist, return the default value. |lookup({a="A",b="B"},"a","C")<br><br>lookup({a="A",b="B"}, "c","C") |A<br><br>C |
|keys |Returns all keys of a list. |keys({a=1,b=2,c=3}) |["a","b","c"] |
|flatten |Flattens all nested elements of a list. |flatten([["a","b"],[],["c"]]) |["a","b","c"] |
|length |Gets the length of a list, map, or string. |length(["a","b","c"])<br><br>length({a="A",b="B"})<br><br>length("Hello,world") |3<br><br>2<br><br>11 |


<span id=".57G75Z6L6L2s5o2i5Ye95pWw"></span>
## Type conversion functions


|Function |Description |Example Value |Result |
|---|---|---|---|
|toset |Converts a list to a set. |toset(["a","b","a"]) |["a","b"] |
|tolist |Converts a set to a list. |toset(["a","b","c"]) |["a","b","c"] |
|tonumber |Converts a string to a number. |tonumber("1") |1 |
|tostring |Converts a number to a string. |tostring(1) |"1" |
