---
title: "IP & URL functions"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-ip-address"
---

<span id="3b9cabc0"></span>
### IPv4NumToString

Accepts a UInt32 number. Interprets it as a big\-endian format IPv4 address. Returns a string containing the corresponding IPv4 address in ABCd format (dot\-separated decimal numbers).

**Syntax**

```SQL
IPv4NumToString(num)
```


**Parameters**


* `num` \- A UInt32 number.


**Return Values**


* A string represented as ipv4.


**Example**

```SQL
SELECT toIPv4('116.106.34.242') as ipv4, toTypeName(ipv4), IPv4NumToString(ipv4) as ipv4_string, toTypeName(ipv4_string)
```


```Plain
┌─ipv4───────────┬─toTypeName(toIPv4('116.106.34.242'))─┬─ipv4_string────┬─toTypeName(IPv4NumToString(toIPv4('116.106.34.242')))─┐
│ 242.34.106.116 │ IPv4                                 │ 116.106.34.242 │ String                                                │
└────────────────┴──────────────────────────────────────┴────────────────┴───────────────────────────────────────────────────────┘
```


<span id="91fabc87"></span>
### IPv4NumToStringClassC

Similar to `IPv4NumToString`, but uses xxx instead of the last eight\-bit byte.

**Syntax**

```SQL
IPv4NumToStringClassC(num)
```


**Parameters**


* `num` – A UInt32 number.


**Return Value**


* A string represented in ipv4, but uses xxx instead of the last eight\-bit byte.


**Example**

```SQL
SELECT toIPv4('116.106.34.242') as ipv4, toTypeName(ipv4), IPv4NumToStringClassC(ipv4) as ipv4_string, toTypeName(ipv4_string)
```


```Plain
┌─ipv4───────────┬─toTypeName(toIPv4('116.106.34.242'))─┬─ipv4_string────┬─toTypeName(IPv4NumToStringClassC(toIPv4('116.106.34.242')))─┐
│ 242.34.106.116 │ IPv4                                 │ 116.106.34.xxx │ String                                                      │
└────────────────┴──────────────────────────────────────┴────────────────┴─────────────────────────────────────────────────────────────┘
```


<span id="a3f6ef6d"></span>
### IPv4StringToNum

The inverse function of IPv4NumToString. If the IPv4 address format is invalid, it returns 0.

**Syntax**

```SQL
IPv4StringToNum(s)
```


**Parameters**


* `s` – IPv4 represented as a string.


**Return Values**


* UInt32。


**Examples**

```SQL
SELECT IPv4StringToNum('116.106.34.242') as ipv4, toTypeName(ipv4), IPv4NumToString(ipv4) as ipv4_string, toTypeName(ipv4_string)
```


```Plain
┌─ipv4───────┬─toTypeName(IPv4StringToNum('116.106.34.242'))─┬─ipv4_string────┬─toTypeName(IPv4NumToString(IPv4StringToNum('116.106.34.242')))─┐
│ 1953112818 │ UInt32                                        │ 116.106.34.242 │ String                                                         │
└────────────┴───────────────────────────────────────────────┴────────────────┴────────────────────────────────────────────────────────────────┘
```


<span id="1793376c"></span>
### IPv4ToIPv6

Uses a UInt32 number. Interpret it as an [big endian](https://en.wikipedia.org/wiki/Endianness) IPv4 address. Return a `FixedString(16)` value containing the binary\-formatted IPv6 address.

**Syntax**

```SQL
IPv4ToIPv6(x)
```


**Parameters**


* `x` is a `UInt32` number


**Return Value**


* Binary\-formatted IPv6 address.FixedString(16)


**Examples**

```SQL
SELECT IPv4StringToNum('192.168.0.1') as ipv4, IPv6NumToString(IPv4ToIPv6(ipv4)) as ipv6_string
```


```Plain
┌─ipv4───────┬─ipv6_string────────┐
│ 3232235521 │ ::ffff:192.168.0.1 │
└────────────┴────────────────────┘
```


<span id="27c9353e"></span>
### IPv6NumToString

Accepts a FixedString(16) value containing the binary\-formatted IPv6 address. Return a string containing the text representation of this address.

IPv6\-mapped IPv4 addresses are output in the format `::ffff:111.222.33.44`.

**Syntax**

```SQL
IPv6NumToString(x)
```


**Parameters**


* `x` – FixedString(16) value contains the binary format of the IPv6 address


**Return value**


* String represented in IPv6.


**Examples**

```SQL
SELECT IPv6NumToString(toFixedString(unhex('2A0206B8000000000000000000000011'), 16)) AS addr;
```


```Plain
┌─addr─────────┐
│ 2a02:6b8::11 │
└──────────────┘
```


<span id="89dcef74"></span>
### IPv6StringToNum

The reverse function of `IPv6NumToString`. If the IPv6 address format is invalid, an empty byte string is returned.

If the input string contains a valid IPv4 address, its IPv6 equivalent is returned. HEX can be uppercase or lowercase.

**Syntax**

```SQL
IPv6StringToNum(string)
```


**Argument**


* `String` — IP Address. String.


**Return Value**


* IPv6 address in binary format. Type: FixedString(16).


**Example**

```SQL
SELECT addr, cutIPv6(IPv6StringToNum(addr), 0, 0) FROM (SELECT ['notaddress', '127.0.0.1', '1111::ffff'] AS addr) ARRAY JOIN addr;
```


```Plain
┌─addr───────┬─cutIPv6(IPv6StringToNum(addr), 0, 0)─┐
│ notaddress │ ::                                   │
│ 127.0.0.1  │ ::                                   │
│ 1111::ffff │ 1111::ffff                           │
└────────────┴──────────────────────────────────────┘
```


<span id="0b8499a7"></span>
### cutIPv6

Accepts FixedString(16) values containing IPv6 addresses in binary format. Returns a string that contains the address with the specified number of bytes removed in text format.

**Syntax**

```SQL
cutIPv6(x, bytesToCutForIPv6, bytesToCutForIPv4)
```


**Parameters**


* `x` – FixedString(16) value containing the IPv6 address in binary format

* `bytesToCutForIPv6` represents the number of bytes to cut for IPv6

* `bytesToCutForIPv4` represents the number of bytes to cut for IPv4


**Return value**

A hash value of the `Uint64` data type.

Type: `UInt64`

**Example**

```SQL
WITH
    IPv6StringToNum('2001:0DB8:AC10:FE01:FEED:BABE:CAFE:F00D') AS ipv6,
    IPv4ToIPv6(IPv4StringToNum('192.168.0.1')) AS ipv4
SELECT
    cutIPv6(ipv6, 2, 0),
    cutIPv6(ipv4, 0, 2)
```


```Plain
┌─cutIPv6(ipv6, 2, 0)─────────────────┬─cutIPv6(ipv4, 0, 2)─┐
│ 2001:db8:ac10:fe01:feed:babe:cafe:0 │ ::ffff:192.168.0.0  │
└─────────────────────────────────────┴─────────────────────┘
```


<span id="50f68426"></span>
### toIPv4

The alias `IPv4StringToNum()` takes a string form of an IPv4 address and returns a binary value of type IPv4, which is equivalent to the value returned by `IPv4StringToNum()`.

**Syntax**

```SQL
toIPv4(string)
```


**Arguments**


* `string`— IP address. String.


**Return value**


* IPv4 Type


**Example**

```SQL
WITH'171.225.130.45' as IPv4_string
SELECT
    toTypeName(IPv4StringToNum(IPv4_string)),
    toTypeName(toIPv4(IPv4_string))
```


```Plain
┌─toTypeName(IPv4StringToNum(IPv4_string))─┬─toTypeName(toIPv4(IPv4_string))─┐
│ UInt32                                   │ IPv4                            │
└──────────────────────────────────────────┴─────────────────────────────────┘
```


```SQL
WITH'171.225.130.45' as IPv4_string
SELECT
    hex(IPv4StringToNum(IPv4_string)),
    hex(toIPv4(IPv4_string))
```


```Plain
┌─hex(IPv4StringToNum(IPv4_string))─┬─hex(toIPv4(IPv4_string))─┐
│ ABE1822D                          │ ABE1822D                 │
└───────────────────────────────────┴──────────────────────────┘
```


<span id="785b7548"></span>
### toIPv6

Convert a string\-formatted IPv6 address into IPv6 type. If the IPv6 address format is invalid, return null.

Similar to the IPv6StringToNum function, converts an IPv6 address into binary format.

**Syntax**

```SQL
toIPv6(string)
```


**Argument**


* `string`— IP address. String


**Return Value**


* IP Address. Type: IPv6.


**Example**

```SQL
WITH '2001:438:ffff::407d:1bc1' AS IPv6_string
SELECT
    hex(IPv6StringToNum(IPv6_string)),
    hex(toIPv6(IPv6_string));
```


```Plain
┌─hex(IPv6StringToNum(IPv6_string))─┬─hex(toIPv6(IPv6_string))─────────┐
│ 20010438FFFF000000000000407D1BC1  │ 20010438FFFF000000000000407D1BC1 │
└───────────────────────────────────┴──────────────────────────────────┘
```


<span id="ca1043cf"></span>
### URLHierarchy

Returns an array containing the URL, truncated at the end of the path and query string by symbols /,? Truncated. Consecutive separators are counted as one. Truncation occurs after all consecutive separators.

**Syntax**

```SQL
URLHierarchy(URL)
```


**Parameter**


* `URL`— URL

* Type: String.


**Return Value**


* Array containing URLs


**Example**

```SQL
SELECT URLHierarchy('https://example.com/browse/CONV-6788');
```


```Plain
┌─URLHierarchy('https://example.com/browse/CONV-6788')────────────────────────────────────────────┐
│ ['https://example.com/', 'https://example.com/browse/', 'https://example.com/browse/CONV-6788'] │
└─────────────────────────────────────────────────────────────────────────────────────────────────┘
```


<span id="bdf04641"></span>
### URLPathHierarchy

Same as above, but the result does not include protocol and host. Does not contain / elements (root).

**Syntax**

```SQL
URLPathHierarchy(URL)
```


**Parameter**


* `URL`— URL

* Type: string.


**Return value**


* Array containing URLs


**Example**

```SQL
SELECT URLPathHierarchy('https://example.com/browse/CONV-6788');
```


```Plain
┌─URLPathHierarchy('https://example.com/browse/CONV-6788')─┐
│ ['/browse/', '/browse/CONV-6788']                        │
└──────────────────────────────────────────────────────────┘
```


<span id="1c154a1c"></span>
### cutFragment

Deletes the fragment identifier. Numerical symbols are also removed.

**Syntax**

```SQL
cutFragment(URL)
```


**Parameter**


* `URL` – URL string


**Return value**


* URL without fragment


**Example**

```SQL
SELECT cutFragment('http://example.com#fragment')
```


```Plain
┌─cutFragment('http://example.com#fragment')─┐
│ http://example.com                         │
└────────────────────────────────────────────┘
```


<span id="a9f2bec4"></span>
### cutQueryString

Remove the query string. The question mark is also removed.

**Syntax**

```SQL
cutQueryString(URL)
```


**Parameter**


* `URL` – URL string


**Return value**


* URL without query


**Example**

```SQL
SELECT cutQueryString('http://example.com/?page=1&lr=213')
```


```Plain
┌─cutQueryString('http://example.com/?page=1&lr=213')─┐
│ http://example.com/                                 │
└─────────────────────────────────────────────────────┘
```


<span id="2fcd3972"></span>
### cutQueryStringAndFragment

Remove the query string and fragment identifier. The question mark and number sign are also removed.

**Syntax**

```SQL
cutQueryStringAndFragment(URL)
```


**Parameters**


* `URL` – URL string


**Return value**


* URL string without query string and fragment


**Example**

```SQL
SELECT cutQueryStringAndFragment('http://example.com/?page=1&lr=213#fragment')
```


```Plain
┌─cutQueryStringAndFragment('http://example.com/?page=1&lr=213#fragment')─┐
│ http://example.com/                                                     │
└─────────────────────────────────────────────────────────────────────────┘
```


<span id="a96a786a"></span>
### cutToFirstSignificantSubdomain

Returns the domain part containing the top\-level subdomain up to the "first significant subdomain."

**Syntax**

```SQL
cutToFirstSignificantSubdomain(URL)
```


**Parameter**


* `URL` \- URL string


**Return value**


* Subdomain string


**Example**

```SQL
SELECT cutToFirstSignificantSubdomain('https://www.example.com.cn/')
```


```Plain
┌─cutToFirstSignificantSubdomain('https://www.example.com.cn/')─┐
│ example.com.cn                                                │
└───────────────────────────────────────────────────────────────┘
```


<span id="529c8201"></span>
### cutURLParameter

Remove the "name" URL parameter (if it exists). This function assumes that the encoding of parameter names in the URL is exactly the same as the encoding in the parameters passed.

**Syntax**

```SQL
cutURLParameter(URL, name)
```


**Parameters**


* `URL` – URL string

* `Name` parameter name


**Return Value**


* URL string


**Example**

```SQL
SELECT cutURLParameter('http://example.com/?page=1&lr=213','page')
```


```Plain
┌─cutURLParameter('http://example.com/?page=1&lr=213', 'page')─┐
│ http://example.com/?lr=213                                   │
└──────────────────────────────────────────────────────────────┘
```


<span id="d9554ba7"></span>
### cutWWW

If present, remove at most one "www." from the beginning of the URL domain

**Syntax**

```SQL
cutWWW(URL)
```


**Parameters**


* `URL` \- URL string

* `Name` parameter name


**Return value**


* URL string


**Example**

```SQL
SELECT cutWWW('http://www.example.com/?page=1&lr=213')
```


```Plain
┌─cutWWW('http://www.example.com/?page=1&lr=213')─┐
│ http://example.com/?page=1&lr=213               │
└─────────────────────────────────────────────────┘
```


<span id="502b03e8"></span>
### decodeURLComponent

Return the decoded URL.

**Syntax**

```SQL
decodeURLComponent(URL) 
```


**Parameters**


* `URL` – URL string


**Return Value**


* Decoded URL string


**Example**

```SQL
SELECT decodeURLComponent('http://127.0.0.1:8123/?query=SELECT%201%3B') AS DecodedURL;
```


```Plain
┌─DecodedURL─────────────────────────────┐
│ http://127.0.0.1:8123/?query=SELECT 1; │
└────────────────────────────────────────┘
```


<span id="2423eb2e"></span>
### domain

Extract the hostname from the URL.

**Grammar**

```SQL
domain(url)
```


**Parameters**


* `url`— URL。 Type: String. URL


May or may not specify a scheme. Example:

```Plain
svn+ssh://some.svn-hosting.com:80/repo/trunk
some.svn-hosting.com:80/repo/trunk
https://yandex.com/time/
```


For these examples, the `domain` function returns the following results:

```Plain
some.svn-hosting.com
some.svn-hosting.com
yandex.com
```


**Return Value**


* Hostname. If ByteHouse can parse the input string into a URL.

* Empty string. If ByteHouse cannot parse the input string into a URL.


Type: `String`.

**Example**

```SQL
SELECT domain('svn+ssh://some.svn-hosting.com:80/repo/trunk');
```


```Plain
┌─domain('svn+ssh://some.svn-hosting.com:80/repo/trunk')─┐
│ some.svn-hosting.com                                   │
└────────────────────────────────────────────────────────┘
```


<span id="b8e22349"></span>
### domainWithoutWWW

Return the domain name and remove at most one "www." from its beginning (if present).

**Syntax**

```SQL
domainWithoutWWW(url)
```


**Parameters**


* `url`— URL

* Type: string.


**Return value**


* Hostname. If ByteHouse can parse the input string as a URL.

* Empty string. If ByteHouse cannot parse the input string as a URL.


Type: `String`.

**Example**

```SQL
SELECT domainWithoutWWW('http://www.example.com#fragment');
```


```Plain
┌─domainWithoutWWW('http://www.example.com#fragment')─┐
│ example.com                                         │
└─────────────────────────────────────────────────────┘
```


<span id="bea7ee15"></span>
### extractURLParameter

Returns the value of the "name" parameter in the URL (if it exists). Otherwise, return an empty string. If there are multiple parameters with the same name, return the first one. The working principle of this function is assuming that the encoding of parameter names in the URL is exactly the same as in the passed parameters.

**Syntax**

```SQL
extractURLParameter(URL, name)
```


**Parameters**


* `URL` \- URL string

* `Name` \- Parameter name


**Return value**


* Parameter value


**Example**

```SQL
SELECT extractURLParameter('http://example.com/?page=1&lr=213','page')
```


```Plain
┌─extractURLParameter('http://example.com/?page=1&lr=213', 'page')─┐
│ 1                                                                │
└──────────────────────────────────────────────────────────────────┘
```


<span id="d8ffb20e"></span>
### extractURLParameterNames

Returns an array of names corresponding to URL parameter names. The values will not be decoded in any way.

**Syntax**

```SQL
extractURLParameterNames(URL)
```


**Parameters**


* `URL` – URL string


**Return Value**


* List of parameter names


**Example**

```SQL
SELECT extractURLParameterNames('http://example.com/?page=1&lr=213')
```


```Plain
┌─extractURLParameterNames('http://example.com/?page=1&lr=213')─┐
│ ['page', 'lr']                                                │
└───────────────────────────────────────────────────────────────┘
```


<span id="0cb19f6d"></span>
### extractURLParameters

Returns an array of name=value strings corresponding to URL parameters. These values are not decoded in any way.

**Syntax**

```SQL
extractURLParameters(URL)
```


**Parameters**


* `URL` – url string


**Return Values**


* Parameter List


**Examples**

```SQL
SELECT extractURLParameters('http://example.com/?page=1&lr=213')
```


```Plain
┌─extractURLParameters('http://example.com/?page=1&lr=213')─┐
│ ['page=1', 'lr=213']                                      │
└───────────────────────────────────────────────────────────┘
```


<span id="e682a020"></span>
### firstSignificantSubdomain

Returns "the first significant subdomain." This is a unique non\-standard concept specific to Yandex.Metrica. If the first significant subdomain is "com," "net," "org," or "co," then it is a second\-level domain. Otherwise, it is a third\-level domain.

**Syntax**

```SQL
firstSignificantSubdomain(URL)
```


**Parameters**


* `URL` \- URL string


**Return value**


* The first significant subdomain


**Example**

```SQL
SELECT firstSignificantSubdomain('https://www.example.com.cn/')
```


```Plain
┌─firstSignificantSubdomain('https://www.example.com.cn/')─┐
│ example                                                  │
└──────────────────────────────────────────────────────────┘
```


<span id="4e2493ec"></span>
### fragment

Return the fragment identifier. The fragment does not include the initial hash mark.

**Syntax**

```SQL
fragment(URL)
```


**Parameters**


* `URL` – URL string


**Return value**


* Fragment string


**Examples**

```SQL
SELECT fragment('http://example.com#fragment')
```


```Plain
┌─fragment('http://example.com#fragment')─┐
│ fragment                                │
└─────────────────────────────────────────┘
```


<span id="46231800"></span>
### path

Return the path. Example: The path `/top/news.html` does not contain a query string.

**Syntax**

```SQL
path(URL)
```


**Parameters**


* `URL` – URL string


**Return Value**


* Path String


**Example**

```SQL
SELECT path('http://example.com/top/news.html')
```


```Plain
┌─path('http://example.com/top/news.html')─┐
│ /top/news.html                           │
└──────────────────────────────────────────┘
```


<span id="bc444f1f"></span>
### protocol

Extract the protocol from the URL.

Typical return value examples: http, https, ftp, mailto, tel, magnet…

**Grammar**

```SQL
protocol(URL)
```


**Parameter**


* `URL` \- URL string


**Return value**


* Protocol string


**Example**

```SQL
SELECT protocol('http://example.com')
```


```Plain
┌─protocol('http://example.com')─┐
│ http                           │
└────────────────────────────────┘
```


<span id="15209fea"></span>
### queryString

Returns the query string. Example: page=1&lr=213. The query string does not include the initial question mark, #, and everything after #.

**Syntax**

```SQL
queryString(URL)
```


**Parameter**


* `URL` – URL string


**Return Value**


* Request Parameters


**Example**

```SQL
SELECT queryString('http://example.com/?page=1&lr=213')
```


```Plain
┌─queryString('http://example.com/?page=1&lr=213')─┐
│ page=1&lr=213                                    │
└──────────────────────────────────────────────────┘
```


<span id="e8e403ab"></span>
### queryStringAndFragment

Returns the query string and fragment identifier. Example: page=1#29390.

**Syntax**

```SQL
queryStringAndFragment(URL)
```


**Parameter**


* `URL` \- URL string


**Return Value**


* Query and Fragment Strings


**Example**

```SQL
SELECT queryStringAndFragment('http://example.com/?page=1&lr=213#fragment')
```


```Plain
┌─queryStringAndFragment('http://example.com/?page=1&lr=213#fragment')─┐
│ page=1&lr=213#fragment                                               │
└──────────────────────────────────────────────────────────────────────┘
```


<span id="ef41b50d"></span>
### topLevelDomain

Extract the top\-level domain from a URL.

**Syntax**

```SQL
topLevelDomain(url)
```


**Parameter**


* `url`— URL

* Type: String. URL


You can specify or not specify a scheme. Example:

```Plain
svn+ssh://some.svn-hosting.com:80/repo/trunk
some.svn-hosting.com:80/repo/trunk
https://yandex.com/time/
```


**Return value**


* Domain Name. If ByteHouse can analyze the input character string as a URL.

* Empty string. If ByteHouse cannot analyze the input character string as a URL.


Type: `String`.

**Example**

```SQL
SELECT topLevelDomain('svn+ssh://www.some.svn-hosting.com:80/repo/trunk');
```


```Plain
┌─topLevelDomain('svn+ssh://www.some.svn-hosting.com:80/repo/trunk')─┐
│ com                                                                │
└────────────────────────────────────────────────────────────────────┘
```
