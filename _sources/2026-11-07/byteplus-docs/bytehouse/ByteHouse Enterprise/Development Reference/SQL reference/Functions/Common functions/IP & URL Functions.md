---
title: "IP & URL Functions"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/ip-and-url-functions"
---

<span id="ipv4numtostring-num"></span>
## IPv4NumToString(num)
Accept a UInt32 (big-endian) representing the IPv4 address and return the corresponding IPv4 string representation in the format A.B.C.D (dot-separated decimal numbers).
<span id="ipv4stringtonum-s"></span>
## IPv4StringToNum(s)
Contrary to the IPv4NumToString function. If the IPv4 address format is invalid, then return 0.
<span id="ipv4numtostringclassc-num"></span>
## IPv4NumToStringClassC(num)
Similar to IPv4NumToString, but uses xxx to replace the last byte.
Example:
```SQL
SELECT IPv4NumToStringClassC(ClientIP) AS k, count() AS c FROM test.hits GROUP BY k ORDER BY c DESC LIMIT 10;
```

```SQL
┌─k──────────────┬─────c─┐
│ 83.149.9.xxx   │ 26238 │
│ 217.118.81.xxx │ 26074 │
│ 213.87.129.xxx │ 25481 │
│ 83.149.8.xxx   │ 24984 │
│ 217.118.83.xxx │ 22797 │
│ 78.25.120.xxx  │ 22354 │
│ 213.87.131.xxx │ 21285 │
│ 78.25.121.xxx  │ 20887 │
│ 188.162.65.xxx │ 19694 │
│ 83.149.48.xxx  │ 17406 │
└────────────────┴───────┘
```

Since using 'xxx' is non-standard, it may change in the future. We advise you not to rely on this format.
<span id="ipv6numtostring-x"></span>
### IPv6NumToString(x)
Accepts a binary format IPv6 address of type FixedString(16). Returns the string of this address in text format. IPv4 addresses mapped to IPv6 are displayed as ::ffff:111.222.33. For example:
```SQL
SELECT IPv6NumToString(toFixedString(unhex('2A0206B8000000000000000000000011'), 16)) AS addr
```

```SQL
┌─addr─────────┐
│ 2a02:6b8::11 │
└──────────────┘
```

```SQL
SELECT IPv6NumToString(ClientIP6 AS k), count() AS c FROM hits_all WHERE EventDate = today() AND substring(ClientIP6, 1, 12) != unhex('00000000000000000000FFFF') GROUP BY k ORDER BY c DESC LIMIT 10;
```

```SQL
┌─IPv6NumToString(ClientIP6)──────────────┬─────c─┐
│ 2a02:2168:aaa:bbbb::2                   │ 24695 │
│ 2a02:2698:abcd:abcd:abcd:abcd:8888:5555 │ 22408 │
│ 2a02:6b8:0:fff::ff                      │ 16389 │
│ 2a01:4f8:111:6666::2                    │ 16016 │
│ 2a02:2168:888:222::1                    │ 15896 │
│ 2a01:7e00::ffff:ffff:ffff:222           │ 14774 │
│ 2a02:8109:eee:ee:eeee:eeee:eeee:eeee    │ 14443 │
│ 2a02:810b:8888:888:8888:8888:8888:8888  │ 14345 │
│ 2a02:6b8:0:444:4444:4444:4444:4444      │ 14279 │
│ 2a01:7e00::ffff:ffff:ffff:ffff          │ 13880 │
└─────────────────────────────────────────┴───────┘
```

```SQL
SELECT IPv6NumToString(ClientIP6 AS k), count() AS c FROM hits_all WHERE EventDate = today() GROUP BY k ORDER BY c DESC LIMIT 10;
```

```SQL
┌─IPv6NumToString(ClientIP6)─┬──────c─┐
│ ::ffff:94.26.111.111       │ 747440 │
│ ::ffff:37.143.222.4        │ 529483 │
│ ::ffff:5.166.111.99        │ 317707 │
│ ::ffff:46.38.11.77         │ 263086 │
│ ::ffff:79.105.111.111      │ 186611 │
│ ::ffff:93.92.111.88        │ 176773 │
│ ::ffff:84.53.111.33        │ 158709 │
│ ::ffff:217.118.11.22       │ 154004 │
│ ::ffff:217.118.11.33       │ 148449 │
│ ::ffff:217.118.11.44       │ 148243 │
└────────────────────────────┴────────┘
```

<span id="ipv6stringtonum-s"></span>
## IPv6StringToNum(s)
Opposite to IPv6NumToString. If the IPv6 address format is invalid, then return an empty byte string. Hexadecimal can be uppercase or lowercase.
<span id="ipv4toipv6-x"></span>
## IPv4ToIPv6(x)
Accepts a UInt32 type IPv4 address and returns a FixedString(16) type IPv6 address. For example:
```SQL
SELECT IPv6NumToString(IPv4ToIPv6(IPv4StringToNum('192.168.0.1'))) AS addr
```

```plaintext
┌─addr───────────────┐
│ ::ffff:192.168.0.1 │
└────────────────────┘
```

<span id="cutipv6-x-bitstocutforipv6-bitstocutforipv4"></span>
## cutIPv6(x,bitsToCutForIPv6,bitsToCutForIPv4)
Accepts a FixedString(16) type IPv6 address, returns a string that contains the text format of the address after specified bits are deleted. For example:
```SQL
WITH IPv6StringToNum('2001:0DB8:AC10:FE01:FEED:BABE:CAFE:F00D') AS ipv6, IPv4ToIPv6(IPv4StringToNum('192.168.0.1')) AS ipv4 SELECT cutIPv6(ipv6, 2, 0), cutIPv6(ipv4, 0, 2)
```

```plaintext
┌─cutIPv6(ipv6, 2, 0)─────────────────┬─cutIPv6(ipv4, 0, 2)─┐
│ 2001:db8:ac10:fe01:feed:babe:cafe:0 │ ::ffff:192.168.0.0  │
└─────────────────────────────────────┴─────────────────────┘
```

<span id="ipv4cidrtorange"></span>
## IPv4CIDRToRange
Accepts an IPv4 address and a UInt8 Type CIDR. Returns a tuple that contains the subnet's lowest and highest range.
```SQL
SELECT IPv4CIDRToRange(toIPv4('192.168.5.2'), 16)
```

```plaintext
┌─IPv4CIDRToRange(toIPv4('192.168.5.2'), 16)─┐
│ ('192.168.0.0','192.168.255.255')          │
└────────────────────────────────────────────┘
```

<span id="ipv6cidrtorange"></span>
## IPv6CIDRToRange
Accepts an IPv6 address and a UInt8 Type CIDR. Returns a tuple that contains the subnet's lowest and highest range.
```SQL
SELECT IPv6CIDRToRange(toIPv6('2001:0db8:0000:85a3:0000:0000:ac1f:8001'), 32);
```

```plaintext
┌─IPv6CIDRToRange(toIPv6('2001:0db8:0000:85a3:0000:0000:ac1f:8001'), 32)─┐
│ ('2001:db8::','2001:db8:ffff:ffff:ffff:ffff:ffff:ffff')                │
└────────────────────────────────────────────────────────────────────────┘
```

<span id="toipv4-字符串"></span>
## toIPv4(String)
`IPv4StringToNum()` is an alias that uses a string form of an IPv4 address and returns a value of [IPv4](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/zh/sql-reference/functions/ip-address-functions.md) Type, this binary value is equal to the value returned by `IPv4StringToNum()`.
```SQL
WITH '171.225.130.45' as IPv4_string SELECT toTypeName(IPv4StringToNum(IPv4_string)), toTypeName(toIPv4(IPv4_string))
```

```plaintext
┌─toTypeName(IPv4StringToNum(IPv4_string))─┬─toTypeName(toIPv4(IPv4_string))─┐
│ UInt32                                   │ IPv4                            │
└──────────────────────────────────────────┴─────────────────────────────────┘
```

```SQL
WITH '171.225.130.45' as IPv4_string SELECT hex(IPv4StringToNum(IPv4_string)), hex(toIPv4(IPv4_string))
```

```plaintext
┌─hex(IPv4StringToNum(IPv4_string))─┬─hex(toIPv4(IPv4_string))─┐
│ ABE1822D                          │ ABE1822D                 │
└───────────────────────────────────┴──────────────────────────┘
```

<span id="toipv6-字符串"></span>
## toIPv6(String)
`IPv6StringToNum()` is an alias that uses a string form of an IPv6 address and returns a value of IPv6 Type, this binary value is equal to the value returned by `IPv6StringToNum()`.
```SQL
WITH '2001:438:ffff::407d:1bc1' as IPv6_string SELECT toTypeName(IPv6StringToNum(IPv6_string)), toTypeName(toIPv6(IPv6_string))
```

```plaintext
┌─toTypeName(IPv6StringToNum(IPv6_string))─┬─toTypeName(toIPv6(IPv6_string))─┐
│ FixedString(16)                          │ IPv6                            │
└──────────────────────────────────────────┴─────────────────────────────────┘
```

```SQL
WITH '2001:438:ffff::407d:1bc1' as IPv6_string SELECT hex(IPv6StringToNum(IPv6_string)), hex(toIPv6(IPv6_string))
```

```plaintext
┌─hex(IPv6StringToNum(IPv6_string))─┬─hex(toIPv6(IPv6_string))─────────┐
│ 20010438FFFF000000000000407D1BC1  │ 20010438FFFF000000000000407D1BC1 │
└───────────────────────────────────┴──────────────────────────────────┘
```
