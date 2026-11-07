---
title: "Common functions"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/common-functions-collection"
---

<span id="算数计算"></span>
# Arithmetic calculations

| | | \
|**Function** |**Function Description** |
|---|---|
| | | \
|plus(a,b) |\
|a+b |Addition |
| | | \
|minus(a,b) |\
|a-b |Subtraction |
| | | \
|multiply(a,b) |\
|a*b |Multiplication |
| | | \
|divide(a,b) |\
|a/b |Division |
| | | \
|intDiv(a,b) |Divide by an integer, round down |
| | | \
|intDivOrZero(a,b) |Divide by 0 returns 0 |
| | | \
|modulo(a,b) |\
|a%b |Modulo |
| | | \
|moduloOrZero(a,b) |Returning zero when modulo zero |
| | | \
|negate(a), |\
|-a |Negative |
| | | \
|abs(a) |Absolute value |
| | | \
|gcd(a,b) |Greatest Common Divisor |
| | | \
|lcm(a,b) |Least Common Multiple |

<span id="日期-时间"></span>
# Date & time

| | | \
|Function |Function Description |
|---|---|
| | | \
|timeZone |Server Time Zone |
| | | \
|toTimeZone |Change Time Zone |
| | | \
|timeZoneOf |Back specific date timezone |
| | | \
|timeZoneOffset |Back and UTC time zone difference (seconds) |
| | | \
|toYear |Back to year |
| | | \
|toQuarter |Back to quarters |
| | | \
|toMonth |Back to Month |
| | | \
|toDayOfYear |Back to the day of the year |
| | | \
|toDayOfMonth |Back to Oh, my God. |
| | | \
|toDayOfWeek |Back to week |
| | | \
|toHour |Back to hour(s) |
| | | \
|toMinute |Back to minute(s) |
| | | \
|toSecond |Return seconds |
| | | \
|toUnixTimestamp |Convert to unix timestamp |
| | | \
|toStartOfYear |Convert to the first day of the year |
| | | \
|toStartOfISOYear |Convert to the first day of the ISO year |
| | | \
|toStartOfQuarter |Convert to the first day of the quarter |
| | | \
|toStartOfMonth |Convert to the first day of the month |
| | | \
|toMonday |Convert to the latest Monday |
| | | \
|toStartOfWeek(t[,mode]) |Convert to the start of the week |
| | | \
|toStartOfDay |Convert to the start of the current day |
| | | \
|toStartOfHour |Convert to the start of the current hour |
| | | \
|toStartOfMinute |Convert to the start of the current minute |
| | | \
|toStartOfSecond |Convert to the start of the current second |
| | | \
|toStartOfFiveMinutes |Start Time by 5-minute intervals |
| | | \
|toStartOfTenMinutes |Start Time by 10-minute intervals |
| | | \
|toStartOfFifteenMinutes |Start Time by 15-minute intervals |
| | | \
|toStartOfInterval(time_or_data, INTERVAL x unit [, time_zone]) |Start Time By Specified Time Type |
| | | \
|toTime |Convert to Time |
| | | \
|toISOYear |Convert to ISO Year |
| | | \
|toISOWeek |Convert to ISO Week |
| | | \
|toWeek(date[,mode]) |Convert to Number of Weeks |
| | | \
|toYearWeek(date[,mode]) |Convert to year + number of weeks |
| | | \
|date_trunc |According to a specific date |
| | | \
|date_add |Add a specific date unit |
| | | \
|date_diff |Time difference between two dates |
| | | \
|date_sub |Date subtraction |
| | | \
|timestamp_add |timestamp add specific date unit |
| | | \
|timestamp_sub |timestamp subtract specific date unit |
| | | \
|now |Time |
| | | \
|today |One day |
| | | \
|yesterday |Last day |
| | | \
|timeSlot |Rounding to the nearest half hour |
| | | \
|toYYYYMM |Convert to year, month format |
| | | \
|toYYYYMMDD |Convert to year, month, day format |
| | | \
|toYYYYMMDDhhmmss |Convert to year, month, day, hour, minute, second format |
| | | \
|addYears, addMonths, addWeeks, addDays, addHours, addMinutes, addSeconds, addQuarters |Add different date or time dimensions |
| | | \
|subtractYears, subtractMonths, subtractWeeks, subtractDays, subtractHours, subtractMinutes, subtractSeconds, subtractQuarters |Subtract different dates or time dimensions |
| | | \
|formatDateTime |Format the date |
| | | \
|dateName |Return the specified part of the date |
| | | \
|FROM_UNIXTIME |Convert Unix time to DateTime |

<span id="字符串"></span>
# String functions

| | | \
|Function |Function Description |
|---|---|
| | | \
|empty |Returns if the input is empty |
| | | \
|notEmpty |Returns if the input is not empty |
| | | \
|length |String length |
| | | \
|lengthUTF8 |Returns the length of a string in Unicode code points |
| | | \
|char_length, CHAR_LENGTH |As above |
| | | \
|character_length, CHARACTER_LENGTH |The same as above. |
| | | \
|leftPad |Padding is added to the left side of the current string until it reaches the specified length. |
| | | \
|leftPadUTF8 |The function is the same as above, except the length is calculated in bytes. |
| | | \
|rightPad |Padding is added to the right side of the current string until it reaches the specified length. |
| | | \
|rightPadUTF8 |The function is the same as above, except the length is calculated in bytes. |
| | | \
|lower, lcase |Convert to lowercase |
| | | \
|upper, ucase |Convert to uppercase |
| | | \
|lowerUTF8 |Convert to lowercase; if the string contains a byte sequence that is not valid UTF-8, then the behavior is undefined |
| | | \
|upperUTF8 |Convert to uppercase; if the string contains a byte sequence that is not a valid UTF-8, then the behavior is undefined |
| | | \
|isValidUTF8 |Input is valid UTF-8 encoding |
| | | \
|toValidUTF8 |Replace invalid UTF-8 characters with � (U+FFFD) character |
| | | \
|repeat |Repeat a string a specified number of times |
| | | \
|reverse |Reverse string |
| | | \
|reverseUTF8 |Reverse a string in the sequence of Unicode |
| | | \
|format(pattern, s0, s1, …) |Formatted string |
| | | \
|concat |String concatenation |
| | | \
|concatAssumeInjective |Same as above, commonly used for Group by optimization |
| | | \
|substring(s, offset, length), mid(s, offset, length), substr(s, offset, length) |Substring of string |
| | | \
|substringUTF8(s, offset, length) |The same as above, length measured in Unicode |
| | | \
|appendTrailingCharIfAbsent(s, c) |If the 's' string is not empty and does not end with the 'c' character, it adds the 'c' character to the end |
| | | \
|convertCharset(s, from, to) |Returns the string 's' converted from encoding in 'from' to encoding in 'to' |
| | | \
|base64Encode(s) |Encode the string 's' into base64 |
| | | \
|base64Decode(s) |Decode the base64 encoded string 's' into the original string |
| | | \
|tryBase64Decode(s) |If decoding errors occur, return an empty string |
| | | \
|endsWith(s, suffix) |Returns whether it ends with the specified suffix |
| | | \
|startsWith(str, prefix) |Ends with the specified prefix |
| | | \
|trim |Remove all specified characters from either the beginning or the end of a string. By default, remove all continuously appearing normal spaces from both ends of a string |
| | | \
|trimLeft |Delete leading spaces continuously appearing |
| | | \
|trimRight |Delete trailing spaces continuously appearing |
| | | \
|trimBoth |Delete continuous normal spaces on both ends |
| | | \
|CRC32(s) |CRC32 check, initial value 0xffffffffff |
| | | \
|CRC32IEEE(s) |CRC32 check |
| | | \
|CRC64(s) |CRC64 check |
| | | \
|normalizeQuery |Replace with placeholders |
| | | \
|normalizedQueryHash |64-bit hash value, generally used for log analysis |

<span id="类型转换"></span>
# Type conversion

| | | | | | | | | | \
|Function |Function description |null |null |null |null |null |null |null |
|---|---|---|---|---|---|---|---|---|
| | | | | | | | | | \
|toInt(8 |16 |32 |64 |128 |256) |Convert to Int type |null |null |
| | | | | | | | | | \
|toInt(8 |16 |32 |64 |128 |256)OrZero |Convert to Int type, return 0 if unsuccessful |null |null |
| | | | | | | | | | \
|toInt(8 |16 |32 |64 |128 |256)OrNull |Convert to Int type, if failed return Null |null |null |
| | | | | | | | | | \
|toInt(8 |16 |32 |64 |128 |256)OrDefault |Convert to Int type, return default value if failed |null |null |
| | | | | | | | | | \
|toUInt(8 |16 |32 |64 |256) |Convert to UInt type |null |null |null |
| | | | | | | | | | \
|toUInt(8 |16 |32 |64 |256)OrZero |Convert to UInt type, if failed return 0 |null |null |null |
| | | | | | | | | | \
|toUInt(8 |16 |32 |64 |256)OrNull |Convert to UInt type, if failed return Null |null |null |null |
| | | | | | | | | | \
|toUInt(8 |16 |32 |64 |256)OrDefault |Convert to UInt type; if failed, return default value |null |null |null |
| | | | | | | | | | \
|toFloat(32 |64) |Convert to Float type |null |null |null |null |null |null |
| | | | | | | | | | \
|toFloat(32 |64)OrZero |Convert to Float type; if failed, return 0 |null |null |null |null |null |null |
| | | | | | | | | | \
|toFloat(32 |64)OrNull |Convert to Float type; if failed, return Null |null |null |null |null |null |null |
| | | | | | | | | | \
|toFloat(32 |64)OrDefault |Convert to Float type, if failed return the default value |null |null |null |null |null |null |
| | | | | | | | | | \
|toDate |Convert to Date type |null |null |null |null |null |null |null |
| | | | | | | | | | \
|toDateOrZero |Convert to Date type, return 0 if failed |null |null |null |null |null |null |null |
| | | | | | | | | | \
|toDateOrNull |Convert to Date type, return null if failed |null |null |null |null |null |null |null |
| | | | | | | | | | \
|toDateOrDefault |Convert to Date type, return default value if failed |null |null |null |null |null |null |null |
| | | | | | | | | | \
|toDateTime |Convert to DateTime type |null |null |null |null |null |null |null |
| | | | | | | | | | \
|toDateTimeOrZero |Convert to DateTime type, return 0 if failed |null |null |null |null |null |null |null |
| | | | | | | | | | \
|toDateTimeOrNull |Convert to DateTime type, if it fails return Null |null |null |null |null |null |null |null |
| | | | | | | | | | \
|toDateTimeOrDefault |Convert to DateTime type, if it fails return the default value |null |null |null |null |null |null |null |
| | | | | | | | | | \
|toDate32 |Convert to Date32 type |null |null |null |null |null |null |null |
| | | | | | | | | | \
|toDate32OrZero |Convert to Date32 type, if it fails return 0 |null |null |null |null |null |null |null |
| | | | | | | | | | \
|toDate32OrNull |Convert to Date32 type, if it fails return Null |null |null |null |null |null |null |null |
| | | | | | | | | | \
|toDate32OrDefault |Convert to Date32 type; if failed, return default value |null |null |null |null |null |null |null |
| | | | | | | | | | \
|toDecimal(32 |64 |128 |256) |Convert to Decimal type |null |null |null |null |
| | | | | | | | | | \
|toDecimal(32 |64 |128 |256)OrNull |Convert to Decimal type, return 0 if failed |null |null |null |null |
| | | | | | | | | | \
|toDecimal(32 |64 |128 |256)OrDefault |Convert to Decimal type, return Null if failed |null |null |null |null |
| | | | | | | | | | \
|toDecimal(32 |64 |128 |256)OrZero |Convert to Decimal Type, return default value if failed |null |null |null |null |
| | | | | | | | | | \
|toString |Convert to String Type |null |null |null |null |null |null |null |
| | | | | | | | | | \
|toFixedString(s, N) |Convert to String Type, return a fixed length of N string |null |null |null |null |null |null |null |
| | | | | | | | | | \
|reinterpretAsUInt(8 |16 |32 |64) |Convert to UInt Type |null |null |null |null |
| | | | | | | | | | \
|reinterpretAsInt(8 |16 |32 |64) |Convert Int type |null |null |null |null |
| | | | | | | | | | \
|reinterpretAsFloat(32 |64) |Convert Float type |null |null |null |null |null |null |
| | | | | | | | | | \
|reinterpretAsDate |Convert Date type |null |null |null |null |null |null |null |
| | | | | | | | | | \
|reinterpretAsDateTime |Convert DateTime type |null |null |null |null |null |null |null |
| | | | | | | | | | \
|reinterpretAsString |Convert String type |null |null |null |null |null |null |null |
| | | | | | | | | | \
|CAST(x, T) |Attempt to represent the same value using a new data type. If the conversion cannot be completed, it will result in an exception |null |null |null |null |null |null |null |
| | | | | | | | | | \
|accurateCast(x, T) |If the type value x does not adhere to the bounds of T, accurateCast does not allow number types to overflow during the cast process |null |null |null |null |null |null |null |
| | | | | | | | | | \
|accurateCastOrNull(x, T) |If the conversion is abnormal, return Null |null |null |null |null |null |null |null |
| | | | | | | | | | \
|accurateCastOrDefault(x, T, default_value) |If conversion is abnormal, return the default value |null |null |null |null |null |null |null |
| | | | | | | | | | \
|toInterval(Year |Quarter |Month |Week |Day |Hour |Minute |Second) |Return different date interval intervals |
| | | | | | | | | | \
|parseDateTimeBestEffort |Convert the date and time represented by the string into the DateTime Data type |null |null |null |null |null |null |null |
| | | | | | | | | | \
|parseDateTime32BestEffort |I convert dates and times represented as strings to the DateTime32 data type |null |null |null |null |null |null |null |
| | | | | | | | | | \
|parseDateTimeBestEffortUS |In unclear situations, there's a preference for the American date format (MM/DD/YYYY and others) |null |null |null |null |null |null |null |
| | | | | | | | | | \
|parseDateTimeBestEffortOrNull |Like parseDateTimeBestEffort, it returns Null if the conversion fails |null |null |null |null |null |null |null |
| | | | | | | | | | \
|parseDateTime32BestEffortOrNull |Like parseDateTime32BestEffort, if it can't convert, it returns Null |null |null |null |null |null |null |null |
| | | | | | | | | | \
|parseDateTimeBestEffortOrZero |Like parseDateTimeBestEffort, if it can't convert, it returns Zero |null |null |null |null |null |null |null |
| | | | | | | | | | \
|parseDateTime32BestEffortOrZero |Like parseDateTime32BestEffort, if it can't convert, it returns Zero |null |null |null |null |null |null |null |
| | | | | | | | | | \
|parseDateTimeBestEffortUSOrNull |Like parseDateTimeBestEffortUS, if it can't convert, it returns Null |null |null |null |null |null |null |null |
| | | | | | | | | | \
|parseDateTimeBestEffortUSOrZero |Like parseDateTimeBestEffortUS, if it can't convert, it returns Zero |null |null |null |null |null |null |null |
| | | | | | | | | | \
|parseDateTime64BestEffort |Converts a string representation of a Date and Time to the DateTime64 Data type |null |null |null |null |null |null |null |
| | | | | | | | | | \
|parseDateTime64BestEffortOrNull |Like parseDateTime64BestEffort, returns Null if conversion cannot be performed |null |null |null |null |null |null |null |
| | | | | | | | | | \
|parseDateTime64BestEffortOrZero |Like parseDateTime64BestEffort, returns Zero if conversion fails |null |null |null |null |null |null |null |
| | | | | | | | | | \
|toLowCardinality |Converts to the same Data type of LowCardinality |null |null |null |null |null |null |null |
| | | | | | | | | | \
|toUnixTimestamp64Milli |Returns UnixTimestamp64, ms level |null |null |null |null |null |null |null |
| | | | | | | | | | \
|toUnixTimestamp64Micro |Return UnixTimestamp64, microsecond level |null |null |null |null |null |null |null |
| | | | | | | | | | \
|toUnixTimestamp64Nano |Return UnixTimestamp64, nanosecond level |null |null |null |null |null |null |null |
| | | | | | | | | | \
|fromUnixTimestamp64Milli |Convert Int64 to DateTime64, input in milliseconds |null |null |null |null |null |null |null |
| | | | | | | | | | \
|fromUnixTimestamp64Micro |Convert Int64 to DateTime64, input in microseconds |null |null |null |null |null |null |null |
| | | | | | | | | | \
|fromUnixTimestamp64Nano |Convert Int64 to DateTime64, input in nanoseconds |null |null |null |null |null |null |null |
| | | | | | | | | | \
|formatRow |The specified format converts any expression to a string |null |null |null |null |null |null |null |
| | | | | | | | | | \
|formatRowNoNewline |As above, trailing newline will be trimmed |null |null |null |null |null |null |null |

<span id="标准聚合函数"></span>
# Standard aggregate functions

| | | \
|Function |Function Description |
|---|---|
| | | \
|count |Count |
| | | \
|min |Minimum Value |
| | | \
|max |Maximum value |
| | | \
|sum |Sum |
| | | \
|avg |Average value |
| | | \
|any |Select the first encountered value |
| | | \
|stddevPop |Equal to the square root of varPop |
| | | \
|stddevSamp |Equal to the square root of varSamp |
| | | \
|varPop |Σ((x - x̅)^2) / n, where n is the sample size, and x̅ is the mean of x. |
| | | \
|varSamp |Σ((x - x̅)^2) / (n - 1), where n is the sample size, and x̅ is the mean of x. |
| | | \
|covarPop(x,y) |Σ((x - x̅)(y - y̅)) / n |
| | | \
|covarSamp(x,y) |Σ((x - x̅)(y - y̅)) / (n - 1) |

<span id="高级聚合函数"></span>
# Advanced aggregate functions

| | | \
|Function |Function description |
|---|---|
| | | \
|anyHeavy |Select a frequently occurring value using the heavy hitter algorithm |
| | | \
|anyLast |Choose the last encountered value |
| | | \
|argMin(arg, val) |Calculate the arg value for the minimum val |
| | | \
|argMax(arg, val) |Calculate the arg value for the maximum val |
| | | \
|avgWeighted |Calculate the weighted arithmetic mean. |
| | | \
|topK |Return an array of the approximately most frequent values in the specified column. |
| | | \
|topKWeighted |Return an array of the approximately most frequent values in the specified column, taking into account data weights for the calculation logic. |
| | | \
|groupArray |Create an array. Values can be added to the array in any (uncertain) order. |
| | | \
|groupUniqArray |Create a unique array. Values can be added to the array in any (indeterminate) order. |
| | | \
|groupArrayInsertAt |Insert a value into an array at a specified position. |
| | | \
|groupArrayMovingAvg |Calculate the moving average of the input values. |
| | | \
|groupArrayMovingSum |Calculate the total sum of movements for the input values. |
| | | \
|groupBitAnd |Perform a bitwise logical AND operation on a series of numeric bits. |
| | | \
|groupBitOr |Bit logic OR operation on a series of numbers |
| | | \
|groupBitXor |Bit logic XOR operation on a series of numbers |
| | | \
|groupBitmap |Using Bitmap data type, returns the cardinality (distinct count) of input fields |
| | | \
|groupBitmapAnd |Cardinality (distinct count) after bit logic AND operation |
| | | \
|groupBitmapOr |Cardinality (distinct count) after bit logic OR operation |
| | | \
|groupBitmapXor |Calculate the cardinality (distinct count) after performing a bitwise XOR logical operation |
| | | \
|sumWithOverflow |Calculate the total sum of numbers, using the same data type as the input parameters If the sum exceeds the maximum value of that data type, calculate it as an overflow |
| | | \
|sumMap(key,value) |Based on the keys specified in the key array, sum up the values in the value array |
| | | \
|minMap(key,value) |For the keys specified in the key array, return the minimum value from the value array |
| | | \
|maxMap |Return the maximum value from the value array based on the specified key in the key array |
| | | \
|skewSamp |Calculate the sample skewness of a sequence |
| | | \
|skewPop |Calculate the skewness of a sequence |
| | | \
|kurtSamp |Calculate the sample kurtosis of a sequence |
| | | \
|kurtPop |Calculate the kurtosis of a sequence |
| | | \
|uniq |Calculate an approximate quantity of a sequence |
| | | \
|uniqExact |Calculate the exact de-duplication quantity of a sequence |
| | | \
|uniqCombined |Using approximation algorithms |
| | | \
|uniqCombined64 |Using approximation algorithms |
| | | \
|uniqHLL12 |Using approximation algorithms, the HyperLogLog algorithm |
| | | \
|uniqTheta |Adopts the Theta Sketch approximation algorithm |
| | | \
|quantile |Approximate quartiles of a sequence |
| | | \
|quantileExact |Accurately calculates the quartiles of a sequence |
| | | \
|quantileExactLow |Similar to quantileExact, returns the lowest value in cases of multiple values |
| | | \
|quantileExactHigh |Similar to quantileExact, returns the highest value in cases of multiple values |
| | | \
|quantileExactWeighted |Accurately calculate the quartiles of the sequence, computational logic with weight |
| | | \
|quantileTiming |Calculate quantile with confirmed precision |
| | | \
|quantileTimingWeighted |Calculate quantile with confirmed precision, computational logic with weight |
| | | \
|quantileDeterministic |Approximate the calculation of quantile |
| | | \
|quantileTDigest |Use the t-digest algorithm to approximate the calculation of quantile |
| | | \
|quantileTDigestWeighted |Use t-digest algorithm for approximate calculation of quantile, computational logic includes weights |
| | | \
|quantileBFloat16 |Bfloat16 sample approximate calculation of quantile |
| | | \
|quantileBFloat16Weighted |Bfloat16 sample approximate calculation of quantile, computational logic includes weights |
| | | \
|median* |Equivalent quantile* function |
| | | \
|simpleLinearRegression |Simple Linear Regression |
| | | \
|stochasticLinearRegression |Random linear regression |
| | | \
|stochasticLogisticRegression |Random logistic regression |

<span id="数学运算"></span>
# Mathematical operations

| | | \
|Function |Function description |
|---|---|
| | | \
|e() |Returns Float64, approximating the constant e |
| | | \
|pi() |Returns Float64, approximating the constant pi |
| | | \
|exp(x) |Exponential Calculation |
| | | \
|log(x), ln(x) |Logarithmic Calculation |
| | | \
|exp2(x) |Exponential Base-2 Calculation |
| | | \
|log2(x) |Base-2 Logarithmic Calculation |
| | | \
|exp10(x) |Exponential Base-10 Calculation |
| | | \
|log10(x) |Logarithmic calculation, base 10 |
| | | \
|sqrt(x) |Square root |
| | | \
|cbrt(x) |Cube root |
| | | \
|sin(x) |Sine function sin |
| | | \
|cos(x) |Cosine function cos |
| | | \
|tan(x) |Trigonometric function tan |
| | | \
|asin(x) |Asin trigonometric function |
| | | \
|acos(x) |Arccosine function in trigonometry |
| | | \
|atan(x) |The arctangent function atan |
| | | \
|pow(x, y), power(x, y) |x to the power of y |
| | | \
|cosh(x) |Hyperbolic cosine function cosh |
| | | \
|acosh(x) |Hyperbolic cosine inverse function acosh |
| | | \
|sinh(x) |Hyperbolic sine function sinh |
| | | \
|asinh(x) |Hyperbolic sine inverse function asinh |
| | | \
|atanh(x) |Hyperbolic tangent function atanh |

<span id="其他函数"></span>
# Other functions
Please refer to the [support functions](https://github.com/ClickHouse/ClickHouse/tree/21.8/docs/en/sql-reference/functions) of ClickHouse open source version 21.8.
