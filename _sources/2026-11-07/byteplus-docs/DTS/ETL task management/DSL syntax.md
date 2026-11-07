---
title: "DSL syntax"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/dsl_syntax"
---

DSL is a script language designed by DTS based on the LISP\-1 standard for data processing needs in data synchronization scenarios. DTS uses the DSL script language to extract, transform, process, and load strings, dates, and numerical values in data.

<span id=".ZHNsLeivreazleeJueaApw=="></span>
## DSL syntax features

DSL syntax includes the following features:


* Powerful: Supports a large number of function combinations.

* Efficient: DSL execution has no extra runtime overhead, causing minimal performance loss during synchronization.

* Simple syntax: Provides typical scenarios such as data filtering, data transformation, and data desensitization, which you can refer to when setting your custom script language. For details, refer to [Application scenarios](https://docs.byteplus.com/en/docs/DTS/brief_introduction_to_etl).


<span id=".5pWw5o2u57G75Z6L"></span>
## Data type


|**Type** |**Description** |**Sample** |
|---|---|---|
|int |An integer, representing a number without a decimal part, can be positive, negative, or zero. |123 |
|float |Float type, representing values with a decimal part. |3.14 |
|string |string. |"abc" |
|char |Character type, representing a single character. |#a |
|bool |Boolean type, indicating true or false value. |true or false |
|bytes |Represents a hexadecimal string starting with 0B. |0B37 |
|symbol |Indicates a string without quotes. |abc |
|time |indicates time type. |(time/parse\-beijing "2015\-02\-23 23:54:55") |


<span id=".6KGo6L6-5byP57G75Z6L"></span>
## Expression type


|**Type** |**Expression** |**Description** |
|---|---|---|
|Array |```sql```<br>```[参数1 参数2 参数3 ...]```<br> |An array is a sequence of elements enclosed in square brackets. For example:<br><br><br>* `[1 2 3]`: Represents an integer array.<br><br>* `["a" "b" "c"]`: Represents a string array. |
|Hash |```sql```<br>```{key1  value1  key2  value2}```<br> |A hash is a series of elements enclosed in curly braces. Odd\-position elements are keys, followed by even\-position elements as values. For example:<br><br>```sql```<br>```{"a" 1 "b" 2 }```<br><br><br>Indicates `key1` is `a`, `value1` is `1`; `key2` is `b`, `value2` is `2`. |
|Function call |```sql```<br>```(function-name 参数1 参数2 参数3 ...)```<br> |A function call is a series of elements enclosed in parentheses. For example:<br><br>```sql```<br>```(+ 1 2)```<br> |
|Quoting |```sql```<br>```'(参数1 参数2 参数3 ...)```<br> |Use single quotation marks `'` to mark the list as data, indicating a data list instead of a function call. For example:<br><br>```sql```<br>```'(1 2 3)```<br> |
|Function definition |```sql```<br>```(defn 函数名 [参数1 参数2 ...]```<br>```  函数体)```<br> |Define a function using `defn`. For example, define a function to calculate the square:<br><br>```sql```<br>```(defn square [x]```<br>```  (* x x))```<br> |
|Variable binding |```sql```<br>```(let [变量1  值1  变量2  值2 ...]```<br>```  使用变量的表达式)```<br> |Use the keyword `let` for variable binding. For example, print the values of variables a and b:<br><br>```sql```<br>```(let [a 100 b 200]```<br>```   (println a b))```<br><br><br>Return `100 200`. |


<span id=".5Ye95pWw57G75Z6L"></span>
## Function type

DTS supports ETL\-based development of DSL script language, as shown below.

<span id=".5YaF572u5Ye95pWw"></span>
### Built\-in function


* Expression function

   * Numerical operation

      
      |**Function** |**Syntax** |**Value range** |**Return value** |
      |---|---|---|---|
      |Addition |```sql```<br>```(+  value1   value2 )```<br> |The value ranges of value1 and value2 include integers or floating\-point numbers. |Return integers when all parameters are integers, otherwise return a floating\-point number. |
      |Subtraction |```sql```<br>```(-  value1   value2)```<br> |The value ranges of value1 and value2 include integers or floating\-point numbers. |Return integers when all parameters are integers, otherwise return a floating\-point number. |
      |Multiplication |```sql```<br>```(*  value1   value2)```<br> |The value ranges of value1 and value2 include integers or floating\-point numbers. |Return integers when all parameters are integers, otherwise return a floating\-point number. |
      |Division |```sql```<br>```(/  value1   value2)```<br> |The value ranges of value1 and value2 include integers or floating\-point numbers. |Return integers when all parameters are integers, otherwise return a floating\-point number. |
      |Modulo |```sql```<br>```(mod  value1   value2)```<br> |The value ranges of value1 and value2 include integers or floating\-point numbers. |Return integers when all parameters are integers, otherwise return a floating\-point number. |
      

   * Logical operation

      * Comparison operation

         
         |**Function** |**Syntax** |**Value range** |**Return value** |
         |---|---|---|---|
         |Greater than |```sql```<br>```(> value1  value2)```<br> |The value ranges of value1 and value2 include integers, floating\-point numbers, or strings. |`true` or `false` |
         |Less than |```sql```<br>```(< value1  value2)```<br> |The value ranges of value1 and value2 include integers, floating\-point numbers, or strings. |`true` or `false` |
         |Equal to |```sql```<br>```(= value1  value2)```<br> |The value ranges of value1 and value2 include integers, floating\-point numbers, or strings. |`true` or `false` |
         |Greater than or equal to |```sql```<br>```(>= value1  value2)```<br> |The value ranges of value1 and value2 include integers, floating\-point numbers, or strings. |`true` or `false` |
         |Less than or equal to |```sql```<br>```(<= value1  value2)```<br> |The value ranges of value1 and value2 include integers, floating\-point numbers, or strings. |`true` or `false` |
         |Not equal to |```sql```<br>```(!= value1  value2)```<br> |The value ranges of value1 and value2 include integers, floating\-point numbers, or strings. |`true` or `false` |
         

      * Boolean operation

         
         |**Function** |**Syntax** |**Value range** |**Return value** |
         |---|---|---|---|
         |OR operation |```sql```<br>```(or true false true)```<br> |* true<br><br>* false |`true` or `false`. For example:<br><br>```sql```<br>```(or (> 1 2) (> 3 2))```<br><br><br>Return `true`. |
         |AND operation |```sql```<br>```(and true false true)```<br> |* true<br><br>* false |`true` or `false`. For example:<br><br>```sql```<br>```(and (> 2 1) (> 3 2))```<br><br><br>Return `true`. |
         |NOT operation |```sql```<br>```(not true)```<br> |* true<br><br>* false |`true` or `false`. For example:<br><br><br>* Example 1<br><br>   ```sql```<br>```   (not (= 1 2))```<br>```   ```<br>   <br><br>   Return `true`.<br><br>* Example 2:<br><br>   ```sql```<br>```   (not (= 1 1))```<br>```   ```<br>   <br><br>   Return `false`. |
         

   * String function

      
      |**Function** |**Syntax** |**Return value** |
      |---|---|---|
      |Get the character at a certain index in the string. |```sql```<br>```(sget "字符串" 索引位置)```<br> |Return the character at the index position. For example:<br><br>```sql```<br>```(sget "abcd" 2)```<br><br><br>Return `#c`. |
      |Append characters to the string. |```sql```<br>```(append "字符串" #追加字符)```<br> |Return the added string. For example:<br><br>```sql```<br>```(append "ab" #c)```<br><br><br>Return `abc`. |
      |Return the substring of the string. |```sql```<br>```(slice 字符串 from to)```<br> |Return a substring from from to to (excluding to). For example:<br><br>```sql```<br>```(slice "abcd" 1 3)```<br><br><br>Return `bc`. |
      |Format conversion between strings |* Convert string to int format.<br><br>   ```sql```<br>```   (int "字符串")```<br>```   ```<br>   <br><br>* Convert string to float format.<br><br>   ```sql```<br>```   (float "字符串")```<br>```   ```<br>    |Convert a string to an int or float format. For example:<br><br><br>* Return 123.<br><br>   ```sql```<br>```   (int "123")```<br>```   ```<br>   <br><br>* Return 3.14.<br><br>   ```sql```<br>```   (float "3.14")```<br>```   ```<br>    |
      

* Flow control function

   
   |**Function** |**Syntax** |**Description** |
   |---|---|---|
   |cond statement |```sql```<br>```(cond```<br>```    first-condition first-expression```<br>```    second-condition second-expression```<br>```    ...```<br>```    default-expression)```<br> |`cond` is similar to the Switch statement in general languages, but cond must include a default branch. For example:<br><br>```sql```<br>```(cond (> age 50)  (println "五十而知天命")```<br>```      (> age 40)  (println "四十不惑")```<br>```      (> age 30)  (println "三十而立")```<br>```      (println "年轻人"))```<br><br><br>When `age` is `20`, it returns `young person`. |
   |if or when statement |* if syntax expression:<br><br><br>```sql```<br>```(if condition expression)```<br><br><br><br>* when syntax expression:<br><br><br>```sql```<br>```(when condition expression)```<br> |The syntax expressions of if and when share the same meaning: executing certain operations when a condition is met. For example:<br><br>```sql```<br>```(if (> 2 1) (println "OK"))```<br><br><br>Return `ok`. |
   |unless statement |```sql```<br>```(unless condition expression)```<br> |Opposite to if, the operation executes when the condition is not met. For example:<br><br>```sql```<br>```(unless false (println "OK"))```<br><br><br>Return `ok`. |
   

* Data operation function

   * Array function

      
      |**Function** |**Syntax** |**Return value** |
      |---|---|---|
      |Create an array of specified length, or create an array of specified length and initialize it with a specified value. |* Create syntax expression for arrays of specified length:<br><br>   ```sql```<br>```   (make-array  长度)```<br>```   ```<br>   <br><br>* Create syntax expression for arrays of specified length initialized with a specified value:<br><br>   ```sql```<br>```   (make-array  长度  默认值)```<br>```   ```<br>    |Return an array of the specified length or an array of the specified length initialized with a specified value. For example:<br><br><br>* Example of returning an array with a specified length:<br><br>   ```sql```<br>```   (make-array 3)```<br>```   ```<br>   <br><br>   The returned array is `[() () ()]`.<br><br>* Example of returning an array with a specified length and initializing it with a specified value:<br><br>   ```sql```<br>```   (make-array 3 0)```<br>```   ```<br>   <br><br>   The returned array is `[0 0 0]`. |
      |Access the array by array index |```sql```<br>```(aget  数组  索引)```<br> |Return the array at the index. For example:<br><br>```sql```<br>```(aget [1  2  3]  1)```<br><br><br>Return `2`. |
      |Set the array element value |```sql```<br>```(aset!  数组  索引  值)```<br> |Replace the value at the index. For example:<br><br>```sql```<br>```(aset! [0 1 2] 1 3)```<br><br><br>Return `[0 3 2]`. |
      |Check if an array contains a specific element. |```sql```<br>```(exist?  数组  USD素)```<br> |The return value is true or false. Check if an array contains a specific element. For example:<br><br>```sql```<br>```(exist? ["a" "b"] "a")```<br><br><br>Return `true`. |
      |Get a subarray from the array. |```sql```<br>```(slice  数组  from  to)```<br> |Return a substring array, the return value is [from to). For example:<br><br>```sql```<br>```(slice [1 2 3 4] 1 3)```<br><br><br>Return `[2 3]`. |
      

   * Hash function

      
      |**Function** |**Syntax** |**Return value** |
      |---|---|---|
      |Access hash element |* Syntax 1:<br><br>   ```sql```<br>```   (hget hash key)```<br>```   ```<br>   <br><br>* Syntax 2:<br><br>   ```sql```<br>```   (hget hash key defalut)```<br>```   ```<br>    |Return access to the hash element. For example:<br><br><br>* Example 1<br><br>   ```sql```<br>```   (hget {"a" 2 "b" 3} "a")```<br>```   ```<br>   <br><br>   Return `2`.<br><br>* Example 2:<br><br>   ```sql```<br>```   (hget {"a" 2 "b" 3} "c" 0)```<br>```   ```<br>   <br><br>   Since the accessed element `key` does not exist, it returns the custom default value `0`.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The default value default supports customization.   </div><br>    |
      |Set hash element |```sql```<br>```(def h {"key1" value1})```<br>```(hset! h "key1" 参数1)```<br> |Return the hash element after successful setting. For example:<br><br>```sql```<br>```(def h {"a" 3})```<br>```(hset! h "a" 2)```<br><br><br>Return `{"a" 2}`. |
      |Delete the hash element |```sql```<br>```(def h {"key1" value1 "key2" value2})```<br>```(hdel! h "key")```<br> |Return the hash element after deletion. For example:<br><br>```sql```<br>```(def h {"a" 3 "b" 2})```<br>```(hdel! h "a")```<br><br><br>Return `{"b" 2}`. |
      |Detect whether the hash contains the key. |```sql```<br>```(exist? {"参数1" "参数2"} "参数1")```<br> |The return value is as follows:<br><br><br>* true: exists.<br><br>* false: does not exist.<br><br><br>Examples are as follows:<br><br>```sql```<br>```(exist? {"a" "b"} "a")```<br><br><br>Return `true`. |
      

   * Generic container function

      
      |**Function** |**Syntax** |**Description** |
      |---|---|---|
      |Add elements to the end of a string or array. |* Add elements after the array.<br><br>   ```sql```<br>```   (append [参数1  参数2]  USD素)```<br>```   ```<br>   <br><br>* Add elements after the string.<br><br>   ```sql```<br>```   (append  "字符串"   #USD素)```<br>```   ```<br>    |Return a new array or string. For example:<br><br><br>* Add elements after the array.<br><br>   ```sql```<br>```   (append [1 2] 3)```<br>```   ```<br>   <br><br>   Return a new array `[1 2 3]`.<br><br>* Add elements after the string.<br><br>   ```sql```<br>```   (append "ab" #c)```<br>```   ```<br>   <br><br>   Return a new string `"abc"`. |
      |Concatenate multiple arrays or strings. |* Concatenate multiple arrays<br><br>   ```sql```<br>```   (concat [参数1 参数2] [参数3 参数4])```<br>```   ```<br>   <br><br>* Concatenate multiple strings<br><br>   ```sql```<br>```   (concat "字符串 1" "字符串 2")```<br>```   ```<br>    |Return a new array or string. For example:<br><br><br>* Concatenate multiple arrays.<br><br>   ```sql```<br>```   (concat [1 2] [3 4])```<br>```   ```<br>   <br><br>   Return a new array `[1 2 3 4]`.<br><br>* Concatenate multiple strings.<br><br>   ```sql```<br>```   (concat "ab" "cd")```<br>```   ```<br>   <br><br>   Return a new string `"abcd"`. |
      

   * Byte stream function

      
      |**Function** |**Syntax** |**Return value** |
      |---|---|---|
      |Convert byte stream to string |```sql```<br>```(string 字节流)```<br> |Return a string. For example:<br><br>```sql```<br>```(string 0B68656c6c6f)```<br><br><br>Return `hello`. |
      |Convert string to byte stream. |```sql```<br>```(bytes "字符串")```<br> |Return a byte stream. For example:<br><br>```sql```<br>```(bytes "abc")```<br><br><br>Return `0B616263`. |
      

   * Higher\-order function

      
      |**Function** |**Syntax** |**Return value** |
      |---|---|---|
      |Apply the function to each element in the list or array. |```sql```<br>```(map 函数 数组)```<br> |Return an array or list where the specified function is applied to each element in the array. For example:<br><br><br>* Apply the function to each element in the list.<br><br>   ```sql```<br>```   (map add3 [1 2 3])```<br>```   ```<br>   <br><br><br>Return a new array `[4 5 6]`.<br><br><br>* Apply the function to each element in the array.<br><br>   ```sql```<br>```   (map int ["1" "2" "3"]```<br>```   ```<br>   <br><br><br>Return a new array `[1 2 3]`. |
      |Filter array using specified function. |```sql```<br>```(filter 函数 数组)```<br> |Keep the element when the filter function returns `true`, otherwise discard it. For example:<br><br>```sql```<br>```(defn even? [a] (= 0 (mod a 2)))```<br>```(filter even? [1 2 3 4])```<br><br><br>The return result is `[2 4]`. |
      |Perform aggregation on an array or list. |```sql```<br>```(foldl 函数 初始值 数组)```<br> |Return the aggregate result of the array or list. For example:<br><br><br>* Aggregate the array.<br><br>   ```sql```<br>```   (foldl + 0 [1 2 3 4])```<br>```   ```<br>   <br><br>   The return result is `10`.<br><br>* Aggregate the list.<br><br>   ```sql```<br>```   (foldl * 1 [1 2 3 4])```<br>```   ```<br>   <br><br><br>The return result is `24`. |
      

   * Type introspection

      
      |**Function** |**Syntax** |**Return value** |
      |---|---|---|
      |Zero check |zero? |When the target parameter is `0` or `0.0`, return `true`, otherwise return `false`. |
      |Null check |null? |When the target parameter is `()`, return `true`, otherwise return `false`. |
      |Empty check |empty? |When the target parameter is `()`, `[]`, `""` or`{}`, return `true`, otherwise return `false`. |
      |Is it List? |list? |If the target parameter is a list, return `true`; otherwise, return `false`. |
      |Is it an array? |array? |When the target parameter’s data type is array, return` true`; otherwise, return `false`. |
      |Is it a number? |number? |If the target parameter's data type is int, char, or float, then return `true`; otherwise, return `false`. |
      |Is it an integer? |int? |If the target parameter's data type is integer, return `true`; otherwise, return `false`. |
      |Is it a floating point number? |float? |When the target parameter’s data type is float, return` true`; otherwise, return `false`. |
      |Is it a character? |char? |When the target parameter’s data type is char, return `true`; otherwise, return `false`. |
      |Is it a string? |string? |If the target parameter's data type is string, return `true`; otherwise, return `false`. |
      |Is it a symbol? |symbol? |When the target parameter's data type is symbol, return `true`; otherwise, return `false`. |
      |Is it a hash value? |hash? |When the target parameter’s data type is hash, return `true`; otherwise, return `false`. |
      |Is it a byte stream? |bytes? |When the target parameter’s data type is bytes, return `true`; otherwise, return `false`. |
      |Whether to return the specified data type? |type |When the returned target parameter's data type is symbol, string, array, bool, char, float, function, hash, int, list, or bytes, it returns `true`. Otherwise, it returns `false`. |
      


<span id=".5omp5bGV5Ye95pWw"></span>
### Extension function


* Expression extension function

   * Operation extension function

      
      |**Function** |**Syntax** |**Return value** |
      |---|---|---|
      |Algebraic left shift |```sql```<br>```(sla  操作的数据  移动位数)```<br> |Return the result of an arithmetic left shift. For example:<br><br>```sql```<br>```(sla 1 3)```<br><br><br>Return `8`. |
      |Arithmetic right shift |```sql```<br>```(sra  操作的数据  移动位数)```<br> |Return the result after algebraic right shift. For example:<br><br>```sql```<br>```(sra 1 1)```<br><br><br>Return `0`. |
      |8bit logical left shift |```sql```<br>```(sll8  操作的数据  移动位数)```<br> |Return the result of 8bit logical left shift. For example:<br><br><br>* Example 1<br><br>   ```sql```<br>```   (sll8 1 1)```<br>```   ```<br>   <br><br><br>Return `2`.<br><br><br>* Example 2<br><br>   ```sql```<br>```   (sll8 -1 1)```<br>```   ```<br>   <br><br><br>Return `254`. |
      |16bit logical left shift |```sql```<br>```(sll16  操作的数据  移动位数)```<br> |Return the result of 16bit logical left shift. For example:<br><br><br>* Example 1:<br><br>   ```sql```<br>```   (sll16 1 1)```<br>```   ```<br>   <br><br><br>Return `2`.<br><br><br>* Example 2:<br><br>   ```sql```<br>```   (sll16 -1 1)```<br>```   ```<br>   <br><br><br>Return `65534`. |
      |32bit logical left shift |```sql```<br>```(sll32  操作的数据  移动位数)```<br> |Return the result of 32bit logical left shift. For example:<br><br><br>* Example 1<br><br>   ```sql```<br>```   (sll32 1 1)```<br>```   ```<br>   <br><br>   Return `2`.<br><br>* Example 2:<br><br>   ```sql```<br>```   (sll32 -1 1)```<br>```   ```<br>   <br><br>   Return `4294967294`. |
      |64bit logical left shift |```sql```<br>```(sll64  操作的数据  移动位数)```<br> |Return the result of 64bit logical left shift. For example:<br><br><br>* Example 1<br><br>   ```sql```<br>```   (sll64 1 1)```<br>```   ```<br>   <br><br><br>Return `2`.<br><br><br>* Example 2:<br><br>   ```sql```<br>```   (sll64 -1 1)```<br>```   ```<br>   <br><br><br>Return `18446744073709551614`. |
      |8bit logical right shift |```sql```<br>```(srl8 操作的数据 移动位数)```<br> |Return the result of 8bit logical right shift. For example:<br><br><br>* Example 1<br><br>   ```sql```<br>```   (srl8 2 1)```<br>```   ```<br>   <br><br>   Return `1`.<br><br>* Example 2:<br><br>   ```sql```<br>```   (srl8 -2 1)```<br>```   ```<br>   <br><br>   Return `127`. |
      |16bit logical right shift |```sql```<br>```(srl16  操作的数据  移动位数)```<br> |Return the result of 16bit logical right shift.<br><br><br>* Example 1<br><br>   ```sql```<br>```   (srl16 2 1)```<br>```   ```<br>   <br><br>   Return `1`.<br><br>* Example 2:<br><br>   ```sql```<br>```   (srl16 -2 1)```<br>```   ```<br>   <br><br>   Return `32767`. |
      |32bit logical right shift |```sql```<br>```(srl32  操作的数据  移动位数)```<br> |Return the result of 32bit logical right shift. For example:<br><br><br>* Example 1:<br><br>   ```sql```<br>```   (srl32 2 1)```<br>```   ```<br>   <br><br>   Return `1`.<br><br>* Example 2:<br><br>   ```sql```<br>```   (srl32 -2 1)```<br>```   ```<br>   <br><br>   Return `2147483647`. |
      |64bit logical right shift |```sql```<br>```(srl64  操作的数据  移动位数)```<br> |Return the result of 64bit logical right shift. For example:<br><br><br>* Example 1<br><br>   ```sql```<br>```   (srl64 2 1)```<br>```   ```<br>   <br><br>   Return `1`.<br><br>* Example 2:<br><br>   ```sql```<br>```   (srl64 -2 1)```<br>```   ```<br>   <br><br>   Return `9223372036854775807`. |
      |bit and |```sql```<br>```(bit-and  操作的数据  移动位数)```<br> |Return the result of bit and. For example:<br><br>```sql```<br>```(bit-and 3 2)```<br><br><br>Return `2`. |
      |bit or |```sql```<br>```(bit-or  操作的数据  移动位数)```<br> |Return the result of bit\-or. For example:<br><br>```sql```<br>```(bit-or 3 1)```<br><br><br>Return `3`. |
      |bit XOR |```sql```<br>```(bit-xor  操作的数据  移动位数)```<br> |Return the result of bitwise XOR. For example:<br><br>```sql```<br>```(bit-xor 3 1)```<br><br><br>Return `2`. |
      |bitwise not |```sql```<br>```(bit-not  操作的数据  移动位数)```<br> |Return the bitwise NOT result. For example:<br><br>```sql```<br>```(bit-not 2)```<br><br><br>Return `-3`. |
      

   * Time extension function

      
      |**Function** |**Syntax** |**Return value** |
      |---|---|---|
      |Return the current time |```sql```<br>```(time/now)```<br> |Return the current time. For example:<br><br>```sql```<br>```(time/now)```<br><br><br>Return the current time point. |
      |Format time |```sql```<br>```(time/format  时间  转换目标)```<br> |Support converting time to a unix timestamp in seconds or milliseconds, and also support converting time to a string in a specified format. For example:<br><br><br>* Convert time to a unix timestamp in seconds.<br><br>   ```sql```<br>```   (time/format (time/now) 'timestamp)```<br>```   ```<br>   <br><br>* Convert time to a unix timestamp in milliseconds.<br><br>   ```sql```<br>```   (time/format (time/now) 'timestamp-ms)```<br>```   ```<br>   <br><br>* Convert time to a string in a specified format.<br><br>   ```sql```<br>```   (time/format (time/now) "2006-01-02 15:04:05")```<br>```   ```<br>    |
      |time parsing |```sql```<br>```(time/parse 解析目标)```<br> |Return time parsing result. For example:<br><br><br>* Parse time from unix timestamp.<br><br>   ```sql```<br>```   (time/parse 1656988237)```<br>```   ```<br>   <br><br>* Parse time from string using the default layout (2006\-01\-02 15:04:05).<br><br>   ```sql```<br>```   (time/parse "2015-02-23 23:54:55")```<br>```   ```<br>   <br><br>* Parse time from string by specifying the layout and time string.<br><br>   ```sql```<br>```   (time/parse "2014-Feb-04" "2006-Jan-02")```<br>```   ```<br>   <br><br>* Parse time from string by specifying the layout, time string, and time zone.<br><br>   ```sql```<br>```   (time/parse "2014-Feb-04" "2006-Jan-02" "Asia/Shanghai")```<br>```   ```<br>    |
      |Beijing time parsing |```sql```<br>```time/parse-beijing```<br> |```sql```<br>```(time/parse-beijing "2015-02-23 23:54:55")```<br> |
      |Time calculation |```sql```<br>```(time/add-date 时间  n年 n月 n日)```<br> |Return the calculated time. For example:<br><br>```sql```<br>```(time/add-date (time/now) 1 2 3)```<br><br><br>Return the current time plus 1 year, 2 months, and 3 days. |
      ||```sql```<br>```(time/add 时间  n 年或 n 月或 n 日或 n 小时或 n 分钟或 n 秒)```<br> |Return the calculated time. For example:<br><br><br>* Add 1 year to the current time.<br><br>   ```sql```<br>```   (time/add (time/now) 1 'year)```<br>```   ```<br>   <br><br>* Add 1 month to the current time.<br><br>   ```sql```<br>```   (time/add (time/now) 1 'month)```<br>```   ```<br>   <br><br>* Add 1 day to the current time.<br><br>   ```sql```<br>```   (time/add (time/now) 1 'day)```<br>```   ```<br>   <br><br>* Add 1 hour to the current time.<br><br>   ```sql```<br>```   (time/add (time/now) 1 'hour)```<br>```   ```<br>   <br><br>* Add 1 minute to the current time.<br><br>   ```sql```<br>```   (time/add (time/now) 1 'minute)```<br>```   ```<br>   <br><br>* Add 1 second to the current time.<br><br>   ```sql```<br>```   (time/add (time/now) 1 'second)```<br>```   ```<br>    |
      ||```sql```<br>```(time/sub  time1   time2)```<br> |Return the time difference between time1 and time2, in seconds. |
      |Return the year |```sql```<br>```(time/year   时间)```<br> |Return the year. For example:<br><br>```sql```<br>```(time/year (time/now))```<br><br><br>Return the current year. |
      |Return the month |```sql```<br>```(time/month  时间)```<br> |Return the month. For example:<br><br>```sql```<br>```(time/month  (time/now))```<br><br><br>Return the current month. |
      |Return the day |```sql```<br>```(time/day  时间)```<br> |Return the day. For example:<br><br>```sql```<br>```(time/day (time/now))```<br><br><br>Return the current day. |
      |Return the hour |```sql```<br>```(time/hour  时间)```<br> |Return the hour. For example:<br><br>```sql```<br>```(time/hour (time/now))```<br><br><br>Return the current hour. |
      |Return the minute |```sql```<br>```(time/minute  时间)```<br> |Return the minute. For example:<br><br>```sql```<br>```(time/minute (time/now))```<br><br><br>Return the current minutes. |
      |Return the seconds |```sql```<br>```(time/second  时间)```<br> |Return the seconds. For example:<br><br>```sql```<br>```(time/second (time/now))```<br><br><br>Return the current seconds. |
      |Return the weekday number |```sql```<br>```(time/weekday  时间)```<br> |Return the weekday number. For example:<br><br>```sql```<br>```(time/weekday (time/now))```<br><br><br>Return the current weekday number. |
      

   * String extension function

      
      |**Function** |**Syntax** |**Return value** |
      |---|---|---|
      |Verify if it contains the string. |```sql```<br>```(str/contains? "字符串" "字符")```<br> |The return value is as follows:<br><br><br>* `true`: Indicates that the character exists in the string.<br><br>* `false`: Indicates that the character does not exist in the string.<br><br><br>For example:<br><br>```sql```<br>```(str/contains? "abc" "b")```<br><br><br>Return `true`. |
      |Query the number of substrings |```sql```<br>```(str/count "字符串" "子字符串")```<br> |Return the count of substrings contained in a string. For example:<br><br>```sql```<br>```(str/count "abcc" "c")```<br><br><br>Return `2`. |
      |Validate whether a string starts with a given substring. |```sql```<br>```(str/start-with? "字符串" "字符")```<br> |The return value is as follows:<br><br><br>* `true`: Indicates using this character as a prefix.<br><br>* `false`: Indicates not using this character as a prefix.<br><br><br>For example:<br><br>```sql```<br>```(str/start-with? "abc" "a")```<br><br><br>Return `true`. |
      |Verify if a string ends with a specific substring. |```sql```<br>```(str/end-with?  "字符串"  "字符")```<br> |The return value is as follows:<br><br><br>* `true`: Indicates using this character as a suffix.<br><br>* `false`: indicates not using this character as a suffix.<br><br><br>For example:<br><br>```sql```<br>```(str/end-with? "abc" "c")```<br><br><br>Return `true`. |
      |Return the index of the first occurrence of a target character in the string. |```sql```<br>```(str/index  "字符串"  "目标字符")```<br> |Return the index of the character in the string. For example:<br><br>```sql```<br>```(str/index "abc" "b")```<br><br><br>Return `1`. |
      |Verify whether the string contains only letters. |```sql```<br>```(str/alpha?  "字符串")```<br> |The return value is as follows:<br><br><br>* `true`: Indicates all letters in the string.<br><br>* `false`: Indicates not all letters in the string.<br><br><br>For example:<br><br>```sql```<br>```(str/alpha? "ab1")```<br><br><br>Return `false`. |
      |Validate whether the string consists of all numbers. |```sql```<br>```(str/digit? "字符串")```<br> |The return value is as follows:<br><br><br>* `true`: Indicates all characters in the string are numbers.<br><br>* `false`: Indicates not all characters in the string are numbers.<br><br><br>For example:<br><br>```sql```<br>```(str/digit? "ab1")```<br><br><br>Return `false`. |
      |Concatenate string |```sql```<br>```(str/join ["字符串1" "字符串2"] "拼接符")```<br> |Return the concatenated string result, supporting string concatenation with any separator. For example:<br><br>```sql```<br>```(str/join ["a" "b"] "_")```<br><br><br>Return `"a_b"`. |
      |Convert uppercase letters in the string to lowercase |```sql```<br>```(str/lower "字符串")```<br> |Return the string converted to lowercase. For example:<br><br>```sql```<br>```(str/lower "ABC")```<br><br><br>Return `"abc"`. |
      |Convert lowercase letters in the string to uppercase letters. |```sql```<br>```(str/upper "字符串")```<br> |Return the string converted to uppercase. For example:<br><br>```sql```<br>```(str/upper "abc")```<br><br><br>Return `"ABC"`. |
      |Replace a substring within a string. |```sql```<br>```(str/replace "字符串" "字符串的子串" "目标子串")```<br> |Return the replaced string. For example:<br><br>```sql```<br>```(str/replace "abc" "b" "B")```<br><br><br>Return `"aBc"`. |
      |Split string |```sql```<br>```(str/split "字符串1 拼接符 字符串2" "拼接符")```<br> |Return the split array. Specify the delimiter used to split the string, supporting any delimiter for concatenation. For example:<br><br>```sql```<br>```(str/split "a_b" "_")```<br><br><br>Return `["a" "b"]`. |
      |Convert the first letter of the string to uppercase. |```sql```<br>```(str/title "字符串")```<br> |Return the converted string. For example:<br><br>```sql```<br>```(str/title "abc")```<br><br><br>Return `"Abc"`. |
      |Verify if the first letter of a string is uppercase. |```sql```<br>```(str/title?  "字符串")```<br> |The return value is as follows:<br><br><br>* `true`: Indicates the first letter of the string is uppercase.<br><br>* `false`: Indicates the first letter of the string is not uppercase.<br><br><br>For example:<br><br>```sql```<br>```(str/title? "abc")```<br><br><br>Return `null`. |
      |Delete string prefix |```sql```<br>```(str/trim-prefix "字符串" "前缀")```<br> |Return the string after deleting the prefix. For example:<br><br>```sql```<br>```(str/trim-prefix "_abc" "_")```<br><br><br>Return `"abc"`. |
      |Delete string suffix |```sql```<br>```(str/trim-suffix "字符串" "后缀")```<br> |Return the string after the suffix is deleted. For example:<br><br>```sql```<br>```(str/trim-suffix "abc_" "_")```<br><br><br>Return `"abc"`. |
      |Delete leading and trailing spaces from a string. |```sql```<br>```(str/trim-space " 字符串 ")```<br> |Return the string after deleting leading and trailing spaces. For example:<br><br>```sql```<br>```(str/trim-space " abc ")```<br><br><br>Return `"abc"`. |
      |Calculate the MD5 value of a string. |```sql```<br>```(str/md5 "字符串")```<br> |Return the MD5 value of the string. For example:<br><br>```sql```<br>```(str/md5 "abc")```<br><br><br>Return `"900150983cd24fb0d6963f7d28e17f72"`. |
      |Sensitive information of the desensitized string |```sql```<br>```(str/mask  "字符串"  开始索引  结束索引  "*")```<br> |Return a masked string, supporting masking of any characters. For example:<br><br><br>* Example 1<br><br>   ```sql```<br>```   (str/mask "hello" 1 2 "*")```<br>```   ```<br>   <br><br>   Return `"h**lo"`.<br><br>* Example 2<br><br>   ```sql```<br>```   (str/mask "hello" 1 -1 "*")```<br>```   ```<br>   <br><br>   `1 -1` means covering from the start index to the end index. This sample returns `"h****"`. |
      

* Data operation extension function

   * Core extension function

      
      |**Function** |**Syntax** |**Return value** |
      |---|---|---|
      |Set function alias |```sql```<br>```(alias 别名 原名)```<br> |Set alias for the original function. For example:<br><br>This example sets an alias `plus` for the addition operation.<br><br>```sql```<br>```(alias plus +)```<br><br><br>When using addition, you can perform addition through the following syntax:<br><br>```sql```<br>```(plus 1  2)```<br><br><br>Return `3`. |
      |Print function |* Syntax 1:<br><br>   ```sql```<br>```   (println  参数)```<br>```   ```<br>   <br><br>* Syntax 2:<br><br>   ```sql```<br>```   (printf  "格式化串" 参数1 参数2...)```<br>```   ```<br>   <br><br>* Syntax 3:<br><br>   ```sql```<br>```   (print  参数)```<br>```   ```<br>    |Output function. For example:<br><br><br>* Example for syntax 1:<br><br>   ```sql```<br>```   (println "hello world")```<br>```   ```<br>   <br><br>   Output `"hello world"`.<br><br>* Example for syntax 2:<br><br>   ```sql```<br>```   (printf "Hi, %v" "Jack")```<br>```   ```<br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Use %v as the default placeholder.   </div><br>   <br><br>   Output `"Hi, Jack"`. |
      

   * JSON extension function

      
      |**Function** |**Syntax** |**Return value** |
      |---|---|---|
      |Convert JSON object to a string. |```sql```<br>```(json/stringify  {"key1"  value1  "key2" value2  "key3"  value3})```<br> |Return the string after successful conversion. For example:<br><br>```sql```<br>```(json/stringify {"a" 1 "b" '() "c" true})```<br><br><br>Return`{"a":1,"b":null,"c":true}`. |
      |Convert string to JSON object. |```sql```<br>```(json/parse   "{"key1" : value1,  "key2" : value2,  "key3" : value3}")```<br> |Return the successfully converted JSON object. For example:<br><br>```sql```<br>```(json/parse "{"a":1,"b":null,"c":true}")```<br><br><br>Return `{"a" 1 "b" () "c" true}`. |
      

      DTS ETL and JSON mapping rules are listed in the following table:

      
      |**DTS ETL syntax construct** |**JSON** |
      |---|---|
      |integer |integer |
      |float |float |
      |string |string |
      |symbol |string |
      |() |null |
      |array |array |
      |bytes |base64 encoded string |
      |list |array |
      |hash |object |
      |bool |bool |
      |char |Integer value of char |
      

   * Base64 extension

      
      |**Function** |**Syntax** |**Return value** |
      |---|---|---|
      |Convert Base64 encoded string to byte stream. |```sql```<br>```(base64/decode "Base64")```<br> |Return the successfully converted byte stream. For example:<br><br>```sql```<br>```(base64/decode "aGVsbG8=")```<br><br><br>Return `"0B68656c6c6f"`. |
      |Convert a byte stream to Base64 encoding |```sql```<br>```(base64/encode 字节流)```<br> |Return the successfully converted Base64. For example:<br><br>```sql```<br>```(base64/encode 0B68656c6c6f)```<br><br><br>Return `"aGVsbG8="`. |
      


<span id=".6aKG5Z-f5Ye95pWw"></span>
### Domain function


|**Function** |**Syntax** |**Return value** |
|---|---|---|
|Delete current record |```sql```<br>```(dts/drop)```<br> |Delete the current data row, no return result. |
|Check whether the current record has been discarded. |```sql```<br>```(dts/dropped?)```<br> |Return type is bool. |
|Return the database name of the current record |```sql```<br>```(dts/db)```<br> |Return type is string. |
|Return the table name of the current record. |```sql```<br>```(dts/table)```<br> |Return type is string. |
|Return the event type of the current record. |```sql```<br>```(dts/event)```<br> |Return type is string. Support the following event types:<br><br><br>* BEGIN<br><br>* COMMIT<br><br>* DDL<br><br>* DML |
|Return the DML type of the current record. |```sql```<br>```(dts/dml)```<br> |Return type is string. Support the following DML types:<br><br><br>* `insert`: add.<br><br>* `update`: update.<br><br>* `delete`: delete. |
|Set tag |```sql```<br>```(dts/set-tag)```<br> |No return type. |
|Check if a certain column in the record is null. |```sql```<br>```(dts/column-null? COLUMN)```<br> |Return type is bool. |
|Query if a certain column exists in the record? |```sql```<br>```(dts/column-exist? COLUMN)```<br> |Return type is bool. |
|Validate if the current event is DDL event. |```sql```<br>```(dts/ddl?)```<br> |Return type is bool. |
|Validate if the current event is DML event. |```sql```<br>```(dts/dml?)```<br> |Return type is bool. |
|Validate if the current event is DML UPDATE. |```sql```<br>```(dts/update?)```<br> |Return type is bool. |
|Validate if the current event is DML DELETE. |```sql```<br>```(dts/delete?)```<br> |Return type is bool. |
|Validate if the current event is DML INSERT. |```sql```<br>```(dts/insert?)```<br> |Return type is bool. |
|Return the value of a field in the record. |```sql```<br>```(dts/column COLUMN DEFAULT)```<br> |The returned field type supports string, int, bool, or float.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the column does not exist or is empty, the default value DEFAULT is given.</div><br> |
|Returns all field names of the current record. |```sql```<br>```(dts/columns)```<br> |Return type is a string array. |
|Set field value |```sql```<br>```(dts/set-column COLUMN VALUE)```<br> |No return type. |
|Transform a column value using the specified function. |```sql```<br>```(dts/map-column COLUMN FUNCTION)```<br> |No return type. |
|Rename field |* Rename column `oldCol` to `newCol` without keeping the original field:<br><br>   ```sql```<br>```   (dts/rename-column "oldCol" "newCol")```<br>```   ```<br>   <br><br>* Rename column `oldCol` to `newCol`, keeping the original field:<br><br>   ```sql```<br>```   (dts/rename-column "oldCol" "newCol" true)```<br>```   ```<br>    |No return type. |
|Filter a column |```sql```<br>```(dts/drop-column COLUMN)```<br> |No return type. |
|Set the specified column as the primary key, especially for modifying primary key column in heterogeneous table synchronization scenarios. |```sql```<br>```(dts/use-index "column1" "column2")```<br> |No return type. |
|(syntactic sugar) Execute certain actions on a table. |```sql```<br>```(dts/match-table TABLE EXPRESSIONS)```<br> |No return type. |
|(syntactic sugar) Execute certain actions if it is an INSERT action on a table. |```sql```<br>```(dts/match-insert-on-table TABLE EXPRESSIONS)```<br> |No return type. |
|(syntactic sugar) Execute certain actions if it is an UPDATE action on a table. |```sql```<br>```(dts/match-update-on-table TABLE EXPRESSIONS)```<br> |No return type. |
|(syntactic sugar) Execute certain actions if it is a DELETE action on a table. |```sql```<br>```(dts/match-delete-on-table TABLE EXPRESSIONS)```<br> |No return type. |
|(syntactic sugar) Execute certain actions if it is a DML event. |```sql```<br>```(dts/match-dml-on-table TABLE EXPRESSIONS)```<br> |No return type. |
|(syntactic sugar) Regex matches a certain table (without database name matching) and performs some actions. |```sql```<br>```(dts/match-table-regexp TABLE EXPRESSIONS)```<br> |No return type. |
|(syntactic sugar) Regex matches a certain table (with database name matching) and performs some actions. |```sql```<br>```(dts/match-db-table-regexp DBTABLE EXPRESIONS)```<br> |No return type. |


<span id=".bXlzcWwt5a2X5q6157G75Z6L"></span>
## MySQL field type

The field types in MySQL correspond to the following types in DSL syntax.


|**MySQL field type** |**Example** |**DSL field type** |**Example** |
|---|---|---|---|
|bit |```sql```<br>```b'111'```<br> |bytes |```lisp```<br>```0B07```<br> |
|tinyint |```sql```<br>```3```<br> |int |```lisp```<br>```3```<br> |
|bool |```sql```<br>```true```<br> |bool |```lisp```<br>```true```<br> |
|smallint |```sql```<br>```3```<br> |int |```lisp```<br>```3```<br> |
|mediumint |```sql```<br>```3```<br> |int |```lisp```<br>```3```<br> |
|int |```sql```<br>```3```<br> |int |```lisp```<br>```3```<br> |
|integer |```sql```<br>```3```<br> |int |```lisp```<br>```3```<br> |
|bigint |```sql```<br>```3```<br> |int |```lisp```<br>```3```<br> |
|bigint unsigned |```sql```<br>```18446744073709551615```<br> |int |```lisp```<br>```18446744073709551615```<br> |
|decimal |```sql```<br>```333.333```<br> |float |```lisp```<br>```333.333```<br> |
|dec |```sql```<br>```333.333```<br> |float |```lisp```<br>```333.333```<br> |
|float |```sql```<br>```1.1```<br> |float |```lisp```<br>```1.1```<br> |
|double |```sql```<br>```1.1```<br> |float |```lisp```<br>```1.1```<br> |
|date |```sql```<br>```'2001-01-01'```<br> |string |```lisp```<br>```"2001-01-01"```<br> |
|datetime |```sql```<br>```'2001-01-01 01:01:01'```<br> |string |```lisp```<br>```"2001-01-01 01:01:01"```<br> |
|timestamp |```sql```<br>```'2001-01-01 01:01:01'```<br> |time |```lisp```<br>```(time/parse "2001-01-01 01:01:01")```<br> |
|time |```sql```<br>```'01:01:01'```<br> |string |```lisp```<br>```"01:01:01"```<br> |
|year |```sql```<br>```2001```<br> |int |```lisp```<br>```2001```<br> |
|char |```sql```<br>```'abc'```<br> |string |```lisp```<br>```"abc"```<br> |
|varchar |```sql```<br>```'abc'```<br> |string |```lisp```<br>```"abc"```<br> |
|binary |```sql```<br>```'abc'```<br> |bytes |```lisp```<br>```0B616263```<br> |
|varbinary |```sql```<br>```'abc'```<br> |bytes |```lisp```<br>```0B616263```<br> |
|tinyblob |```sql```<br>```'abc'```<br> |bytes |```lisp```<br>```0B616263```<br> |
|tinytext |```sql```<br>```'abc'```<br> |string |```lisp```<br>```"abc"```<br> |
|blob |```sql```<br>```'abc'```<br> |bytes |```lisp```<br>```0B616263```<br> |
|text |```sql```<br>```'abc'```<br> |string |```lisp```<br>```"abc"```<br> |
|mediumblob |```sql```<br>```'abc'```<br> |bytes |```lisp```<br>```0B616263```<br> |
|mediumtext |```sql```<br>```'abc'```<br> |string |```lisp```<br>```"abc"```<br> |
|longblob |```sql```<br>```'abc'```<br> |bytes |```lisp```<br>```0B616263```<br> |
|longtext |```sql```<br>```'abc'```<br> |string |```lisp```<br>```"abc"```<br> |
|enum |```sql```<br>```'a'```<br> |int |```lisp```<br>```1```<br> |
|set |```sql```<br>```'a,b'```<br> |int |```lisp```<br>```3```<br> |
|geometry |```sql```<br>```GeomFromText('POINT(1 1)')```<br> |bytes |```lisp```<br>```0B000000000101000000000000000000f03f000000000000f03f```<br> |
|point |```sql```<br>```GeomFromText('POINT(1 1)')```<br> |bytes |```lisp```<br>```0B000000000101000000000000000000f03f000000000000f03f```<br> |
|linestring |```sql```<br>```GeomFromText('LINESTRING(0 0,1 1,2 2)')```<br> |bytes |```lisp```<br>```0B000000000101000000000000000000f03f000000000000f03f```<br> |
|polygon |```sql```<br>```GeomFromText('POLYGON((0 0,10 0,10 10,0 10,0 0),(5 5,7 5,7 7,5 7, 5 5))')```<br> |bytes |```lisp```<br>```0B000000000101000000000000000000f03f000000000000f03f```<br> |
|multipoint |```sql```<br>```GeomFromText('MULTIPOINT(1 1,2 2)')```<br> |bytes |```lisp```<br>```0B000000000101000000000000000000f03f000000000000f03f```<br> |
|multilinestring |```sql```<br>```GeomFromText('MULTILINESTRING((0 0,1 1,2 2),(0 0,2 2,4 4))')```<br> |bytes |```lisp```<br>```0B000000000101000000000000000000f03f000000000000f03f```<br> |
|multipolygon |```sql```<br>```GeomFromText(‘MULTIPOLYGON(((0 0,10 0,10 10,0 10,0 0)),((5 5,7 5,7 7,5 7, 5 5)))’)```<br> |bytes |```lisp```<br>```0B000000000101000000000000000000f03f000000000000f03f```<br> |
|geometrycollection |```sql```<br>```GeomFromText('GEOMETRYCOLLECTION(POINT(2 1),LINESTRING(0 0,1 1,2 2,3 3,4 5))')```<br> |bytes |```lisp```<br>```0B000000000101000000000000000000f03f000000000000f03f```<br> |
|json |```sql```<br>```'{"key":"value"}'```<br> |string |```lisp```<br>```"{\"key\": \"value\"}"```<br> |


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [Creating and starting a data synchronization task](https://docs.byteplus.com/en/docs/DTS/creating_and_initiating_a_synchronization_task)

* [How to configure ETL in a DTS synchronization task](https://docs.byteplus.com/en/docs/DTS/configuring_etl_in_dts_synchronization_task)
