---
title: "Integer function"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/integer-function"
---

<span id="floor-x-n"></span>
## floor(x[,N])
Returns the largest integer less than or equal to x. This function multiplies the parameter by 1/10N; if 1/10N is not precise, it selects the closest accurate number of an appropriate data type. 'N' is an integer constant, an optional parameter. Defaults to 0, which means no rounding is applied. 'N' can be a negative number.
Example: `floor(123.45, 1) = 123.4, floor(123.45, -1) = 120.`
`x` can be of any numeric type. The result is of the same type as x. For integer parameters, using a negative 'N' value for rounding makes sense (for non-negative "N", the function does nothing). If rounding leads to overflow (for example, floor(-128, -1)), it returns a result specific to the implementation.
<span id="ceil-x-n"></span>
## ceil(x[,N])
Returns the smallest rounding number that is greater than or equal to 'x'. In other respects, it functions the same as 'floor' (see above).
<span id="round-x-n"></span>
## round(x[,N])
Rounds the value to a specified number of decimal places.
The function returns the closest number in sequence. If multiple nearest numbers are present, the function returns the one closest to an even number (bankers' rounding).
```plaintext
round(expression [, decimal_places])
```

Parameters:

* `Expression` — Number to be rounded. Can be any expression that returns a number type.
* `Decimal-places` — Integer type.
   * If `decimal-places > 0`, the function rounds the value to the right of the decimal point.
   * If `decimal-places < 0`, the function rounds the value to the left of the decimal point.
   * If `decimal-places = 0`, the function rounds the value to an integer. In this case, the parameter can be omitted.

Return Value:
Number rounded to the same type as the input number.
<span id="示例"></span>
### Example
Usage Example
SELECT number / 2 AS x, round(x) FROM system.numbers LIMIT 3
```plaintext
┌───x─┬─round(divide(number, 2))─┐
│   0 │                        0 │
│ 0.5 │                        0 │
│   1 │                        1 │
└─────┴──────────────────────────┘
```

Example of Rounding
Round to the nearest number:
```plaintext
round(3.2, 0) = 3
round(4.1267, 2) = 4.13
round(22,-1) = 20
round(467,-2) = 500
round(-467,-2) = -500
```

The rounding method of the bank:
```plaintext
round(3.5) = 4
round(4.5) = 4
round(3.55, 1) = 3.6
round(3.65, 1) = 3.6
```

<span id="roundtoexp2-num"></span>
## roundToExp2(num)
Accepts a number. If the number is less than 1, return 0. Otherwise, it rounds the number down to the nearest (whole non-negative) power of two.
<span id="roundduration-num"></span>
## **roundDuration**(num)
Accept a number. If the number is less than 1, return 0. Otherwise, it rounds down the number to the nearest value in this set: 1, 10, 30, 60, 120, 180, 240, 300, 600, 1200, 1800, 3600, 7200, 18000, 36000. This function is used in Yandex.Metrica reports to calculate the duration of a session.
<span id="roundage-num"></span>
## **roundAge**(num)
Accept a number. If the number is less than 18, return 0. Otherwise, it rounds down the number to the nearest value in this set: 18, 25, 35, 45, 55. This function is used in Yandex.Metrica reports for calculating user age.
<span id="rounddown-num-arr"></span>
## roundDown(num,arr)
Accept a number and round it down to an element in the specified array. If the value is lower than the smallest boundary in the array, return that smallest boundary.
