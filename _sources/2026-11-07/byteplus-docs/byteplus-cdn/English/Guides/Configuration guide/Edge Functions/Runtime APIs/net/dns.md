---
title: "dns"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-DNS"
---

This document describes the runtime API related to DNS resolution.

<span id="resolvev4"></span>
## resolveV4

Resolve the domain name to an A record. This method returns an object with the following data structure:

```json
{
  "ttl": <Number>,
  "address": [
    <String>
  ]
}
```


<span id="example"></span>
### Example

```javascript
const data = await net.dns.resolveV4("www.example.com");
console.log("%s", JSON.stringify(data));
```


console.log will output a JSON string, for example:

```json
{"ttl":122,"address":["203.0.113.1","203.0.113.2"]}
```


<span id="resolvev6"></span>
## resolveV6

Resolve the domain name to an AAAA record. This method returns an object with the following data structure:

```json
{
  "ttl": <Number>,
  "address": [
    <String>
  ]
}
```


<span id="example"></span>
### Example

```javascript
const data = await net.dns.resolveV6("www.example.com");
console.log("%s", JSON.stringify(data));
```


console.log will output a JSON string, for example:

```json
{"ttl":87,"address":["2001:db8::abcd:0012","2001:db8::abcd:0014"]}
```


<span id="resolvemx"></span>
## resolveMx

Resolve the domain name to an MX record. This method returns an object with the following data structure:

```json
{
  "ttl": <Number>,
  "name": <String>,
  "cname": <String>,
  "mx": [
    {
      "name": <String>,
      "priority": <Number>
    }
  ]
}
```


<span id="example"></span>
### Example

```javascript
const data = await net.dns.resolveMx("www.example.com");
console.log("%s", JSON.stringify(data));
```


console.log will output a JSON string, for example:

```json
{"ttl":300,"name":"example.com","cname":"example.com","mx":[{"name":"smtp.example.com","priority":10}]}
```


<span id="resolvesrv"></span>
## resolveSrv

Resolve the domain name into an SRV record. This method returns an object with the following data structure:

```json
{
  "ttl": <Number>,
  "name": <String>,
  "cname": <String>,
  "srv": [
    {
      "hostname": <String>,
      "priority": <Number>,
      "weight": <Number>,
      "port": <Number>
    }
  ]
}
```


<span id="example"></span>
### Example

```javascript
const data = await net.dns.resolveSrv("example.com", "imaps","tcp");
console.log("%s", JSON.stringify(data));
```


console.log will output a JSON string, for example:

```json
{"ttl":86400,"name":"_imaps._tcp.example.com","cname":"_imaps._tcp.example.com","srv":[{"hostname":"imap.example.com","priority":5,"weight":0,"port":993}]}
```


<span id="resolvetxt"></span>
## resolveTxt

Resolve the domain name into a TXT record. This method returns an object with the following data structure:

```json
{
  "ttl": <Number>,
  "name": <String>,
  "cname": <String>,
  "txt": [
    <ArrayBuffer>
  ]
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The member format of the "txt" array is <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer">ArrayBuffer</a>. If you need to print the contents of the "txt" array, you need to decode it first using <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Web-standards">TextDecoder</a>.</div>


<span id="example"></span>
### Example

```javascript
const data = await net.dns.resolveTxt("byteplus.com");
console.log(data);
```


The console.log will output the following:

```javascript
Object {ttl: 922, name: "byteplus.com", cname: "byteplus.com", txt: Array(9)}
```


<span id="resolvenaptr"></span>
## resolveNaptr

Resolve the domain name into a NAPTR record. This method returns an object with the following data structure:

```json
{
  "ttl": <Number>,
  "name": <String>,
  "cname": <String>,
  "srv": [
    {
      "services": <String>,
      "flags": <String>,
      "regex": <String>,
      "replacement": <String>,
      "order": <Number>,
      "preference": <Number>
    }
  ]
}
```


<span id="example"></span>
### Example

```javascript
const data = await net.dns.resolveNaptr("example.com");
console.log(JSON.stringify(data));
```


console.log will output a JSON string, for example:

```json
{"ttl":565,"name":"example.com","cname":"example.com","srv":[{"services":"RELAY:turn.udp","flags":"s","regex":"","replacement":"_turn._udp.example.com","order":10,"preference":0},{"services":"RELAY:turn.tls","flags":"s","regex":"","replacement":"_turns._tcp.example.com","order":10,"preference":0},{"services":"SIPS+D2T","flags":"s","regex":"","replacement":"_sips._tcp.example.com","order":10,"preference":0}]}
```


<span id="resolveptr"></span>
## resolvePtr

Reverse resolve the IP address to a PTR record. This method returns an object with the following data structure:

```Plain Text
{
  "ttl": <Number>,
  "name": <String>,
  "cname": <String>,
  "domainName": [
    <String>
  ]
}
```


<span id="example"></span>
### Example

```javascript
const data = await net.dns.resolvePtr("xxx.xxx.xxx.xxx");
console.log(JSON.stringify(data));
```


console.log will output a JSON string, for example:

```json
{"ttl":86399,"name":"xxx.xxx.xxx.xxx.in-addr.arpa","cname":"xxx.xxx.xxx.xxx.in-addr.arpa","domainName":["example.com"]}

```
