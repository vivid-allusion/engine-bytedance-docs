---
title: "Hash function"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/hash-function"
---

Hash functions are used to irreversibly and pseudorandomly scramble elements.

<span id="halfmd5"></span>
## halfMD5

Calculate the MD5 of a string. Then, acquire the first 8 bytes of the result and return them as UInt64 (big endian). This function is quite inefficient (5 million short strings/second/core). If you do not need to specifically use MD5, please use the 'sipHash64' function.

<span id="md5"></span>
## MD5

Calculate the MD5 of a string and return the result in FixedString(16). If you only need a 128\-bit hash and do not specifically need to use MD5, please use the 'sipHash128' function. If you want to obtain the same output as the md5sum program, use lower(hex(MD5(s))).

<span id="siphash64"></span>
## sipHash64

Calculate the SipHash of a string. Accepts a String type parameter and returns UInt64. SipHash is an encrypted hash function. Its processing performance is at least three times faster than that of MD5. For more details, refer to [https://131002.net/siphash/](https://131002.net/siphash/)

<span id="siphash128"></span>
## linksipHash128

Calculate the SipHash of a string. Accepts a String type parameter and returns FixedString(16). The difference with the sipHash64 function is that its final calculation results in 128 bits.

<span id="cityhash64"></span>
## cityHash64

Calculate the CityHash64 for any number of strings or use a specific implementation of Hash function to calculate the hash for any other types. For strings, use the CityHash algorithm. This is a fast non\-cryptographic hash function for strings. For other types of parameters, use a specific implementation of Hash function, a fast non\-cryptographic hash function. If multiple parameters are passed, use CityHash to combine the hash results of these parameters. For example, you can calculate the checksum of an entire table, the result depends on the order of the rows: `SELECT sum(cityHash64(*)) FROM table`.

<span id="inthash32"></span>
## intHash32

Calculate a 32\-bit hash for any type of integer. This is a relatively efficient non\-encrypted hash function.

<span id="inthash64"></span>
## intHash64

Calculates a 64\-bit hash code from any type of integer. It works faster than the intHash32 function.

<span id="sha1、sha224、sha256"></span>
## SHA1、SHA224、SHA256

Calculates the SHA\-1, SHA\-224, or SHA\-256 of strings and returns the result as FixedString(20), FixedString(28), or FixedString(32). This function is quite inefficient (SHA\-1 approximates 5 million short strings per second per core, while SHA\-224 and SHA\-256 approximate 2.2 million short strings per second per core). We recommend using these functions only when it is necessary and cannot be changed. Even in these cases, we still recommend using the method of precomputing the functions during data entry to complete the calculations. Rather than calculating them in SELECT.

<span id="urlhash-url-n"></span>
## URLHash(url[,N])

A fast non\-encrypting hash function used for normalizing strings acquired from URLs. `URLHash(s)` \- Calculates a hash from a string, ignoring trailing symbols `/`, `?` or `#` if present. `URLHash(s, N)` \- Calculates the hash value of a string up to the N level in the URL hierarchy, ignoring trailing symbols `/`, `?` or `#` if present. The levels in URLs are the same as those in URLHierarchy. This function is used in Yandex.Metrica.

<span id="farmhash64"></span>
## farmHash64

Calculates the FarmHash64 of a string. Accepts a parameter of String type. Returns UInt64. For more details, please see the link: [FarmHash64](https://github.com/google/farmhash).

<span id="b6a1fe57"></span>
## javaHash

Calculates the JavaHash of a string. Accepts a parameter of String type. Returns Int32. For more information, please see the link: [JavaHash](http://hg.openjdk.java.net/jdk8u/jdk8u/jdk/file/478a4add975b/src/share/classes/java/lang/String.java#l1452).

<span id="0032ecc1"></span>
## hiveHash

Calculates the HiveHash of a string. Accepts a parameter of type String. Returns Int32. Same as [JavaHash](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/en/sql-reference/functions/hash-functions.md#hash_functions-javahash), but does not return a negative number.

<span id="metrohash64"></span>
## metroHash64

Calculates the MetroHash of a string. Accepts a parameter of type String. Returns UInt64. For more details, refer to [MetroHash64](https://www.jandrewrogers.com/2015/05/27/metrohash/).

<span id="jumpconsistenthash"></span>
## jumpConsistentHash

Calculates the JumpConsistentHash for UInt64. Accepts a UInt64 type parameter. Returns Int32. For more information, please see the link: [JumpConsistentHash](https://arxiv.org/pdf/1406.2294.pdf)

<span id="a2961020"></span>
## murmurHash2_32,murmurHash2_64

Calculates the MurmurHash2 of a string. Accepts a string type parameter. Returns UInt64 or UInt32. For more information, please see the link: [MurmurHash2](https://github.com/aappleby/smhasher)

<span id="efb941b7"></span>
## murmurHash3_32,murmurHash3_64,murmurHash3_128

Calculates the MurmurHash3 of a string. Accepts a string type parameter. Returns UInt64 or UInt32 or FixedString(16). For more details, please refer to the link: [MurmurHash3](https://github.com/aappleby/smhasher)

<span id="8898fabf"></span>
## xxHash32,xxHash64

Calculates the xxHash of a string. Accepts a String type parameter. Returns UInt64 or UInt32. For more details, refer to [xxHash](https://xxhash.com/).
