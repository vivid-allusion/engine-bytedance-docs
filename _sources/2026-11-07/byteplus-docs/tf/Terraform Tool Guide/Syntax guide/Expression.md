---
title: "Expression"
product: "Terraform"
product_code: "tf"
source: "https://docs.byteplus.com/en/docs/tf/Expressions"
---

<span id=".6L-Q566X56ym"></span>
## Operators

Operators are symbols that compilers use to perform specific numerical or logical operations.


* Arithmetic operators: The operands and results are all numbers. Supported arithmetic operators: +, \- (subtraction), \*, /, (), %, \- (negative numbers).

* Comparison operators: The operands are numbers while the results are boolean values. Supported comparison operators: ==, !=, \>, \>=, <, <=.

* Logical operators: The operands and results are all boolean values. Supported logical operators: ||, &&, !.


When operators appear in the same expression, their priorities are as follows:


1. !, \- (negative numbers)

2. \*，/，%

3. +, \- (subtraction)

4. \>，\>=，<，<=

5. ==，!=

6. &&

7. ||


<span id=".5p2h5Lu26KGo6L6-5byP"></span>
## Conditional expression

A conditional expression evaluates the result of a boolean expression to select one of two options.

For example,

```Plain Text
condition ? one_value : two_value
```


The result is one_value if `condition` is true, and the result is two_value if condition is false.

<span id=".Zm9y6KGo6L6-5byP"></span>
## For expression

A for expression iterates through a group of [elements of a complex Type](https://docs.byteplus.com/en/docs/tf/Basic-syntax#复合类型) to process the elements and outputs another group of elements of a new complex type.

For example,

```Plain Text
[for item in items : upper(item)]
```


All values in items are converted to uppercase.

<span id=".5Ye95pWw6KGo6L6-5byP"></span>
## Function expression

Use some built\-in functions while computing expressions, and function call expressions are similar to actions. For example: `upper("123")`.
