---
title: "Data conversion function library"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/data_conversion_function_library"
---

This article will list some functions supported by the data transformation mode of the solution.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The default time zone for string and timestamp input and output is currently UTC+8. You can use the CONVERT_TZ function to convert to another desired time zone.</div>


<div data-tips="true" data-tips-type="warning">Unless otherwise specified, when the parameter is null, the return value will be null.</div>


<span id="0e100e3e"></span>
## Comparison functions


|**Function name** |**Description** |
|---|---|
|value1 = value2 |If value1 equals value2, return true. If either value1 or value2 is null, return null. |
|value1 <\> value2 |Return true if value1 is not equal to value2; return null if either value1 or value2 is null. |
|value1 \> value2 |If value1 is greater than value2, return true; if either value1 or value2 is null, return null. |
|value1 \>= value2 |If value1 is greater than or equal to value2, return true. If either value1 or value2 is null, return null. |
|value1 < value2 |If value1 is less than value2, return true; if either value1 or value2 is null, return null. |
|value1 <= value2 |Returns true if value1 is less than or equal to value2; returns null if either value1 or value2 is null. |
|value IS NULL |Returns true if value is null. |
|value IS NOT NULL |Return true if value is not null. |
|value1 BETWEEN value2 AND value3 |If value1 is greater than or equal to value2 and less than or equal to value3, return true.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The SYMMETRIC keyword is not supported in the current version at this time.</div><br><br><br>For example:<br><br><br>* 12 BETWEEN 15 AND 12 returns false<br><br>* 12 BETWEEN 10 AND NULL returns null<br><br>* 12 BETWEEN NULL AND 10 returns false |
|value1 NOT BETWEEN value2 AND value3 |If value1 is less than value2 or greater than value3, return true.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The current version does not yet support the SYMMETRIC keyword.</div><br> |
|string1 LIKE string2 |If string1 matches the pattern string2, return true. If either string1 or string2 is null, return null.<br><br>The '%' symbol can match multiple characters, while the '_' symbol can match only a single character.<br><br>For example, "HELLO" LIKE "_EL%" returns true. |
|string1 NOT LIKE string2 |Returns true if string1 does not match the pattern string2; returns null if either string1 or string2 is null.<br><br>The '%' symbol can match multiple characters, while the '_' symbol can match only a single character.<br><br>For example, 'HELLO' NOT LIKE '_EL%' returns false. |
|value1 IN (value2 [, value3]\* ) |If value1 is present in the given list (value2, value3, and so on), return true<br><br>If value1 is null, null is always returned. |
|value1 NOT IN (value2 [, value3]\* ) |If value1 is not in the given list (value2, value3, ...), return true<br><br>If value1 is null, always return null. |


<span id="0001c790"></span>
## Logic functions


|**Function name** |**Description** |
|---|---|
|boolean1 OR boolean2 |If boolean1 is true or boolean2 is true, return true.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Parameters containing null are not supported for now.</div><br> |
|boolean1 AND boolean2 |If boolean1 is true and boolean2 is true, return true.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Parameters with null values are not currently supported.</div><br> |
|NOT boolean |If the boolean is false, return true; if the boolean is true, return false.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Parameters containing null are not currently supported.</div><br> |
|boolean IS FALSE |If the boolean is false, return true; if the boolean is true, return false.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Parameters containing null are not currently supported.</div><br> |
|boolean IS NOT FALSE |If the boolean is true, return true; if the boolean is false, return false.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Parameters containing null are not currently supported.</div><br> |
|boolean IS TRUE |If the boolean is true, return true; if the boolean is false, return false.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Parameters containing null values are not currently supported.</div><br> |
|boolean IS NOT TRUE |If the boolean is false, return true; if the boolean is true, return false.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Parameters with null values are not currently supported.</div><br> |


<span id="5f806eac"></span>
## Arithmetic functions


|**Function name** |**Description** |
|---|---|
|numeric1 + numeric2 |Return the value of numeric1 + numeric2.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Parameters containing null are not currently supported.</div><br> |
|numeric1 \- numeric2 |Return the value of numeric1 minus numeric2<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Parameters containing null are not currently supported</div><br> |
|numeric1 \* numeric2 |Return the product of numeric1 and numeric2.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Parameters containing null are not currently supported.</div><br> |
|numeric1 / numeric2 |Return the quotient of numeric1 divided by numeric2<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Parameters containing null are not currently supported</div><br> |
|numeric1 % numeric2 |Returns the remainder of numeric1 divided by numeric2 (modulo operation)<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Parameters containing null are not supported at this time.</div><br> |
|ABS(numeric) |Returns the absolute value of numeric.<br><br>If numeric is null, return null. |
|CEIL(numeric) |Round the value up and return the smallest integer that is greater than or equal to the value.<br><br>If numeric is null, return null. |
|FLOOR(numeric) |Round the value down and return the smallest integer greater than or equal to the value.<br><br>If numeric is null, return null. |
|* ROUND(numeric)<br><br>* ROUND(numeric, int) |Round the number to the nearest integer.<br><br><br>* If the second parameter is not provided, the function returns the smallest integer greater than or equal to the given value.<br><br>* If a second parameter int is provided, the value is rounded to int decimal places.<br><br>* If numeric is null, return null. |
|UUID() |Return a randomly generated UUID string |
|* LOG(numeric2)<br><br>* LOG(numeric1, numeric2) |* If only one argument is passed, the natural logarithm of numeric2 is returned.<br><br>* If two arguments are provided, the function returns the logarithm of numeric2 with base numeric1.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Currently, numeric2 must be greater than 0, and numeric1 must be greater than 1.</div><br> |
|EXP(numeric) |Returns e raised to the numeric power. |
|POWER(numeric1, numeric2) |Returns numeric1 raised to the power of numeric2. |
|SQRT(numeric) |Return the square root of numeric. |
|* RAND()<br><br>* RAND(seed)<br><br>* RAND(from, to) |* No parameters: Returns a pseudo\-random double\-precision value between 0.0 (inclusive) and 1.0 (exclusive).<br><br>* One parameter: returns a pseudo\-random double\-precision value between 0.0 (inclusive) and 1.0 (exclusive), using an initial seed integer. If two RAND functions have the same initial seed, they will return the same sequence of numbers.<br><br>* Two parameters: returns a pseudorandom integer value between 0 (inclusive) and the specified integer (exclusive).<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The seed parameter does not accept null values. If either the from or to parameter is null, the result is null.</div><br> |
|* RAND_INTEGER(to)<br><br>* RAND_INTEGER(seed, to) |* One parameter: returns a pseudorandom integer between 0 (inclusive) and the specified integer (exclusive).<br><br>* Two parameters: Returns a pseudorandom integer value between 0 (inclusive) and the specified value (exclusive), using an initial seed. If two RAND_INTEGER functions have the same initial seed and boundaries, they will return the same sequence of numbers.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The seed and to parameters do not accept null values.</div><br> |
|TRUNCATE(numeric1, integer2) |Return a value truncated to integer2 decimal places.<br><br>If numeric1 or integer2 is null, return null.<br><br>If integer2 is 0, the result will not have a decimal point or decimal part.<br><br>integer2 can be negative, causing the specified number of digits to the left of the decimal point to become zero.<br><br>This function can also be called with only the numeric1 parameter, without setting integer2. If integer2 is not set, the function will truncate as if integer2 were 0.<br><br>For example: truncate(42.345, 2) returns 42.34, and truncate(42.345) returns 42.0. |


<span id="bab5421e"></span>
## String functions


|**Function name** |**Description** |
|---|---|
|string1 |<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If any parameter is null, the entire result is null.</div><br> |
|CHAR_LENGTH(string) |Return the number of characters in the string. If the string is null, null is returned. |
|UPPER(string) |Returns the uppercase form of the string. If the string is null, return null. |
|LOWER(string) |Returns the lowercase form of the string. If the string is null, return null. |
|TRIM(string1)、BTRIM(string1) |Remove whitespace from both ends of string1.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Currently, the "LEADING", "TRAILING", and "FROM" keywords are not supported.</div><br> |
|LTRIM(string1) |Remove spaces or whitespace characters from the left side of string1. |
|RTRIM(string1) |Remove spaces or whitespace characters from the right side of the string string1. |
|REGEXP_REPLACE(string1, string2, string3) |Returns a string in which all substrings in string1 that match the regular expression string2 are replaced with STRING3. If any parameter is null, the result is null.<br><br>For example, REGEXP_REPLACE('foobar', 'oo |
|SUBSTRING(string FROM integer1 [ FOR integer2 ]) |Returns the substring of STRING starting from position integer1 (note that the starting position is 1), with a length of integer2. If the FOR keyword is not specified, the substring extends to the end of the string by default.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The integer1 and integer2 parameters do not accept null values.</div><br> |
|SUBSTR(string, integer1[, integer2]) |Returns the substring of STRING starting from position integer1 (note that the starting position is 1), with a length of integer2. If the length is not specified, the substring extends to the end of the string by default.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The integer1 and integer2 parameters do not accept null values.</div><br> |
|CONCAT(string1, string2,…) |Returns the result of concatenating string1 and string2, which is equivalent to using<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If any parameter is null, the entire result is null.</div><br> |
|OVERLAY(str1 PLACING str2 FROM int1 [ FOR int2 ]) |Returns a string where, starting from position integer1 in string1, integer2 characters are replaced by string2. If integer2 is not specified, it defaults to the length of string2. If any parameter is null, the result is null.<br><br>For example, OVERLAY('This is an old string' PLACING ' new' FROM 10 FOR 5) returns "This is a new string". |
|PRINTF(format[, obj]\*) |Return a formatted string using the semantics of the Java printf function. If the string is null, the result is null.<br><br>For example, PRINTF('User: %s, Count: %d', 'Kyle', 10) returns the string 'User: Kyle, Count: 10'. |
|STARTSWITH(expr, startExpr) |Determine whether expr starts with startExpr. If startExpr is empty, the result is true.<br><br>If any parameter is null, return null. |
|ENDSWITH(expr, endExpr) |Determine whether expr ends with startExpr. If startExpr is empty, the result is true.<br><br>If any parameter is null, return null. |
|REGEXP(string1, string2) |Return true if any (possibly empty) substring of string1 matches the Java regular expression string2; otherwise, return false.<br><br>If any parameter is null, return null. |
|REGEXP_EXTRACT(string1, string2[, integer]) |Returns a string extracted from string1 using the specified regular expression string2 and match group index integer.<br><br>Note: In regular expression matching, group indices start from 1, while 0 refers to the entire regular expression match.<br><br>In addition, the group index in a regular expression match must not exceed the number of defined groups.<br><br>For example, REGEXP_EXTRACT('foothebar', 'foo(.\*?)(bar)', 2) returns "bar". |
|SIMILAR TO |string1 SIMILAR TO string2: Determines whether any (including empty) substring of string1 matches the specified Java regular expression string2. Returns true if a match is found; otherwise, returns false.<br><br>string1 NOT SIMILAR TO string2: Determines whether none of the substrings (including empty substrings) of string1 match the specified Java regular expression string2. Returns true if there is no match; otherwise, returns false. |
|LPAD(string1, integer, string2) |Returns a new string that is created by left\-padding string1 with string2 until it reaches the specified integer length.<br><br>If the length of string1 is shorter than the integer, string1 will be truncated to the integer length.<br><br>For example, LPAD('hi', 4, '??') returns "??hi", and LPAD('hi', 1, '??') returns "h". |
|RPAD(string1, integer, string2) |Returns a new string by right\-padding string1 with string2 until the specified integer length is reached.<br><br>If the length of string1 is less than the integer, string1 will be shortened to the integer length.<br><br>For example, RPAD('hi', 4, '??') returns "hi??"; RPAD('hi', 1, '??') returns "h". |
|LOCATE(string1, string2[, integer]) |Returns the position of the first occurrence of string1 in string2, starting the search from position integer. If not found, return 0.<br><br>If any parameter is null, return null. |
|STR_TO_MAP(string1[, string2, string3]) |Returns a mapping of <String, String\> key\-value pairs by splitting string1 using a delimiter. "string2" is the delimiter, which defaults to the comma (,) symbol.<br><br>string3 is the key\-value separator, and its default is the = symbol.<br><br>If you want to create key\-value pairs of a type other than String, use the CREATE_MAP method. |
|REVERSE(string) |Returns the reversed form of the string. If string is null, return null. |
|SPLIT(string, delimiter) |Splits the input string `string` using the specified delimiter `delimiter` and returns an array of strings. The specific rules are as follows:<br><br><br>* If the string does not contain a delimiter, a **single\-element array** containing the original string is returned.<br><br>* If the delimiter is an empty string, it returns **the result of splitting each character into a separate element.** <br><br>* If the string or delimiter is null, return null.<br><br>* Special boundary handling:<br><br>   * If the delimiter appears at the beginning or end of the string, an empty string is generated at the corresponding position.<br><br>   * If there are consecutive delimiters, an empty string will be generated between each pair of delimiters. |
|SPLIT_INDEX(string1, string2, integer1) |Split string1 using the delimiter string2, and return the string at index integer (starting from 0) from the resulting array. If the integer is negative, return null. If any parameter is null, return null. |


<span id="11a3bdf9"></span>
### JSON functions


|**Function name** |**Description** |
|---|---|
|GET_JSON_OBJECT(jsonStr, pathStr[, defaultVal]) |Returns the value of the element at the position specified by pathStr in jsonStr (a JSON string). The value can be of various types.<br><br>You can specify the default value to use when an element cannot be retrieved by using the third parameter, defaultVal.<br><br>For example, if jsonStr is '{"name":"John","age":30,"address":{"city":"New York","zip":"10001"}}' and pathStr is '.name', the return value is 'John'. |
|GET_JSON_STRING(jsonStr, pathStr[, defaultVal]) |Returns the value at the position specified by pathStr in jsonStr (a JSON string) as a String.<br><br>For example, if jsonStr is '{"name":"John","age":30,"address":{"city":"New York","zip":"10001"}}' and pathStr is '.name', the return value is 'John'. |
|TO_JSON(value[, defaultVal])<br><br>JSON_STRING(value) |Convert the value object (which can be of various types) to a JSON string.<br><br>The TO_JSON function supports an optional second parameter, defaultVal. When value is null, you can return defaultVal as a string. |
|JSON_EXISTS(jsonValue, path) |Determine whether the jsonValue string meets the given path search criteria. If the condition for finding the path is met, return true.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">ON ERROR and similar keywords are not currently supported. If any parameter is null, return false.</div><br> |


<span id="3e57bed9"></span>
### Encryption and decryption, encoding, and hash functions


|**Function name** |**Description** |
|---|---|
|AES_ENCRYPT(plaintext, base64Key, [algorithm]) |Encrypt the plaintext string using the specified encryption algorithm (default is 'aes\-256\-cbc') and the provided base64Key (the original key must be 16, 24, or 32 bytes in length), and output the result as a Base64\-encoded string.<br><br>If the parameter is null, output null.<br><br>The algorithms currently supported are:<br><br>'aes\-256\-cbc', 'aes\-128\-cbc', 'aes\-192\-cbc', 'aes\-256\-ecb', 'aes\-128\-ecb', 'aes\-192\-ecb' |
|AES_DECRYPT(encryptedBase64, base64Key, [algorithm]) |Decrypt the encryptedBase64 string, which is encoded in Base64, using the specified encryption algorithm (default is 'aes\-256\-cbc') and the provided base64Key (the original key must be 16, 24, or 32 bytes in length), and output the result as a string.<br><br>If the parameter is null, null is output.<br><br>Currently supported algorithms:<br><br>'aes\-256\-cbc', 'aes\-128\-cbc', 'aes\-192\-cbc', 'aes\-256\-ecb', 'aes\-128\-ecb', 'aes\-192\-ecb' |
|TO_BASE64(plaintext) |Encode the plaintext string in Base64 format and return it.<br><br>If the parameter is null, output null. |
|FROM_BASE64(encoded) |Decode the Base64\-encoded string and return the original text.<br><br>If the parameter is null, output null. |
|DECODE(str, charset) |Use the provided character set charset (for example, 'US\-ASCII', 'ISO\-8859\-1', 'UTF\-8', 'UTF\-16BE', 'UTF\-16LE', or 'UTF\-16') to decode the string str.<br><br>If any parameter is null, the result is also null. |
|ENCODE(str, charset) |Encode the string str using the provided character set charset (for example, "US\-ASCII", "ISO\-8859\-1", "UTF\-8", "UTF\-16BE", "UTF\-16LE", or "UTF\-16"), and output as a binary byte array.<br><br>You can further encode the output byte array as a string in conjunction with the TO_BASE64 function.<br><br>If any parameter is null, the result is also null. |
|* MD5(str)<br><br>* SHA1(str)<br><br>* SHA224(str)<br><br>* SHA256(str)<br><br>* SHA384(str)<br><br>* SHA512(str) |Apply the hash algorithm specified by the function name (such as MD5) to str.<br><br>If str is null, the result is null. |


<span id="368a0007"></span>
## Time\-related functions


|**Function name** |**Description** |
|---|---|
|LOCALTIME |Returns the current time with millisecond precision. The type is Time, which includes hour, minute, second, and millisecond.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Currently, only the UTC+8 time zone is supported.</div><br> |
|LOCALTIMESTAMP |Returns the current timestamp with millisecond precision. The type is Timestamp, which includes year, month, day, hour, minute, second, and millisecond.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Currently, only the UTC+8 time zone is supported.</div><br> |
|CURRENT_TIME |Returns the current time with millisecond precision. The type is Time, which includes hour, minute, second, and millisecond.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Currently, only the UTC+8 time zone is supported; therefore, this function is equivalent to the LOCALTIME function.</div><br> |
|CURRENT_DATE |Returns the current date as a Date type, which includes the year, month, and day.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Currently, only the UTC+8 time zone is supported.</div><br> |
|INTERVAL string range |You can add or subtract a duration from the return value of a function that returns a value of type Timestamp, which can partially replace the TIMESTAMPADD function.<br><br>Currently, range supports only four types: DAY, HOUR, MINUTE, and SECOND.<br><br>For example, TO_TIMESTAMP('2024\-10\-08 23:59:59', 'yyyy\-MM\-dd HH:mm:ss') \- INTERVAL 2 DAY <= NOW() |
|NOW() |Returns the current timestamp (with millisecond precision), of type Timestamp, which includes year, month, day, hour, minute, second, and millisecond.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Currently, only the UTC+8 time zone is supported, so this function is equivalent to LOCALTIMESTAMP.</div><br> |
|DATE_FORMAT(timestamp, string) |Convert a timestamp to a string in the specified date format. Format strings are compatible with Java's SimpleDateFormat. |
|TIMESTAMPDIFF(timepointunit, timepoint1, timepoint2) |Returns the signed number of time units between timepoint1 and timepoint2.<br><br>The unit of the interval is specified by the first parameter. This parameter must be one of the following values: "SECOND", "MINUTE", "HOUR", "DAY", "MONTH", or "YEAR".<br><br>For example, TIMESTAMPDIFF(HOUR, TIMESTAMPADD(DAY, \-1, NOW()), NOW()) returns 24. |
|CONVERT_TZ(string1, string2, string3) |Convert the date and time string string1 (with the default ISO timestamp format 'yyyy\-MM\-dd HH:mm:ss') from time zone string2 to time zone string3. The format for time zones can be an abbreviation, for example 'PST' (which may be ambiguous). It is recommended to use the full name of the time zone (for example, "Asia/Shanghai") or a custom ID (for example, "UTC+8:00").<br><br>For example, CONVERT_TZ('2024\-11\-08 18:35:33', 'Asia/Shanghai', 'Asia/Tokyo') returns "2024\-11\-08 19:35:33." |
|TIMESTAMPADD(timeintervalunit, interval, timepoint) |Returns a new time value, which is obtained by adding a signed integer interval to timepoint. The unit of the interval is specified by the unit parameter. This parameter must be one of the following values: SECOND, MINUTE, HOUR, DAY, MONTH, or YEAR. Currently, WEEK, QUARTER, and other values are not supported.<br><br>For example, TIMESTAMPADD(DAY, \-1, NOW()) returns the timestamp for one day ago. |
|FROM_UNIXTIME(numeric[, string]) |Output the value of the numeric parameter `numberic` using the format string (default: 'yyyy\-MM\-dd HH:mm:ss'). The numeric value represents the number of seconds since '1970\-01\-01 00:00:00' and can be generated by the UNIX_TIMESTAMP() function.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Currently, only the UTC+8 time zone is supported.</div><br> |
|* UNIX_TIMESTAMP()<br><br>* UNIX_TIMESTAMP(timestampStr[, format]) |Returns the current Unix timestamp in seconds.<br><br>If the timestampStr string parameter is provided, the string will be converted to a Unix timestamp using the 'yyyy\-MM\-dd HH:mm:ss' format by default.<br><br>If an additional format parameter is provided, you can customize the format of the timestampStr string using the Java SimpleDateFormat pattern. |
|UNIX_TIMESTAMP_MILLIS() |Returns the current Unix timestamp in milliseconds. |
|TO_DATE(string1[, string2]) |Convert the date string string1, which is in the format specified by string2 (default: 'yyyy\-MM\-dd'), to a Date type. |
|TO_TIMESTAMP(string1[, string2]) |Convert the date\-time string string1 in the format specified by string2 (default format: 'yyyy\-MM\-dd HH:mm:ss') to a timestamp. |


<span id="80adf396"></span>
## Condition functions


|**Function name** |**Description** |
|---|---|
|CASE value WHEN value1_1 [, value1_2]\* THEN RESULT1 (WHEN value2_1 [, value2_2 ]\* THEN result_2)\* (ELSE result_z) END |When the value first matches one of the values (valueX_1, valueX_2, ...), return the corresponding result resultX.<br><br>If no match is found, result_z is returned if it is provided; otherwise, null is returned. |
|CASE WHEN condition1 THEN result1 (WHEN condition2 THEN result2)\* (ELSE result_z) END |When the first condition conditionX is met, return resultX.<br><br>If no conditions are met, return result_z if it is provided; otherwise, return null. |
|COALESCE(value1 [, value2]\*) |Return the first non\-null parameter. If all parameters are null, null is also returned. |
|IF(condition, true_value, false_value) |If the condition "condition" is met, return true_value; otherwise, return false_value.<br><br>For example, IF(5 \> 3, 5, 3) returns 5. |
|NULLIF(value1, value2) |If value1 equals value2, return null; otherwise, return value1.<br><br>For example, NULLIF(5, 5) returns null; NULLIF(5, 0) returns 5. |
|IS_NUMBER(str)<br><br>IS_DECIMAL(str) |Determine whether the given string str is a valid number; if so, return true. If the string is null, return null.<br><br>For example, "123", "1.23", "\-123.45", and "1e10" are all valid numbers.<br><br>IS_NUMBER is determined according to the acceptance criteria of the Java Double type; IS_DECIMAL is determined according to the acceptance criteria of the Java BigDecimal type and is suitable for very large numbers. |
|IS_SPACES(str) |Determine whether the given string str consists only of whitespace characters (spaces and tabs); if so, return true. If the string is null, null is returned.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Neither null nor the empty string contains any symbols, so the result is false.</div><br> |
|IS_ALPHA(str) |The IS_ALPHA(str) function is used to check whether the given string str consists only of letters. If all characters in str are letters, return TRUE; otherwise, return FALSE.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Neither null nor an empty string contains any characters; therefore, the function returns false.</div><br> |
|IS_DIGIT(str) |Determine whether the given string str consists entirely of digits; if so, return true. If the string is null, return null.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Neither null nor the empty string contains any symbols, so the function returns false.</div><br> |


<span id="de97678d"></span>
## Type conversion functions


|**Function name** |**Description** |
|---|---|
|CAST(value AS type) |Convert value to the specified type. For example, CAST(value AS VARCHAR) converts value to a string type. |
|TYPEOF(input) |Returns the actual Java object type of the input field in uppercase, for example, STRING, INTEGER, ARRAY, MAP, and so on.<br><br>For null values, return the 'NULL' string. |


<span id="e81f1823"></span>
## Aggregate functions


|**Function name** |**Description** |
|---|---|
|CARDINALITY(array) |Return the number of elements in the array. If the array is null, return 0. |
|CARDINALITY(map) |Returns the number of elements in the Map. If the parameter is null, return 0. |
|CREATE_MAP(k1, v1, k2, v2 ...) |Create a Map key\-value pair where k and v can be of any type |
|CREATE_LIST(...) |Create a List array with elements of any type |
