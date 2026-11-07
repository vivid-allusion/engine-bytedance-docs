---
title: "Functions overview"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Overview-of-functions-2"
---

This topic lists all SQL functions supported by Torch Log Service (TLS).

<span id="948a9098"></span>
## Aggregate functions


|Function |Function Syntax |Description |
|---|---|---|
|ARBITRARY |ARBITRARY(KEY) |This function returns an arbitrary non\-empty value in a group of values. |
|AVG |AVG(KEY) |This function returns the average of a group of values. |
|BITWISE_AND_AGG |BITWISE_AND_AGG(KEY) |This function returns the result of the bitwise AND operation on the values. |
|BITWISE_OR_AGG |BITWISE_OR_AGG(KEY) |This function returns the result of the bitwise OR operation on the values. |
|BOOL_AND |BOOL_AND(boolean_expression) |This function checks whether all values meet the specified condition. |
|BOOL_OR |BOOL_OR(boolean_expression) |This function checks whether a value meets the specified condition exists. |
|CHECKSUM |CHECKSUM(KEY) |This function returns the checksum of a group of values. |
|COUNT |COUNT(\*) |This function returns the number of values. |
||COUNT(1) |This function returns the number of values. |
||COUNT(KEY) |This function returns the number of non\-null values. |
|COUNT_IF |COUNT_IF (Boolean Expression) |This function returns the number of values that meet the specified condition. |
|EVERY |EVERY(boolean_expression) |This function determines whether all values satisfy the specified Boolean expression. |
|GEOMETRIC_MEAN |GEOMETRIC_MEAN(KEY) |This function calculates the geometric mean of the values. |
|KURTOSIS |KURTOSIS(KEY) |This function calculates the kurtosis of the values. |
|MAP_UNION |MAP_UNION(KEY) |This function merges multiple sets of map data. |
|MAX |MAX(KEY) |This function returns the maximum value in a group of values. |
|MAX_BY |MAX_BY(KEY1, KEY2) |This function queries the KEY1 values associated with the maximum value of KEY2. |
||MAX_BY(KEY1, KEY2, n) |This function queries the KEY1 values associated with the top N values of KEY2, returning the results in array form. |
|MIN |MIN(KEY) |This function returns the minimum value in a group of values. |
|SUM |SUM(KEY) |This function returns the sum of a group of values. |


<span id="Date and time functions"></span>
## Date and time functions


|Function |Syntax |Description |
|---|---|---|
|CURRENT_DATE |CURRENT_DATE |This function returns the current date. |
|CURRENT_TIME |CURRENT_TIME |This function returns the current time and time zone. |
|CURRENT_TIMESTAMP |CURRENT_TIMESTAMP |This function returns the current date, time, and time zone. |
|CURRENT_TIMEZONE |CURRENT_TIMEZONE() |This function returns the current time and time zone. |
|DATE |DATE(KEY) |This function returns the date part of a date and time value. |
|DATE_FORMAT |DATE_FORMAT(KEY, format) |This function converts a date or time of the Timestamp type to a value in a specified format. |
|DATE_PARSE |DATE_PARSE(KEY, format) |This function converts a date and time string to a value in a specified format. |
|FROM_ISO8601_DATE |FROM_ISO8601_DATE(KEY) |This function converts a date in ISO8601 format to that of the Date data type. |
|FROM_ISO8601_TIMESTAMP |FROM_ISO8601_TIMESTAMP(KEY) |This function converts a date and time value in ISO8601 format to a date and time value of the Timestamp data type. |
|FROM_UNIXTIME |FROM_UNIXTIME(KEY) |This function converts a Unix timestamp to a date and time value of the Timestamp data type without a time zone. |
||FROM_UNIXTIME(KEY, time zone) |This function converts a Unix timestamp to a date and time value of the Timestamp data type with a time zone. |
||FROM_UNIXTIME(KEY, hours, minutes) |This function converts a Unix timestamp to a date and time value of the Timestamp data type with a time zone. In this format, you can set the offset of a time zone. |
|LOCALTIME |LOCALTIME |This function returns the local time. |
|LOCALTIMESTAMP |LOCALTIMESTAMP |This function returns the local date and time. |
|NOW |NOW() |This function returns the local date and time. |
|TO_ISO8601 |TO_ISO8601(KEY) |This function converts a date and time value of the Date or Timestamp data type to a date and time value in ISO 8601 format. |
|TO_UNIXTIME |TO_UNIXTIME(KEY) |This function converts a date and time value of the Timestamp data type to a Unix timestamp. |
|DAY |DAY(KEY) |This function returns the day of the month from a date and time value. |
|DAY_OF_MONTH |DAY_OF_MONTH(KEY) |This function returns the day of the month from a date and time value. |
|DAY_OF_WEEK |DAY_OF_WEEK(KEY) |This function returns the day of the week from a date and time value. |
|DAY_OF_YEAR |DAY_OF_YEAR(KEY) |This function returns the day of the year from a date and time value. |
|DOW |DOW(KEY) |This function returns the day of the week from a date and time value. |
|DOY |DOY(KEY) |This function returns the day of the year from a date and time value. |
|EXTRACT |EXTRACT(field from KEY) |This function returns a date or time value from a date and time value based on the specified field. |
|HOUR |HOUR(KEY) |This function returns the hour of the day from a date and time value in 24\-hour format. |
|MINUTE |MINUTE(KEY) |This function returns the minute of the hour from a date and time value. |
|MONTH |MONTH(KEY) |This function returns the month of the year from a date and time value. |
|QUARTER |QUARTER(KEY) |This function returns the quarter of the year from a specified date. |
|SECOND |SECOND(KEY) |This function returns the second of the minute from a date and time value. |
|TIMEZONE_HOUR |TIMEZONE_HOUR(KEY) |This function returns the offset of the time zone in hours. |
|TIMEZONE_MINUTE |TIMEZONE_MINUTE(KEY) |This function returns the offset of a time zone in minutes. |
|WEEK |WEEK(KEY) |This function returns the week of the year from a specified date. |
|WEEK_OF_YEAR |WEEK_OF_YEAR(KEY) |This function returns the week of the year from a specified date. |
|YEAR |YEAR(KEY) |Thisfunction returns the year from a date and time value. |
|YEAR_OF_WEEK |YEAR_OF_WEEK(KEY) |This function returns the year on which a specified date falls in the ISO week date system. |
|YOW |YOW(KEY) |This function returns the year on which a specified date falls in the ISO week date system. |
|DATE_ADD |DATE_ADD(unit, N, KEY) |This function adds or subtracts a specified time period from a date and time value. |
|DATE_DIFF |DATE_DIFF(unit, KEY1, KEY2) |This function returns the difference between the two dates or points in time. |
|DATE_TRUNC |DATE_TRUNC(unit, KEY) |This function truncates a date or time value based on the time unit you specify. |
|DATE_TRUNC_SEC |DATE_TRUNC_SEC(unit, KEY) |This function truncates a date or time value based on the time unit you specify. |
|TIME_SERIES |TIME_SERIES(KEY, window_time, format, padding_data) |This function pads a value if no value exists in a time window. |


<span id="String functions"></span>
## String functions


|Function |Function Syntax |Description |
|---|---|---|
|CHR |CHR(KEY) |This function converts an ASCII code to ASCII characters. |
|CODEPOINT |CODEPOINT (KEY) |This function converts ASCII characters to an ASCII code. |
|CONCAT |CONCAT(KEY1, KEY2...) |This function concatenates multiple strings into one string. |
|FROM_UTF8 |FROM_UTF8(KEY) |This function decodes a binary string into a UTF\-8 encoded string. Invalid UTF\-8 sequences are replaced with the default replacement character U+FFFD. |
||FROM_UTF8(KEY, replace_string) |This function decodes a binary string into a UTF\-8 encoded string. Invalid UTF\-8 sequences are replaced with a custom string. |
|LENGTH |LENGTH(KEY) |This function returns the length of a string. |
|LEVENSHTEIN_DISTANCE |LEVENSHTEIN_DISTANCE(KEY1, KEY2) |This function returns the minimum edit distance between two strings. |
|LOWER |LOWER(KEY) |This function converts the characters in a string to lowercase letters. |
|LPAD |LPAD(KEY, length, lpad_string) |This function pads the beginning of a specified string with characters until it reaches a specified length, and then returns the resulting string. |
|LTRIM |LTRIM(KEY) |This function removes spaces from the beginning of a string. |
|NORMALIZE |NORMALIZE(KEY) |This function transforms a string using normalization form C (NFC). |
|POSITION |POSITION(sub_string in KEY) |This function returns the position of a specified substring in a string. |
|REPLACE |REPLACE(KEY, sub_string ) |This function removes a specified substring. |
||REPLACE (KEY, sub_string, replace_string) |This function replaces a specified substring with another string. |
|REVERSE |REVERSE(KEY) |This function returns a string in reverse order. |
|RTRIM |RTRIM(KEY) |This function removes spaces from the end of a string. |
|SPLIT |SPLIT(KEY, delimeter) |This function splits a string using a specified delimiter and returns a set of substrings. |
||SPLIT(KEY, delimeter, limit) |This function splits a string using a specified delimiter and returns a set of substrings. The number of substrings that can be generated is specified by limit. |
|SPLIT_PART |SPLIT_PART(KEY,delimeter,index) |This function splits a string using a specified delimiter and returns the substring at the position specified by index. |
|SPLIT_TO_MAP |SPLIT_TO_MAP(KEY, delimiter01, delimiter02) |This function splits a string using a specified first delimiter and then splits the resulting substrings using a specified second delimiter to key\-value pairs. |
|STRPOS |STRPOS(KEY, sub_string) |This function is used to find the position of the first occurrence of a substring within a specified string. The position count starts at 1. If the substring is not found in the specified string, the function returns 0. |
|SUBSTR |SUBSTR(KEY, start) |This function returns the substring at a specified position in a string. |
||SUBSTR(KEY, start, length) |This function returns the substring at a specified position in a string. The length of the substring is specified. |
|TO_UTF8 |TO_UTF8(KEY) |This function converts a string to a UTF\-8 representation. |
|TRIM |TRIM(KEY) |This function removes spaces from the beginning and end of a string. |
|UPPER |UPPER(KEY) |This function converts the characters in a string to uppercase letters. |


<span id="Regular expression functions"></span>
## Regular expression functions


|Function |Syntax |Description |
|---|---|---|
|REGEXP_EXTRACT_ALL |REGEXP_EXTRACT_ALL(KEY, regular_expression) |This function extracts the substrings matched by a specified regular expression and returns arrays of all matched substrings. |
||REGEXP_EXTRACT_ALL(KEY, regular_expression, n) |This function extracts the substrings matched by the regular expression in a specified string and returns an array of substrings that match the nth capturing group. |
|REGEXP_EXTRACT |REGEXP_EXTRACT(KEY, regular_expression) |This function extracts the first substring matched by the regular expression in a specified string and returns the substring. |
||REGEXP_EXTRACT(KEY, regular_expression, n) |This function extracts the substrings matched by the regular expression in a specified string and returns the first substring that matches the nth capturing group. |
|REGEXP_LIKE |REGEXP_LIKE(KEY, regular_expression) |This function verifies whether the value of a field matches a specified regular expression. |
|REGEXP_REPLACE |REGEXP_REPLACE(KEY, regular_expression) |This function removes the substrings matched by the regular expression in a specified string and returns the substrings that remain. |
||REGEXP_REPLACE(KEY, regular_expression, replace_string) |This function replaces the substrings matched by the regular expression in a specified string and returns the result string. |
|REGEXP_SPLIT |REGEXP_SPLIT(KEY, regular_expression) |This function splits a string into an array of substrings based on a regular expression pattern. |


<span id="Period-over-period comparison functions"></span>
## Period\-over\-period comparison functions


|Function |Syntax |Description |
|---|---|---|
|COMPARE |COMPARE(KEY, n) |This function compares the calculation result of the current time period with the calculation result of a time period n seconds before. |
||COMPARE(KEY, n1, n2, n3...) |This function compares the calculation result of the current time period with the calculation results of time periods n1, n2, and n3 seconds before. |
|TS_COMPARE |TS_COMPARE(KEY, n) |This function compares the calculation result of the current time period with the calculation result of a time period n seconds before. |
||TS_COMPARE(KEY, n1, n2, n3...) |This function compares the calculation result of the current time period with the calculation results of time periods n1, n2, and n3 seconds before. |


<span id="235cfeb1"></span>
## Mathematical calculation functions


|Function |Function Syntax |Description |
|---|---|---|
|ABS |ABS(KEY) |This function calculates the absolute value of a number. |
|ACOS |ACOS(KEY) |This function calculates the arccosine of a value. |
|ASIN |ASIN(KEY) |This function calculates the arcsine of a value. |
|ATAN |ATAN(KEY) |This function calculates the arctangent of a value. |
|CBRT |CBRT(KEY) |This function calculates the cube root of a value. |
|CEIL |CEIL(KEY) |This function rounds values up to the nearest integer. |
|CEILING |CEILING(KEY) |This function rounds values up to the nearest integer. |
|COS |COS(KEY) |This function calculates the cosine of a value. |
|COSH |COSH(KEY) |This function calculates the hyperbolic cosine of a value. |
|COSINE_SIMILARITY |COSINE_SIMILARITY(KEY1, KEY2) |This function calculates the cosine similarity between two values. |
|DEGREES |DEGREES |This function converts radians to degrees. |
|E |E() |This function calculates the value of the natural base e. |
|EXP |EXP(x) |This function calculates the natural base e to the power of x. |
|FLOOR |FLOOR(KEY) |This function rounds a number down to the nearest integer. |
|FROM_BASE |FROM_BASE(number_str, base) |This function converts a numeric string in a given base to its decimal equivalent. |
|IS_NAN |IS_NAN(KEY) |This function determines whether the value is NaN. If so, return true. |
|LN |LN(KEY) |This function calculates the natural logarithm of a value. |
|LOG |LOG(KEY) |This function calculates the natural logarithm of a number. |
|LOG2 |LOG2(KEY) |This function calculates the logarithm of the target value to the base 2. |
|LOG10 |LOG10(KEY) |This function calculates the base 10 logarithm of a number. |
|MOD |MOD(KEY1, KEY2) |This function calculates the remainder after dividing two values. |
|NAN |NAN() |This function returns a `NaN`value. |
|PI |PI() |This function returns the value of π, accurate to 15 decimal places. |
|POWER |POWER(KEY, y) |This function raises a number to the power of y. |
|RADIANS |RADIANS(KEY) |This function converts degrees to radians. |
|RAND |RAND() |This function returns a random number. |
|RANDOM |RANDOM() |This function returns a random number in the range [0,1). |
||RANDOM(0, KEY) |This function returns a random number in the range [0,KEY). |
|ROUND |ROUND(KEY) |This function rounds a number to the nearest integer. |
||ROUND(KEY,n) |This function rounds a number to the nearest decimal with n decimal places. |
|SIGN |SIGN(KEY) |This function determines the sign of the target value, indicating the positivity or negativity of the value through 1, 0, and \-1. |
|SIN |SIN(KEY) |This function calculates the sine of the target value. |
|SQRT |SQRT(KEY) |This function calculates the square root of a number. |
|TAN |TAN(KEY) |This function calculates the tangent of the target value. |
|TANH |TANH(KEY) |This function calculates the hyperbolic tangent of the target value. |
|TO_BASE |TO_BASE(number, base) |This function converts a decimal to a string of the specified base. |
|WIDTH_BUCKET |WIDTH_BUCKET(KEY, bound1, bound2, numBuckets) |This function divides a range of values into multiple buckets of the same size, and then returns the number of the bucket in which the KEY value resides. |
|WIDTH_BUCKET |WIDTH_BUCKET(KEY, bins) |This function uses an array to specify the range of buckets, and then returns the number of the bucket in which the KEY value resides. |


<span id="Mathematical statistics functions"></span>
## Mathematical statistics functions


|Function |Function Syntax |Description |
|---|---|---|
|BETA_CDF |BETA_CDF(α, β, v) |This function calculates the cumulative probability that the random variable is less than v given the parameters α and β. |
|CORR |CORR(KEY1, KEY2) |This function calculates the correlation between two sets of values. |
|COVAR_POP |COVAR_POP(KEY1, KEY2) |This function calculates the overall covariance of two sets of values. |
|COVAR_SAMP |COVAR_SAMP(KEY1, KEY2) |This function calculates the sample covariance of two sets of values. |
|INVERSE_NORMAL_CDF |INVERSE_NORMAL_CDF(x, y, p) |This function calculates a value in the normal distribution based on a given cumulative probability p. |
|NORMAL_CDF |NORMAL_CDF(x, y, v) |This function calculates the probability that a random variable in a normal distribution is less than or equal to a particular value v. |
|STDDEV |STDDEV(KEY) |This function calculates the sample standard deviation of the values. |
|STDDEV_SAMP |STDDEV_SAMP(KEY) |This function calculates the sample standard deviation of the values. |
|STDDEV_POP |STDDEV_POP(KEY) |This function calculates the population standard deviation of the values. |
|VARIANCE |VARIANCE(KEY) |This function calculates the sample variance of the values. |
|VAR_SAMP |VAR_SAMP(KEY) |This function calculates the sample variance of the values. |
|VAR_POP |VAR_POP(KEY) |This function calculates the population variance of the values. |


<span id="1a085f49"></span>
## Map functions


|Function |Function Syntax |Description |
|---|---|---|
|Subscript operator |[x] |This function returns the x\-th element in an array. |
|CARDINALITY |CARDINALITY(KEY) |This function calculates the number of key\-value pairs in a map. |
|ELEMENT_AT |ELEMENT_AT(map, key) |This function obtains the value of the specified key in the map. |
|HISTOGRAM |HISTOGRAM(KEY) |This function groups the query and analysis results and returns the results in JSON format. |
|MAP |MAP() |This function constructs an empty map. |
||MAP(KEY1, KEY2) |This function maps two arrays to a map. |
|MAP_AGG |MAP_AGG(KEY1, KEY2) |This function aggregates data and maps it to a map. Each key corresponds to a unique value. |
|MAP_FILTER |MAP_FILTER(KEY, lambda_expression) |This function filters elements in a map based on a lambda expression. |
|MAP_KEYS |MAP_KEYS(KEY) |This function extracts all the keys in the map and returns them as an array. |
|MAP_VALUES |MAP_VALUES(KEY) |This function extracts the values of all the keys in the map and returns them as an array. |
|MULTIMAP_AGG |MULTIMAP_AGG(KEY1, KEY2) |This function aggregates data and maps it to a map. Each key can correspond to multiple values. |


<span id="Array functions"></span>
## Array functions


|Function |Function Syntax |Description |
|---|---|---|
|Subscript operator |[x] |This function returns the x\-th element in an array. |
|ARRAY_AGG |ARRAY_AGG(KEY) |This function returns an array aggregated from all values of a field or expression. |
|ARRAY_DISTINCT |ARRAY_DISTINCT(KEY) |This function removes duplicate elements from an array. |
|ARRAY_EXCEPT |ARRAY_EXCEPT(KEY1, KEY2) |This function removes duplicate elements from two arrays and returns the first array. |
|ARRAY_INTERSECT |ARRAY_INTERSECT(KEY1, KEY2) |This function returns the intersection of two arrays. |
|ARRAY_JOIN |ARRAY_JOIN(KEY, delimiter) |This function concatenates the elements of an array into a string using a specified delimiter. If the array contains a null element, the null element is ignored. |
|ARRAY_JOIN(KEY, delimiter, null_replacement) |ARRAY_JOIN(KEY, delimiter, null_replacement) |This function concatenates the elements of an array into a string using a specified delimiter. If the array contains a null element, the null element is replaced with the specified string. |
|ARRAY_MAX |ARRAY_MAX(KEY) |This function returns the maximum value in an array. |
|ARRAY_MIN |ARRAY_MIN(KEY) |This function returns the minimum value in an array. |
|ARRAY_POSITION |ARRAY_POSITION(KEY, element) |This function returns the position of a specified element, with an element index starting at 1. |
|ARRAY_REMOVE |ARRAY_REMOVE(KEY, element) |This function removes a specified element from an array. |
|ARRAY_SORT |ARRAY_SORT(KEY) |This function sorts an array of elements in ascending order. If the array contains a null element, the null element is placed at the end. |
|ARRAY_TRANSPOSE |ARRAY_TRANSPOSE(KEY) |This function transposes the array, extracting the same index elements in the two\-dimensional array to form a new two\-dimensional array. |
|ARRAY_UNION |ARRAY_UNION(KEY1, KEY2) |This function returns the union of two arrays. |
|CARDINALITY |CARDINALITY(KEY) |This function returns the number of elements in an array. |
|CONCAT |CONCAT(KEY1, KEY2…) |This function concatenates multiple arrays into one array. |
|CONTAINS |CONTAINS(KEY, element) |This function verifies whether an array contains a specified element. |
|ELEMENT_AT |ELEMENT_AT(KEY, index) |This function gets the element at the specified position in the array. |
|FLATTEN |FLATTEN(KEY) |This function converts a two\-dimensional array to a one\-dimensional array. |
|FILTER |FILTER(KEY, lambda_expression) |This function filters elements in an array based on a lambda expression. |
|REDUCE |REDUCE(KEY, lambda_expression) |This function accumulates the individual elements of the array as defined in the lambda expression, and then returns the result of the evaluation. |
|REVERSE |REVERSE(KEY) |This function sorts an array of elements in reverse order. |
|SEQUENCE |SEQUENCE(x, y) |This function generates an array within the specified range, consisting of a continuous and increasing set of values within the range of starting and ending values. Where the increment interval is the default value of 1. |
||SEQUENCE(x, y, step) |This function generates an array within the specified range, consisting of a continuous and increasing set of values within the range of starting and ending values. Where the increment interval is a custom value. |
|SHUFFLE |SHUFFLE(KEY) |This function randomly rearranges the array elements. |
|SLICE |SLICE(KEY, start, length) |This function gets a subset of the array. |
|TRANSFORM |TRANSFORM(KEY, lambda_expression) |This function applies a lambda expression to each element of the array. |
|ZIP |ZIP(KEY1, KEY2...) |This function combines multiple arrays into a two\-dimensional array according to the corresponding positions, and the elements in each array with the same subscript form a new number. |


<span id="JSON functions"></span>
## JSON functions


|Function |Function Syntax |Description |
|---|---|---|
|JSON_ARRAY_CONTAINS |JSON_ARRAY_CONTAINS(KEY, value) |This function verifies whether a JSON array contains a specific element. |
|JSON_ARRAY_GET |JSON_ARRAY_GET(KEY, index) |This function gets the JSON element corresponding to the specified index in a JSON array. |
|JSON_ARRAY_LENGTH |JSON_ARRAY_LENGTH(KEY) |This function calculates the length of a JSON array, that is, the number of JSON elements. |
|json_EXTRACT |json_EXTRACT(KEY, json_path) |This function extracts a set of JSON values from a JSON object or a JSON array. The JSON values can be of the array or object type. |
|JSON_EXTRACT_SCALAR |JSON_EXTRACT_SCALAR(KEY, json_path) |This function extracts a set of scalar values from a JSON string. The scalar values can be of the string, integer, or Boolean type. |
|JSON_FORMAT |JSON_FORMAT(KEY) |This function converts JSON data to a string. |
|JSON_PARSE |JSON_PARSE(KEY) |This function converts a JSON string to JSON data. |
|JSON_SIZE |JSON_SIZE(KEY, json_path) |This function calculates the number of elements in a JSON object or a JSON array. |


<span id="IP address functions"></span>
## IP address functions


|Function |Syntax |Description |
|---|---|---|
|IP_TO_CITY |IP_TO_CITY(KEY) |This function identifies the city to which an IPv4 address belongs, and returns the Chinese name of the city. |
|IP_TO_CITY |IP_TO_CITY(KEY, 'en') |This function identifies the city to which an IPv4 address belongs, and returns the administrative division code of the city. |
|IP_TO_CITY_GEO |IP_TO_CITY_GEO(KEY) |This function identifies the latitude and longitude of the city to which an IPv4 address belongs. Each city has only one set of coordinates. |
|IP_TO_COUNTRY |IP_TO_COUNTRY(KEY) |This function identifies the country or region to which an IPv4 address belongs, and returns the Chinese name of the country or region. |
|IP_TO_COUNTRY |IP_TO_COUNTRY(KEY, 'en') |This function identifies the country or region to which an IPv4 address belongs, and returns the code of the country or region. |
|IP_TO_DOMAIN |IP_TO_DOMAIN(KEY) |This function verifies whether an IPv4 address is a private or public address. |
|IP_TO_GEO |IP_TO_GEO(KEY) |This function identifies the latitude and longitude of the location of an IPv4 address. |
|IP_TO_PROVIDER |IP_TO_PROVIDER(KEY) |This function identifies the ISP of an IPv4 address. |
|IP_TO_PROVINCE |IP_TO_PROVINCE(KEY) |This function identifies the province to which an IPv4 address belongs, and returns the Chinese name of the province. |
|IP_TO_PROVINCE |IP_TO_PROVINCE(KEY, 'en') |This function identifies the province to which an IPv4 address belongs, and returns the administrative division code of the province. |
|IS_PREFIX_SUBNET_OF |IS_PREFIX_SUBNET_OF(*x*, KEY) |This function verifies whether an IPv4 CIDR block is a subnet of a specified CIDR block. |
|IS_SUBNET_OF |IS_SUBNET_OF(*x*, KEY) |This function verifies whether an IPv4 address is within a specified CIDR block. |
|IP_SUBNET_RANGE |IP_SUBNET_RANGE(KEY) |This function returns the range of an IPv4 CIDR block. |
|IPV6_TO_CITY |IPV6_TO_CITY(KEY) |This function identifies the city to which an IPv6 address belongs. |
|IPV6_TO_CITY_GEO |IPV6_TO_CITY_GEO(KEY) |This function identifies the longitude and latitude of the city to which an IPv6 address belongs. |
|IPV6_TO_COUNTRY |IPV6_TO_COUNTRY(KEY) |This function identifies the country or region to which an IPv6 address belongs. |
|IPV6_TO_DOMAIN |IPV6_TO_DOMAIN(KEY) |This function verifies whether an IPv6 address is a private or public address. |
|IPV6_TO_PROVIDER |IPV6_TO_PROVIDER(KEY) |This function identifies the ISP of an IPv6 address. |
|IPV6_TO_PROVINCE |IPV6_TO_PROVINCE(*x*)) |This function identifies the province to which an IPv6 address belongs. |


<span id="URL functions"></span>
## URL functions


|Function |Function Syntax |Description |
|---|---|---|
|URL_ENCODE |URL_ENCODE(KEY) |This function encodes a URL. |
|URL_DECODE |URL_DECODE(KEY) |This function decodes a URL. |
|URL_EXTRACT_FRAGMENT |URL_EXTRACT_FRAGMENT(KEY) |This function extracts the fragment from a URL. |
|URL_EXTRACT_HOST |URL_EXTRACT_HOST(KEY) |This function extracts the host from a URL. |
|URL_EXTRACT_PARAMETER |URL_EXTRACT_PARAMETER(KEY, parameter name) |This function extracts the value of a specified parameter in the query string from a URL. |
|URL_EXTRACT_PATH |URL_EXTRACT_PATH(KEY) |This function extracts the path from a URL. |
|URL_EXTRACT_PORT |URL_EXTRACT_PORT(KEY) |This function extracts the port number from a URL. |
|URL_EXTRACT_PROTOCOL |URL_EXTRACT_PROTOCOL(KEY) |This function extracts the protocol from a URL. |
|URL_EXTRACT_QUERY |URL_EXTRACT_QUERY(KEY) |This function extracts the query string from a URL. |


<span id="7632c16d"></span>
## Approximate functions


|Function |Function Syntax |Description |
|---|---|---|
|APPROX_PERCENTILE |APPROX_PERCENTILE(KEY, percentage) |This function sorts a set of values in ascending order and returns the KEY value that is approximately at the percentage position. |
||APPROX_PERCENTILE(KEY, array[percentage01, percentage02...]) |This function sorts a set of values in ascending order and returns the KEY values that are approximately at the percentage01 and percentage02 positions. |
||APPROX_PERCENTILE(KEY, weight, percentage) |This function sorts a set of values multiplied by a weight in ascending order and returns the KEY value that is approximately at the percentage position. |
||APPROX_PERCENTILE(KEY, weight, array[percentage01, percentage02...]) |This function sorts a set of values multiplied by a weight in ascending order and returns the KEY values that are approximately at the percentage01 and percentage02 positions. |
||APPROX_PERCENTILE(KEY, weight, percentage, accuracy) |This function sorts a set of values multiplied by a weight in ascending order and returns the value that is approximately at the percentage position. The accuracy can be specified. |


<span id="Binary functions"></span>
## Binary functions


|Function |Function Syntax |Description |
|---|---|---|
|FROM_BASE64 |FROM_BASE64(KEY) |This function converts a Base64\-encoded string to a binary string. |
|FROM_BASE64URL |FROM_BASE64URL(KEY) |This function converts a Base64\-encoded string to a binary string using URL\-safe characters. |
|FROM_HEX |FROM_HEX(KEY) |This function converts a hexadecimal string to a binary string. |
|LENGTH |LENGTH(KEY) |This function computes the length of a binary string. |
|MD5 |MD5(KEY) |This function computes the MD5 hash value for a binary string. |
|TO_BASE64 |TO_BASE64(KEY) |This function converts a binary string to a Base64\-encoded string. |
|TO_BASE64URL |TO_BASE64URL(KEY) |This function converts a binary string to a Base64\-encoded string using URL\-safe characters. |
|TO_HEX |TO_HEX(KEY) |This function converts a binary string to a hexadecimal string. |
|SHA1 |SHA1(KEY) |This function computes the SHA\-1 hash value for a binary string. |
|SHA256 |SHA256(KEY) |This function computes the SHA\-256 hash value for a binary string. |
|SHA512 |SHA512(KEY) |This function computes the SHA\-512 hash value for a binary string. |
|XXHASH64 |XXHASH64(KEY) |This function computes the XXHASH64 hash value for a binary string. |


<span id="Bitwise functions"></span>
## Bitwise functions


|Function |Syntax |Description |
|---|---|---|
|BIT_COUNT |BIT_COUNT(x, bits) |This function counts the number of 1 in the binary representation of x. |
|BITWISE_AND |BITWISE_AND(x, y) |This function returns the result of the bitwise AND operation on x and y. |
|BITWISE_NOT |BITWISE_NOT(x) |This function returns the result of the bitwise NOT operation on x. |
|BITWISE_OR |BITWISE_OR(x, y) |This function returns the result of the bitwise OR operation on x and y. |
|BITWISE_XOR |BITWISE_XOR(x, y) |This function returns the result of the bitwise XOR operation on x and y. |


<span id="Geo functions"></span>
## Geo functions


|Function |Syntax |Description |
|---|---|---|
|GEOHASH |GEOHASH(KEY) |This function encodes latitudes and longitudes using the Geohash algorithm. |


<span id="Color processing functions"></span>
## Color processing functions


|Function |Function Syntax |Description |
|---|---|---|
|BAR |BAR(x, width) |This function returns a part of an ANSI bar chart whose start color is red and end color is green. The width parameter specifies the width of the ANSI bar chart. The x parameter specifies the part to be returned. |
||BAR(x, width, low_color, high_color) |This function returns a part of an ANSI bar chart with a specified start color and end color. The width parameter specifies the width of the ANSI bar chart. The x parameter specifies the part to be returned. |
|COLOR |COLOR(string) |This function converts a color string to a color type. |
||COLOR(x, low, high, low_color, high_color) |This function returns a hybrid color based on the portions of high_color and low_color. The portions are determined by the proportion of x between high and low. |
||COLOR(y, low_color, high_color) |This function returns a hybrid color based on the portions of high_color and low_color. The portions are determined by y. |
|RENDER |RENDER(boolean expression) |This function returns results using default color rendering. If the Boolean expression evaluates to true, the function returns a green tick. Otherwise, the function returns a red cross. |
||RENDER(x, color) |This function returns results using custom color rendering. |
|RGB |RGB(red, green, blue) |This function returns a color value based on a specified RGB value. |


<span id="Phone number processing functions"></span>
## Phone number processing functions


|Function |Syntax |Description |
|---|---|---|
|MOBILE_CARRIER |MOBILE_CARRIER(KEY) |This function returns the ISP of a phone number. |
|MOBILE_CITY |MOBILE_CITY(KEY) |This function returns the city of a phone number. |
|MOBILE_PROVINCE |MOBILE_PROVINCE(KEY) |This function returns the province of a phone number. |


<span id="Unit conversion functions"></span>
## Unit conversion functions


|Function |Syntax |Description |
|---|---|---|
|CONVERT_DATA_SIZE |CONVERT_DATA_SIZE(KEY) |This function converts a measurement from the current unit to the optimal unit determined by the system. |
||CONVERT_DATA_SIZE(KEY, unit) |This function converts a measurement from the current unit to a specified unit. |
|FORMAT_DATA_SIZE |FORMAT_DATA_SIZE(KEY, unit) |This function converts a measurement in bytes to a measurement in a specified unit. |
|PARSE_DATA_SIZE |PARSE_DATA_SIZE(KEY) |This function converts a measurement from the current unit to a measurement in bytes. |
|TO_DATA_SIZE_B |TO_DATA_SIZE_B(KEY) |This function converts a measurement from the current unit to a measurement in bytes. The return value is of the Double type. |
|TO_DATA_SIZE_KB |TO_DATA_SIZE_KB(KEY) |This function converts a measurement from the current unit to a measurement in KB. |
|TO_DATA_SIZE_MB |TO_DATA_SIZE_MB(KEY) |This function converts a measurement from the current unit to a measurement in MB. |
|TO_DATA_SIZE_GB |TO_DATA_SIZE_GB(KEY) |This function converts a measurement from the current unit to a measurement in GB. |
|TO_DATA_SIZE_TB |TO_DATA_SIZE_TB(KEY) |This function converts a measurement from the current unit to a measurement in TB. |
|TO_DATA_SIZE_PB |TO_DATA_SIZE_PB(KEY) |This function converts a measurement from the current unit to a measurement in PB. |
|FORMAT_DURATION |FORMAT_DURATION(KEY) |This function converts a time interval in seconds to a time interval in`xx weeks, xx days, xx hours, xx minutes, xx seconds` format. |
|PARSE_DURATION |PARSE_DURATION(KEY) |This function converts a time interval to a time interval in `0 00:00:00.000` format. |
|TO_DAYS |TO_DAYS(KEY) |This function converts a time interval to a time interval in days. |
|TO_MILLISECONDS |TO_MILLISECONDS(KEY) |This function converts a time interval to a time interval in milliseconds. |
|TO_MINUTES |TO_MINUTES(KEY) |This function converts a time interval to a time interval in minutes. |
|TO_MOST_SUCCINCT_TIME_UNIT |TO_MOST_SUCCINCT_TIME_UNIT(KEY) |This function converts a time interval from the current unit to the optimal unit determined by the system. |
|TO_SECONDS |TO_SECONDS(KEY) |This function converts a time interval to a time interval in seconds. |
|TO_NANOSECONDS |TO_NANOSECONDS(KEY) |This function converts a time interval to a time interval in nanoseconds. |
|TO_MICROSECONDS |TO_MICROSECONDS(KEY) |This function converts a time interval to a time interval in microseconds. |
|TO_HOURS |TO_HOURS(KEY) |This function converts a time interval to a time interval in hours. |


<span id="Window funnel functions"></span>
## Window funnel functions


|Function |Syntax |Description |
|---|---|---|
|WINDOW_FUNNEL |WINDOW_FUNNEL(sliding_window,<br><br>timestamp, event_id, array[event_list01, event_list02...]) |This function searches for an event chain in the sliding time window and counts the maximum number of consecutive events in the event chain.<br><br>Use this syntax if the value of the event_id parameter is specified in an event chain. |
||WINDOW_FUNNEL(sliding_window,<br><br>timestamp, array[event_id=event_list01, event_id=event_list02...]) |This function searches for an event chain in the sliding time window and counts the maximum number of consecutive events in the event chain.<br><br>This syntax is more flexible. Use this syntax if you want to specify values for the event_id parameter. |


<span id="0a5ef297"></span>
## Window functions


|Function |Syntax |Description |
|---|---|---|
|Aggregate functions |/ |Supports the use of aggregate functions in window functions. Please refer to [Aggregate functions](https://docs.byteplus.com/docs/tls/Aggregate-functions-2) for the list of aggregate functions. |
|CUME_DIST |CUME_DIST() |Calculates the cumulative distribution of a row within its window partition, computed as the ratio of the number of rows that are preceding or peer with the current row to the total number of rows in the window partition. |
|DENSE_RANK |DENSE_RANK() |Ranks values within a window partition. |
|FIRST_VALUE |FIRST_VALUE(KEY) |Returns the value of the first row in each window partition. |
|LAG |LAG(KEY, offset, default_value) |Returns the value located `offset` rows above the current row within the partition. |
|LAST_VALUE |LAST_VALUE(KEY) |Returns the value of the last row in each window partition. |
|LEAD |LEAD(KEY, offset, default_value) |Returns the value located `offset` rows below the current row within the partition. |
|NTILE |NTILE(n) |Divides the rows within each window partition into an ordered and approximately equal number of groups, and it returns the group number for each row, starting from 1. |
|NTH_VALUE |NTH_VALUE(KEY, offset) |Returns the KEY value of the row at the specified offset within each window partition. |
|PERCENT_RANK |PERCENT_RANK() |Calculates the relative position of each row within each window partition, expressed as a percentage. |
|RANK |RANK() |Calculates the rank of each data row in each window partition. The same value in the same partition will receive the same ranking, and the ranking of the next value will skip these duplicate ranking values. F |
|ROW_NUMBER |ROW_NUMBER() |Calculates the rank of each data row in each window partition. Each value has a unique sequence number, starting with 1. |


<span id="b8c68139"></span>
## Type conversion functions


|Function |Function Syntax |Description |
|---|---|---|
|CAST |CAST(KEY AS type) |This function converts the data type of the KEY. |
|TRY_CAST |TRY_CAST(KEY AS type) |This function converts the data type of the KEY. |
|TYPEOF |TYPEOF(KEY) |This function returns the data type of the Key. |


<span id="d0859305"></span>
## HyperLogLog functions


|Function |Function syntax |Description |
|---|---|---|
|APPROX_SET |APPROX_SET(KEY) |This function estimates the number of distinct values in the KEY field. |
|EMPTY_APPROX_SET |EMPTY_APPROX_SET() |This function constructs a null value of the HyperLogLog data type. |
|MERGE |MERGE(KEY) |This function merges multiple HyperLogLogLogs into one HyperLogLog. |
