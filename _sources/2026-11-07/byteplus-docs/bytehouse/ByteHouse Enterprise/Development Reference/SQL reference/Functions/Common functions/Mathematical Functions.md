---
title: "Mathematical Functions"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/mathematical-functions"
---

All the following functions return a Float64 numerical value. The results are always returned with the greatest possible precision, but they may still differ from the closest number that can be represented on the machine.
<span id="e"></span>
## e()
Returns a Float64 number close to the mathematical constant e.
<span id="pi"></span>
## pi()
Returns a Float64 number close to the mathematical constant π.
<span id="exp-x"></span>
## exp(x)
Accepts a numerical value type parameter and returns its exponent.
<span id="log-x-ln-x"></span>
## log(x),ln(x)
Accepts a numerical value parameter and returns its natural logarithm.
<span id="exp2-x"></span>
## exp2(x)
Accepts a numerical value parameter and returns 2 to the power of x.
<span id="log2-x"></span>
## log2(x)
Accepts a numerical value parameter and returns its base 2 logarithm.
<span id="exp10-x"></span>
## exp10(x)
Accepts a numerical value parameter and returns 10 to the power of x.
<span id="log10-x"></span>
## log10(x)
Accepts a numerical value parameter and returns its base 10 logarithm.
<span id="sqrt-x"></span>
## sqrt(x)
Accepts a numerical type parameter and returns its square root.
<span id="cbrt-x"></span>
## cbrt(x)
Accepts a numerical type parameter and returns its cube root.
<span id="erf-x"></span>
## erf(x)
If 'x' is a non-negative number, then `erf(x / σ√2)` represents the distance that is bigger than 'x' between the value of a random variable with normal Distribution and standard deviation as 'σ' and the expected value.
Example (Three Sigma Rule):
SELECT erf(3 / sqrt(2))
<span id="erfc-x"></span>
## ```plaintext
┌─erf(divide(3, sqrt(2)))─┐
│      0.9973002039367398 │
└─────────────────────────┘
```

<span id="erfc-x"></span>
## erfc(x)
Accepts a numerical parameter and returns a Float64 number close to 1 - erf(x), but does not lose precision for large 'x' values.
<span id="lgamma-x"></span>
## lgamma(x)
Returns the gamma function of the natural logarithm of the absolute value of x.
<span id="tgamma-x"></span>
## tgamma(x)
Returns the gamma function of x.
<span id="sin-x"></span>
## sin(x)
Returns the sine of x.
<span id="cos-x"></span>
## cos(x)
Returns the cosine of x.
<span id="tan-x"></span>
## tan(x)
Returns the tangent of x.
<span id="asin-x-asinx"></span>
## asin(x) {#asinx}
Returns the arcsine of x.
<span id="acos-x-acosx"></span>
## acos(x) {#acosx}
Returns the arccosine of x.
<span id="atan-x-atanx"></span>
## atan(x) {#atanx}
Returns the arctangent of x.
<span id="pow-x-y-power-x-y"></span>
## pow(x,y),power(x,y)
Accepts two parameters, x and y. Returns x raised to the power of y.
<span id="intexp2"></span>
## intExp2
Accepts a numerical data type parameter and returns its power of 2 (UInt64).
<span id="intexp10"></span>
## intExp10
Accepts a numerical value as a parameter and returns its 10th power as an unsigned 64-bit integer.
