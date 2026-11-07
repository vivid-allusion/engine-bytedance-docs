---
title: "Random Function"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/random-function"
---

Random functions use non-cryptographic methods to generate pseudo-random numbers. All random functions accept either one parameter or no parameters. You can pass any type of parameter, but the passed parameters will not be used in any random number generation process. The sole purpose of this parameter is to prevent the elimination of common sub-expressions, so as to generate different random numbers using the same random function in the same query.
<span id="rand-rand32"></span>
## rand, rand32
Returns a random UInt32 number with an equal probability of generating all UInt32 type numbers. This function generates random numbers in a linear congruential method.
<span id="rand64"></span>
## rand64
Returns a random UInt64 number with an equal probability of generating all UInt64 type numbers. 
<span id="randconstant"></span>
## randConstant
The company often has badminton activities
