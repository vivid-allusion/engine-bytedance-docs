---
title: "Configuring Data Source Mappings"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configuring-data-source-mappings"
---

When syncing third\-party data sources, administrators must configure an employee synchronization mapping policy. This policy is divided into two types: **Data Field Mapping** and **Expression Mapping**. This article introduces both mapping methods and focuses on how to configure Expression Mapping.

<span id="ab3e92d2"></span>
# Introduction

When adding a data source on the **Identity** \> **Account Setup** \> **Directory Sync** page in the Admin Console, administrators must configure the mapping relationship between the third\-party data source fields and the internal SealSuite fields. This allows the enterprise to specify which data needs to be synchronized.

The configuration supports two mapping rules: **Data** **Field Mapping** and **Expression Mapping**.


|**Mapping Rule** |**Description** |
|---|---|
|**Data Field Mapping** |During synchronization, SealSuite retrieves the organizational structure fields from the third\-party data source. Through Data Field Mapping, you can map these third\-party fields to the corresponding SealSuite fields, ensuring that the specified data is transferred into SealSuite during the sync process. For example, by mapping the third\-party field for employee ID (user_id) to the SealSuite field for employee ID (user_id), the employee's ID in SealSuite will remain consistent with their ID in the original platform after synchronization.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Data Field Mapping is supported for both Upstream Synchronization and Downstream Synchronization when adding a data source.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can add extended fields for third\-party data sources. For details, see <a href="https://docs.byteplus.com/docs/sealsuite/docs-configuring-custom-attributes">Configuring custom attributes</a>.</div><br> |
|**Expression Mapping** |Expression Mapping is used to dynamically generate values from third\-party fields and map them to a specified SealSuite field. By flexibly combining expressions and third\-party fields, you can generate a wide variety of data formats.<br><br><br>* **Expressions**: For the expression syntax supported by SealSuite, refer to the [Expression Syntax](https://docs.byteplus.com/docs/sealsuite/configuring-data-source-mappings#4e89f04d) section below.<br><br>* **Third Party Fields**: These are the fields passed from the upstream third\-party data source to SealSuite.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Expression Mapping is only supported for Upstream Synchronization when adding a data source.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">An expression can contain one or more third\-party fields, or it can be composed solely of an expression without any third\-party fields.</div><br><br><br><br>**Example Usage**:<br><br>When syncing an upstream data source to SealSuite, suppose you need to replace employees' old email addresses with new ones, where the new email address prefix is the employee's ID (user_id). You can set the expression in the email mapping field to `user_id + "@example.com".` After synchronization, all employee emails in SealSuite will be updated to the new format, such as `123456@example.com`. |


<span id="4e89f04d"></span>
# Expression Syntax

This section summarizes the supported expression syntax. You can use it as a reference when creating your own expressions.

<span id="230c490a"></span>
## Literals

Literals are used to represent fixed values in an expression. The following literals are supported.


|**Literal** |**Description** |
|---|---|
|**Comment** |Used to add notes about the expression's logic. The format is /\* \*/ or //. |
|**Boolean** |Boolean values, which can be `true` or `false`. |
|**Integer** |Integer values. Examples:<br><br><br>* Binary: 0b101010<br><br>* Octal: 0o52<br><br>* Decimal: 42<br><br>* Hexadecimal: 0x2A |
|**Float** |Floating\-point numbers. Example: 0.5 (can also be written as .5). |
|**String** |String values. Examples: "foo", 'bar'. |
|**Array** |Arrays. Example: [1, 2, 3]. |
|**Map** |A collection of key\-value pairs. Example: {a: 1, b: 2, c: 3}. |
|**Nil** |The nil value, represented by nil. |


<span id="d099c0b8"></span>
## Operators

The following operators are supported in expressions.


|**Operator** |**Description** |
|---|---|
|Arithmetic Operators |* `+`: Addition<br><br>* `-`: Subtraction<br><br>* `*`: Multiplication<br><br>* `/`: Division<br><br>* `%`: Modulo<br><br>* `^` or `**`: Power |
|Comparison Operators |* `==`: Equal<br><br>* `!=`: Note equal<br><br>* `<`: Less than<br><br>* `>`: Greater than<br><br>* `<=`: Less than or equal to<br><br>* `>=`: Greater than or equal to |
|Logical Operators |* `not` or `!`: Logical NOT<br><br>* `and` or `&&`: Logical AND<br><br>* `or` or `\|\|`: Logical OR |
|Conditional Operators |* `?:`: Ternary operator. Format: `condition ? true : false`. Returns true if the condition is met, otherwise returns `false`.<br><br>* `??`: Nil\-coalescing operator. Format: value `?? default_value`. Returns value if it is not nil and defined, otherwise returns default_value. |
|Member Operators |Includes `[]`, `.`, `?.`, and `in` operators.<br><br><br>* Fields of a struct can be accessed with `[]` or `.`. The following are equivalent:<br><br>   ```Go```<br>```   user.Name```<br>```   user["Name"]```<br>```   ```<br>   <br><br>* Array elements can be accessed with `[]`. Negative indices are supported (\-1 is the last element).<br><br>   ```Go```<br>```   array [0] // First element```<br>```   array [-1] // Last element```<br>```   ```<br>   <br><br>* The`in` operator checks for the presence of an item in an array or a key in a map.<br><br>   ```Go```<br>```   "John" in ["John", "Jane"]```<br>```   "name" in {"name": "John", "age": 30}```<br>```   ```<br>   <br><br>* The`?.` operator (optional chaining) checks if a field is `nil` before access. If it is `nil`, the expression returns `nil`.<br><br>   ```Go```<br>```   author.User?.Name```<br>```   ```<br>   <br><br>   Returns the value of `author.User.Name` if `author.User` is not `nil`, and `nil` otherwise.<br><br>   ```Go```<br>```   author.User != nil ? author.User.Name : nil```<br>```   ```<br>   <br><br>* Combine `?.` with `??` to provide a default value for `nil` cases.<br><br>   ```Go```<br>```   author.User?.Name ?? "Anonymous"```<br>```   ```<br>   <br><br>   Returns the value of `author.User.Name` if `author.User` is not `nil`, and `"Anonymous"` otherwise.<br><br>   ```Go```<br>```   author.User?.Name ?? "Anonymous"```<br>```   ```<br>    |
|String Operators |* `+`: String concatenation.<br><br>* `contains`: Checks if a string contains a substring (returns boolean).<br><br>* `startsWith`: Checks if a string starts with a substring (returns boolean).<br><br>* `endsWith`: Checks if a string ends with a substring (returns boolean). |
|Regular Expression |`matches` |
|Range Operator |`..`: Creates a range of integers.<br><br>```Go```<br>```1..3 == [1, 2, 3]```<br> |
|Array Slicing |`[start:end]`: Extracts a subarray. `start` is inclusive, `end` is exclusive.<br><br>Example with array = [1, 2, 3, 4, 5].<br><br>```Go```<br>```array[1:3] == [2, 3]```<br>```array[1:-1] == [2, 3, 4]```<br>```array[:3] == [1, 2, 3]```<br>```array[3:] == [4, 5]```<br>```array[:] == array```<br> |
|Pipe Operator |`\|`: Pipes the output of the left expression into the right expression as its first argument.<br><br>```Go```<br>```// 1. Pass the value of the user.Name field to the lower() function.```<br>```// 2. Pass the resulting lowercase string to the split() function, which splits it by spaces.```<br>```user.Name```<br> |


<span id="3059f37d"></span>
## Variables

You can declare variables within an expression using the `let` keyword. Variable names must start with a letter or underscore (_) and can contain letters, numbers, and underscores.

```Go
let x = 42; x * 2
```


Multiple variables can be separated by semicolons.

```Go
let x = 42;
let y = 2;
x * y
```


Variable values can be expressions themselves.

```Go
let name = user.Name | lower() | split(" ");
"Hello, " + name[0] + "!"
```


<span id="f2c81bb0"></span>
## Predicates

Predicates such as `filter`, `all`, `any`, `one`, and `none` can be applied in expressions. The following example creates an array from 0 to 9 and then filters it for even numbers.

```Go
filter(0..9, {# % 2 == 0})
```


If an array item is a struct or map, you can omit the `#` to access fields. For example, `*.Value` can be written as `.Value`.

```Go
filter(tweets, {len(.Content) > 240})
```


The curly braces `{}` can also be omitted:

```Go
filter(tweets, len(.Content) > 240)
```


<span id="73d26e57"></span>
## String Functions

<span id="df7f6cb3"></span>
### trim(str[, chars])

Removes whitespace from both ends of the string `str`. The `chars` argument is optional and specifies a set of characters to remove.

```Go
trim("  Hello  ") == "Hello"      // Removes whitespace
trim("__Hello__", "_") == "Hello" // Removes underscores
```


<span id="60866b81"></span>
### trimPrefix(str, prefix)

Removes the specified `prefix` from the beginning of `str` if it exists.

```Go
trimPrefix("HelloWorld", "Hello") == "World"
```


<span id="b2b07611"></span>
### trimSuffix(str, suffix)

Removes the specified `suffix` from the end of `str` if it exists.

```Go
trimSuffix("HelloWorld", "World") == "Hello"
```


<span id="ea53aba9"></span>
### upper(str)

Converts all characters in `str` to uppercase.

```Go
upper("hello") == "HELLO"
```


<span id="c4439bf2"></span>
### lower(str)

Converts all characters in `str` to lowercase.

```Go
lower("HELLO") == "hello"
```


<span id="a9cce58d"></span>
### split(str, delimiter[, n])

Splits `str` by the `delimiter` and returns an array of substrings. The optional `n` limits the number of splits.

```Go
split("apple,orange,grape", ",") == ["apple", "orange", "grape"]
split("apple,orange,grape", ",", 2) == ["apple", "orange,grape"]
```


<span id="3fc60d8a"></span>
### splitAfter(str, delimiter[, n])

Splits `str` after each `delimiter`.

```Go
splitAfter("apple,orange,grape", ",") == ["apple,", "orange,", "grape"]
splitAfter("apple,orange,grape", ",", 2) == ["apple,", "orange,grape"]
```


<span id="5839f36b"></span>
### replace(str, old, new)

Replaces all occurrences of `old` with `new` in `str`.

```Go
replace("Hello World", "World", "Universe") == "Hello Universe"
```


<span id="404f8c5d"></span>
### repeat(str, n)

Repeats `str` `n` times.

```Go
repeat("Hi", 3) == "HiHiHi"
```


<span id="fb0995e1"></span>
### indexOf(str, substring)

Returns the index of the first occurrence of `substring` in `str`, or `-1` if not found.

```Go
indexOf("apple pie", "pie") == 6
```


<span id="e085d1ac"></span>
### lastIndexOf(str, substring)

Returns the index of the last occurrence of `substring` in `str`, or `-1` if not found.

```Plain
    lastIndexOf("apple pie apple", "apple") == 10
```


<span id="55147b1e"></span>
### hasPrefix(str, prefix)

Returns `true` if `str` starts with the given `prefix`.

```Go
hasPrefix("HelloWorld", "Hello") == true
```


<span id="020b9fd8"></span>
### hasSuffix(str, suffix)

Returns `true` if `str` ends with the given `suffix`.

```Go
hasSuffix("HelloWorld", "World") == true
```


<span id="157518f7"></span>
## Date Functions

Includes built\-in support for the [Go time package](https://pkg.go.dev/time).


* Subtract two dates to get a duration:


```Go
createdAt - now()
```



* Add a duration to a date:


```Go
createdAt + duration("1h")
```



* Compare dates:


```Go
createdAt > now() - duration("1h")
```


<span id="c912ed2f"></span>
### now()

Returns the current date and time, corresponding to Go's [time.Time](https://pkg.go.dev/time#Time).

```Go
now().Year() == 2024
```


<span id="240a2978"></span>
### duration(str)

Parses a duration string, corresponding to Go's [time.Duration](https://pkg.go.dev/time#Duration). Valid units: ns, us, ms, s, m, h.

```Go
duration("1h").Seconds() == 3600
```


<span id="ab39c7b6"></span>
### date(str[, format[, timezone]])

Converts a string `str` to a date object.


* If `format` is provided, it uses the specified layout from Go's [time](https://pkg.go.dev/time#pkg-constants) package.

* If `timezone` is provided, it sets the time zone.

* If no `format` is provided, `str` must be one of the following formats:

   * 2006\-01\-02

   * 15:04:05

   * 2006\-01\-02 15:04:05

   * RFC3339

   * RFC822, RFC850, RFC1123


```Go
date("2023-08-14")
date("15:04:05")
date("2023-08-14T00:00:00Z")
date("2023-08-14 00:00:00", "2006-01-02 15:04:05", "Europe/Zurich")
```


Available methods on a date object:


* `Year()`, `Month()`, `Day()`, `Hour()`, `Minute()`, `Second()`, `Weekday()`, `YearDay()`. For more, see [time.Time](https://pkg.go.dev/time#Time).


```Go
date("2023-08-14").Year() == 2023
```


<span id="02edb387"></span>
### timezone(str)

Returns a time zone location.

```Go
timezone("Europe/Zurich")
timezone("UTC")
```


Use the [In()](https://pkg.go.dev/time#Time.In) method to convert a date to a different time zone.

```Go
date("2023-08-14 00:00:00").In(timezone("Europe/Zurich"))
```


<span id="fb027bf0"></span>
## Numeric Functions

<span id="3e29a41a"></span>
### max(n1, n2)

Returns the greater of `n1` and `n2`.

```Go
max(5, 7) == 7
```


<span id="dddc8c40"></span>
### min(n1, n2)

Returns the smaller of `n1` and `n2`.

```Go
min(5, 7) == 5
```


<span id="73f3fb92"></span>
### abs(n)

Returns the absolute value of `n`.

```Go
abs(-5) == 5
```


<span id="971b75da"></span>
### ceil(n)

Returns the least integer value greater than or equal to `n`.

```Go
ceil(1.5) == 2.0
```


<span id="36c8ccd4"></span>
### floor(n)

Returns the greatest integer value less than or equal to `n`.

```Go
floor(1.5) == 1.0
```


<span id="c5d96d95"></span>
### round(n)

Returns the nearest integer, rounding half to even.

```Go
round(1.5) == 2.0
```


<span id="db4727de"></span>
## Array Functions

Array functions are often used with predicates. See [Predicates](https://docs.byteplus.com/docs/sealsuite/configuring-data-source-mappings#f2c81bb0).

<span id="372674c4"></span>
### all(array, predicate)

Returns true if all elements satisfy the predicate. Returns true for an empty array.

```Go
all(tweets, {.Size < 280})
```


<span id="60092b3d"></span>
### any(array, predicate)

Returns true if at least one element satisfies the predicate. Returns true for an empty array.

```Go
any(tweets, {.Size > 280})
```


<span id="b85a8b2f"></span>
### one(array, predicate)

Returns true if exactly one element satisfies the predicate. Returns true for an empty array.

```Go
one(participants, {.Winner})
```


<span id="0afdbcc7"></span>
### none(array, predicate)

Returns true if no elements satisfy the predicate. Returns true for an empty array.

```Go
none(tweets, {.Size > 280})
```


<span id="e62b4638"></span>
### map(array, predicate)

Applies the predicate to each element and returns a new array.

```Go
map(tweets, {.Size})
```


<span id="c0688ff1"></span>
### filter(array, predicate)

Filters array elements using the predicate and returns a new array.

```Go
filter(users, .Name startsWith "J")
```


<span id="ba47df49"></span>
### find(array, predicate)

Finds the first element in the array that satisfies the predicate.

```Go
find([1, 2, 3, 4], # > 2) == 3
```


<span id="81a8c5e7"></span>
### findIndex(array, predicate)

Finds the index of the first element that satisfies the predicate.

```Go
findIndex([1, 2, 3, 4], # > 2) == 2
```


<span id="d30fe76c"></span>
### findLast(array, predicate)

Finds the last element in the array that satisfies the predicate.

```Go
findLast([1, 2, 3, 4], # > 2) == 4
```


<span id="2a4f89c8"></span>
### findLastIndex(array, predicate)

Finds the index of the last element that satisfies the predicate.

```Go
findLastIndex([1, 2, 3, 4], # > 2) == 3
```


<span id="f9c5fd23"></span>
### groupBy(array, predicate)

Groups array elements based on the predicate.

```Go
groupBy(users, .Age)
```


<span id="15a5ce49"></span>
### count(array[, predicate])

Returns the number of elements that satisfy the predicate.

```Go
count(users, .Age > 18)
```


Equivalent to:

```Go
len(filter(users, .Age > 18))
```


<span id="1ce03ad6"></span>
### concat(array1, array2[, ...])

Concatenates two or more arrays.

```Go
concat([1, 2], [3, 4]) == [1, 2, 3, 4]
```


<span id="a6ccf065"></span>
### join(array[, delimiter])

Joins elements of a string array with a delimiter.

```Go
join(["apple", "orange", "grape"], ",") == "apple,orange,grape"
join(["apple", "orange", "grape"]) == "appleorangegrape"
```


<span id="cdde6c7e"></span>
### reduce(array, predicate[, initialValue])

Reduces an array to a single value by applying a predicate. The optional `initialValue` sets the initial value of the accumulator.

Supported variables in the predicate:


* `#`: current element

* `#acc`: accumulator

* `#index`: current index


```Go
reduce(1..9, #acc + #)
reduce(1..9, #acc + #, 0)
```


<span id="d2119576"></span>
### sum(array[, predicate])

Returns the sum of all numbers in an array.

```Go
sum([1, 2, 3]) == 6
```


If a predicate is provided, it is applied to each element before summing.

```Go
sum(accounts, .Balance)
```


Equivalent to:

```Go
reduce(accounts, #acc + .Balance, 0)
// or
sum(map(accounts, .Balance))
```


<span id="5527d0ae"></span>
### mean(array)

Returns the average of all numbers in an array.

```Go
mean([1, 2, 3]) == 2.0
```


<span id="63979bf1"></span>
### median(array)

Returns the median of all numbers in an array.

```Go
median([1, 2, 3]) == 2.0
```


<span id="d94aa80b"></span>
### first(array)

Returns the first element of an array. Returns `nil` if the array is empty.

```Go
first([1, 2, 3]) == 1
```


<span id="963274f0"></span>
### last(array)

Returns the last element of an array. Returns `nil` if the array is empty.

```Go
last([1, 2, 3]) == 3
```


<span id="6de7a44f"></span>
### take(array, n)

Returns the first `n` elements of an array.

```Go
take([1, 2, 3, 4], 2) == [1, 2]
```


<span id="cf0aaa5d"></span>
### reverse(array)

Reverses the order of elements in an array.

```Go
reverse([3, 1, 4]) == [4, 1, 3]
```


<span id="79fa2cbe"></span>
### sort(array[, order])

Sorts the elements of an array in ascending order.

```Go
sort([3, 1, 4]) == [1, 3, 4]
sort([3, 1, 4], "desc") == [4, 3, 1]
```


<span id="b5eab289"></span>
### sortBy(array[, predicate, order])

Sorts array elements based on a predicate. The optional `order` can be `asc` or `desc`.

```Go
sortBy(users, .Age)
sortBy(users, .Age, "desc")
```


<span id="b092c4cc"></span>
## Map Functions

<span id="5dc14d87"></span>
### keys(map)

Returns all keys from a map.

```Go
keys({"name": "John", "age": 30}) == ["name", "age"]
```


<span id="9fa95698"></span>
### values(map)

Returns all values from a map.

```Go
values({"name": "John", "age": 30}) == ["John", 30]
```


<span id="e93ad115"></span>
## Type Conversion Functions

<span id="e4af445e"></span>
### type(v)

Returns the data type of the given value `v`. Possible values include `nil`, `bool`, `int`, `uint`, `float`, `string`, `array`, `map`, or the struct type name.

```Go
type(42) == "int"type("hello") == "string"type(now()) == "time.Time"
```


<span id="4c18517a"></span>
### int(v)

Returns the integer value of a number or string.

```Go
int("123") == 123
```


<span id="8f7d1ff5"></span>
### float(v)

Returns the float value of a number or string.

```Go
float("123.45") == 123.45
```


<span id="ed59b97b"></span>
### string(v)

Converts the given value `v` to a string.

```Go
string(123) == "123"
```


<span id="51991683"></span>
### toJSON(v)

Converts the given value `v` to a JSON string.

```Go
toJSON({"name": "John", "age": 30})
```


<span id="35beecc9"></span>
### fromJSON(v)

Parses a given JSON string `v` and returns the corresponding value.

```Go
fromJSON('{"name": "John", "age": 30}')
```


<span id="17148d85"></span>
### toBase64(v)

Encodes the string `v` into Base64 format.

```Go
toBase64("Hello World") == "SGVsbG8gV29ybGQ="
```


<span id="9a86c5f8"></span>
### fromBase64(v)

Decodes a Base64 encoded string `v` back to its original form.

```Go
fromBase64("SGVsbG8gV29ybGQ=") == "Hello World"
```


<span id="92362a09"></span>
### toPairs(map)

Converts a map into an array of key\-value pairs.

```Go
toPairs({"name": "John", "age": 30}) == [["name", "John"], ["age", 30]]
```


<span id="e5141f8a"></span>
### fromPairs(array)

Converts an array of key\-value pairs into a map.

```Go
fromPairs([["name", "John"], ["age", 30]]) == {"name": "John", "age": 30}
```


<span id="98b1a9e6"></span>
## Other Functions

<span id="cc821558"></span>
### len(v)

Returns the length of an array, map, or string.

```Go
len([1, 2, 3]) == 3len({"name": "John", "age": 30}) == 2len("Hello") == 5
```


<span id="d1060cf4"></span>
### get(v, index)

Retrieves an element from an array or map by its index or key. Returns `nil` if the index is out of bounds or the key does not exist.

```Go
get([1, 2, 3], 1) == 2get({"name": "John", "age": 30}, "name") == "John"
```


<span id="1fcfddf0"></span>
## Bitwise Functions

<span id="9124b9a1"></span>
### bitand(int, int)

Returns the bitwise AND result.

```Go
bitand(0b1010, 0b1100) == 0b1000
```


<span id="0128776f"></span>
### bitor(int, int)

Returns the bitwise OR result.

```Go
bitor(0b1010, 0b1100) == 0b1110
```


<span id="eca274be"></span>
### bitxor(int, int)

Returns the bitwise XOR result.

```Go
bitxor(0b1010, 0b1100) == 0b110
```


<span id="7bc0ad7d"></span>
### bitnand(int, int)

Returns the bitwise AND NOT result.

```Go
bitnand(0b1010, 0b1100) == 0b10
```


<span id="df283ca2"></span>
### bitnot(int)

Returns the bitwise NOT result.

```Go
bitnot(0b1010) == -0b1011
```


<span id="175ad87c"></span>
### bitshl(int, int)

Returns the left shift result.

```Go
bitshl(0b101101, 2) == 0b10110100
```


<span id="9c57b570"></span>
### bitshr(int, int)

Returns the right shift result.

```Go
bitshr(0b101101, 2) == 0b1011
```


<span id="8bfcae85"></span>
### bitushr(int, int)

Returns the unsigned right shift result.

```Go
bitushr(-0b101, 2) == 4611686018427387902
```
