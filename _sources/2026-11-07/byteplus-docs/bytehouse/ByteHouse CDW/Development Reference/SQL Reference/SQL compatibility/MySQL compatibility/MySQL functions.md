---
title: "MySQL functions"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-mysql-functions"
---

<span id="e635de86"></span>
### Set the dialect type to MySQL

By setting `dialect_type='MYSQL'`, you can execute the functions listed below using the MySQL method.

```SQL
ENABLE OPTIMIZER=1
SET dialect_type='MYSQL';
or
[query] + SETTINGS dialect_type='MYSQL';
DESC TABLE t1 SETTINGS dialect_type='MYSQL';
or
CLICKHOUSE_CLIENT --dialect_type=MYSQL
```



* format()

* locate()

* adddate()

* date_sub()

* datediff()

* dayofweek(): In MySQL, the default first day is Sunday. In ByteHouse, the default first day is Monday.

* concat_ws()


<span id="297fb5f1"></span>
### Control Flow Functions

<span id="d3832010"></span>
#### CASE


* **Syntax**:

   * Usage 1: `CASE value WHEN comparison_value THEN result [ELSE result] END`

   * Usage 2: `CASE WHEN condition THEN result [ELSE result] END`

* **Description:**  Returns a value when a condition is met. If the condition is not met, it returns the ELSE result; if ELSE is not provided, it returns NULL.


<span id="5694b6ea"></span>
#### IF Function


* **Syntax**: `IF(expr1, expr2, expr3)`

* **Description:**  If expr1 is TRUE, then return expr2; otherwise, return expr3. Requires three parameters, use NULL as an optional third parameter in two\-parameter scenarios.


<span id="0921d45e"></span>
#### IFNULL function


* **Syntax**: `IFNULL(expr1, expr2)`

* **Description:**  If not NULL, return expr1; otherwise, return expr2.


<span id="45812c1f"></span>
#### NULLIF function


* **Syntax**: `NULLIF(expr1, expr2)`

* **Description:**  If expr1 equals expr2, return NULL; otherwise, return expr1.


<span id="f6536ad1"></span>
### Numeric functions

<span id="b7ef7b25"></span>
#### Basic arithmetic operators


* Addition (+): Calculates the sum of two numbers.

* Subtraction (\-): Calculates the difference between two numbers.

* Multiplication (\*): Multiplies two numbers.

* Division (/): Divides one number by another.

* Integer Division (div): Divides one number by another and returns the integer part of the quotient.

* Modulo (`%` or `mod`): Returns the remainder of a division operation.


<span id="cfd415c9"></span>
#### Math Functions


* Absolute (abs): Returns the absolute value of a number.

* Arc Cosine (acos): Calculates the arccosine of a number.

* Arc Sine (asin): Calculates the arcsine of a number.

* Arc Tangent (atan): Calculates the arctangent of a number.

* Arc Tangent of Two Numbers (atan2): Returns the arctangent of the quotient of its arguments.

* Ceiling (ceiling or ceil): Rounds a number up to the nearest integer.

* Cosine (cos): Calculates the cosine of a number.

* Cotangent (cot): Calculates the cotangent of a number.

* CRC32 (crc32): Calculates the cyclic redundancy check value of a string.

* Degrees (degrees): Converts radians to degrees.

* Exponential (exp): Calculates the exponent of a number.

* Floor (floor): Rounds a number down to the nearest integer.

* Natural Logarithm (ln): Calculates the natural logarithm of a number.

* Logarithm (log): Calculates the logarithm of a number. Use log_with_base to denote logarithms with a base.

* Base\-2 Logarithm (log2): Calculates the logarithm of a number with base 2.

* Base\-10 Logarithm (log10): Calculates the logarithm of a number with base 10.

* Pi (pi): Returns the value of π.

* Power (power or pow): Raises one number to the power of another.

* Radians (radians): Converts angles into radians.

* Random Number (rand): Generates a random number. Use randCanonical for numbers between 0 and 1.

* Round (round): Rounds a number to a specified number of decimal places.

* Sign (sign): Determine the sign of a number, returning \-1, 0, or 1.

* Sine (sin): Calculate the sine of a number.

* Square Root (sqrt): Calculate the square root of a number.

* Tangent (tan): Calculate the tangent of a number.


<span id="368d7699"></span>
### Date and Time Functions

<span id="7931be36"></span>
#### Date and Time Function Operations


* ADDDATE(): Add a specific time interval to a date.

* SUBDATE(): Subtract a specific time interval from a date.

* ADDTIME(): Add a specific time interval to a time or datetime value.

* SUBTIME(): Subtract a specific time interval from a time or datetime value.

* DATE_SUB(): Subtract a time interval from a date.

* DATE_ADD(): Add a time interval to a date.


<span id="9f68ef71"></span>
#### Date and Time Extraction


* CURDATE(): Returns the current date.

* CURTIME(): Returns the current time.

* NOW(): Returns the current date and time.

* SYSDATE(): Returns the system's current date and time.

* EXTRACT(): Extracts a specified part of the date as designated by the user.

* YEAR(), MONTH(), DAY(), HOUR(), MINUTE(), SECOND(): Extract specific components from a date/time value.


<span id="79b03c2d"></span>
#### Format Functions


* DATE_FORMAT(): Set the date according to the specified format.

* TIME_FORMAT(): Set the time according to the specified format.


<span id="21c197a3"></span>
#### Conversion Functions


* STR_TO_DATE(): Convert a string to a date according to the specified format.

* UNIX_TIMESTAMP(): Convert a date to a UNIX timestamp.

* FROM_UNIXTIME(): Convert a UNIX timestamp to a date.


<span id="725559dd"></span>
#### Time Zone Functions


* CONVERT_TZ(): Convert the date and time from one time zone to another.


<span id="3c1713d4"></span>
#### Other Functions


* DATEDIFF(): Returns the number of days between two dates.

* TIMEDIFF(): Returns the difference between two times/datetime expressions.

* DATE(), TIME(): Extracts the date or time part from a datetime expression.

* DAYNAME(), MONTHNAME(): Returns the day of the week or month name from a date.

* WEEK(), YEARWEEK(): Returns the week number of a date.


<span id="7cd52f40"></span>
### String Functions

<span id="908f2c1d"></span>
#### Operations and Analysis


* ASCII(): Returns the ASCII value of the first character in a string.

* BIN(): Converts a number to a binary string.

* BIT_LENGTH(): Returns the bit length of a string.

* CHAR(): Constructs a string from a series of ASCII values.

* CHAR_LENGTH(): Returns the number of characters in a string.

* CONCAT(): Concatenates two or more strings into one string.

* CONCAT_WS(): Connects strings using a specified delimiter.

* ELT(): Returns the Nth element from a list of strings.

* EXPORT_SET(): Returns a string representing the bits set in a value.

* FIELD(): Returns the index of a value in a list of values.

* FIND_IN_SET(): Finds the position of a string in a comma\-separated list of strings.

* FORMAT(): Formats a number to a specified number of decimal places.

* FROM_BASE64(): Decodes a Base64 encoded string.

* HEX(): Converts a string or number to hexadecimal.

* INSTR(): Returns the position where the substring first appears in the string.

* LCASE() or LOWER(): Converts a string to lowercase.

* LEFT(): Returns the leftmost part of the string of a specified length.

* LENGTH(): Returns the byte length of a string.

* LIKE: Performs pattern matching using SQL simple regular expression comparison.

* LOCATE(): Returns the position where the substring first appears in the string.

* LPAD(): Pads a string on the left with another string until a certain length is reached.

* LTRIM(): Removes leading spaces from the string.

* MAKE_SET(): Constructs a set of comma\-separated strings that correspond to the bits set in the given values.

* MID(), SUBSTR(), SUBSTRING(): Returns a substring from a string.

* OCT(): Converts a number into an octal string.

* ORD(): Returns the code of the leftmost character in a string.

* POSITION(): Synonym for LOCATE().

* QUOTE(): Escapes special characters in strings for use in SQL statements.

* REPEAT(): Repeats a string a specified number of times.

* REPLACE(): Replaces occurrences of a specified substring with another substring.

* REVERSE(): Reverses a string.

* RIGHT(): Returns the rightmost part of a string of specified length.

* RPAD(): Right\-pads a string with another string to a certain length.

* RTRIM(): Removes trailing spaces from a string.

* SOUNDEX(): Returns a soundex string from a string.

* SPACE(): Returns a string of spaces of the specified quantity.

* STRCMP(): Compares two strings.

* SUBSTRING_INDEX(): Returns the substring before the number of occurrences of a specified delimiter in a string.

* TO_BASE64(): Encodes a string using base64.

* TRIM(): Removes leading and trailing spaces from a string.

* UCASE() or UPPER(): Converts a string to uppercase.

* UNHEX(): Converts a hexadecimal string to a regular string.


<span id="88c12279"></span>
### Aggregate functions

<span id="43ff3359"></span>
#### Average value


* Calculate the average value of numerical values in the column.

* ByteHouse returns `nan` for empty tables, which differs from MySQL and ADB, both of which return NULL.


<span id="2d8f4352"></span>
#### BIT_AND, BIT_OR, BIT_XOR represent bit and, bit or, bit xor respectively.


* Perform bitwise operations on the values in the column.

* BIT_AND returns the bitwise and of all values.

* BIT_OR returns the bitwise or of all values.

* BIT_XOR returns the bitwise xor of all values.


<span id="8db5df2f"></span>
#### COUNT counts


* Calculate the number of rows that meet specified conditions.

* COUNT(DISTINCT xx) counts unique values.

* COUNT(ALL xx) counts all values, including duplicates.


<span id="37ab9861"></span>
#### MAX and MIN are the maximum and minimum values.


* Returns the maximum and minimum values in the column respectively.

* Applicable to various data types, including dates and strings.

* For numeric types where NULL values are inserted, behavior may vary by system.


<span id="f83adc7c"></span>
#### STD, STDDEV_POP, and VAR, VAR_POP, VAR_SAMP


* Calculate standard deviation and variance.

* STD and STDDEV_POP return the overall standard deviation.

* VAR_POP returns the overall variance.

* VAR_SAMP returns the sample variance.

* The accuracy and processing of an empty set may vary; ByteHouse returns `nan` for empty sets.


<span id="2166efef"></span>
#### SUM calculation


* Calculate the total of a numeric column.


<span id="704146f9"></span>
### Special Considerations


* Conversion and default values: The results of aggregate functions on data types with implicit conversions or default values can differ significantly across SQL systems. For instance, ByteHouse's handling of default values for numbers may differ from MySQL and ADB, affecting functions like Min and Max.

* Handling of NULL: The treatment of NULL values by aggregate functions can impact results. In ByteHouse, certain functions such as Min and Max might return 0 or the actual value, while MySQL or ADB would return NULL.

* Precision issues: Precision problems may occur when calculating standard deviation or variance due to the internal representation of floating\-point numbers.


<span id="2e531f58"></span>
### **Not supported yet**

Not supported yet: MySQL functions below:


* `convert_tz()`: Currently does not support timezone parameters like GMT/MET


<span id="55daaba8"></span>
#### Inconsistent with MySQL


| |Function differences |
|---|---|
|repeat(),<br><br>rpad(), sapce() |Passing negative numbers as parameters will result in an error, whereas in MySQL it returns empty or NULL |
|exp() |Precision difference |
|ln() |Precision difference |
|bin() |ByteHouse returns results with additional '0000' prefix compared to MySQL |
|from_base64() |Passing an incorrect base64 value will result in an error, while MySQL returns NULL |
|cast() |There are differences from ADB, some usages are not supported by MySQL either; conversion to boolean type results are true/false, not 1/0 |
|avg() |When avg() is applied to an empty table, ByteHouse returns 'nan', while MySQL returns NULL. |
|min(),<br><br>max() |The default values in ByteHouse and MySQL are inconsistent. Numeric types have a default value of 0 in ByteHouse, while MySQL defaults to NULL, which may affect the results when calculating min() and max(). You can avoid this issue by adding Nullable() when creating a table. |
|localtime() |The result lacks year, month, and day compared to MySQL. |
|str_to_date() |If the formatting parameters and the input time are not aligned, the return values differ.<br><br>For str_to_date('2022\-01\-06 10:20:30','%Y\-%m\-%d'), ByteHouse returns NULL, while MySQL returns 2022\-01\-06. |


<span id="a0f5aeb7"></span>
#### Usage differs from MySQL

The usage of the following functions differs from MySQL, please use with caution:


|Function name |Difference |Solution |
|---|---|---|
|if |Only supports 3 parameters, 2 parameters need to be rewritten | |
|log() |Parameter log(Oct,100) is not supported |Add log_with_base() to support usage with two parameters |
|rand() |In MySQL, it returns a random number within the range [0,1), but in ByteHouse, it returns a random number within the entire UInt32 range |To generate a random number in the range [0,1) in ByteHouse, use randCanonical |
|encrypt() |In MySQL, two parameters are sufficient, but in ByteHouse, three parameters are required. The first parameter specifies the encryption algorithm. |encrypt('aes\-128\-ecb','abdABC123','1234567890123456'); |
|data_format() |In ByteHouse, existing customers require the use of `data_format` to mimic the Hive format. |In ByteHouse, replace `data_format_mysql` with `data_format`. |
