---
title: "dns"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-DNS-cn"
---

本文档介绍 DNS 解析相关的运行时 API。

<span id="resolvev4"></span>
## resolveV4

将域名解析为 A 记录。该方法返回一个对象，数据结构如下：

```json
{
  "ttl": <Number>,
  "address": [
    <String>
  ]
}
```


<span id="示例"></span>
### 示例

```javascript
const data = await net.dns.resolveV4("www.example.com");
console.log("%s", JSON.stringify(data));
```


console.log 会输出一个 JSON 字符串，例如：

```json
{"ttl":122,"address":["203.0.113.1","203.0.113.2"]}
```


<span id="resolvev6"></span>
## resolveV6

将域名解析为 AAAA 记录。该方法返回一个对象，数据结构如下：

```json
{
  "ttl": <Number>,
  "address": [
    <String>
  ]
}
```


<span id="示例"></span>
### 示例

```javascript
const data = await net.dns.resolveV6("www.example.com");
console.log("%s", JSON.stringify(data));
```


console.log 会输出一个 JSON 字符串，例如：

```json
{"ttl":87,"address":["2001:db8::abcd:0012","2001:db8::abcd:0014"]}
```


<span id="resolvemx"></span>
## resolveMx

将域名解析为 MX 记录。该方法返回一个对象，该对象的数据结构如下：

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


<span id="示例"></span>
### 示例

```javascript
const data = await net.dns.resolveMx("www.example.com");
console.log("%s", JSON.stringify(data));
```


console.log 会输出一个 JSON 字符串，例如：

```json
{"ttl":300,"name":"example.com","cname":"example.com","mx":[{"name":"smtp.example.com","priority":10}]}
```


<span id="resolvesrv"></span>
## resolveSrv

将域名解析为 SRV 记录。该方法返回一个对象，该对象的数据结构如下：

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


<span id="示例"></span>
### 示例

```javascript
const data = await net.dns.resolveSrv("example.com", "imaps","tcp");
console.log("%s", JSON.stringify(data));
```


console.log 会输出一个 JSON 字符串，例如：

```json
{"ttl":86400,"name":"_imaps._tcp.example.com","cname":"_imaps._tcp.example.com","srv":[{"hostname":"imap.example.com","priority":5,"weight":0,"port":993}]}
```


<span id="resolvetxt"></span>
## resolveTxt

将域名解析为 TXT 记录。该方法返回一个对象，该对象的数据结构如下：

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


<div data-tips="true" data-tips-type="tip">"txt" 数组的成员格式是 <a href="https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer">ArrayBuffer</a>。如果您需要打印 "txt" 数组的内容，您需要首先使用 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Web-standards-cn">TextDecoder</a> 进行解码。</div>


<span id="示例"></span>
### 示例

```javascript
const data = await net.dns.resolveTxt("byteplus.com");
console.log(data);
```


console.log 会输出以下内容：

```javascript
Object {ttl: 922, name: "byteplus.com", cname: "byteplus.com", txt: Array(9)}
```


<span id="resolvenaptr"></span>
## resolveNaptr

将域名解析为 NAPTR 记录。该方法返回一个对象，该对象的数据结构如下：

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


<span id="示例"></span>
### 示例

```javascript
const data = await net.dns.resolveNaptr("example.com");
console.log(JSON.stringify(data));
```


console.log 会输出一个 JSON 字符串，例如：

```json
{"ttl":565,"name":"example.com","cname":"example.com","srv":[{"services":"RELAY:turn.udp","flags":"s","regex":"","replacement":"_turn._udp.example.com","order":10,"preference":0},{"services":"RELAY:turn.tls","flags":"s","regex":"","replacement":"_turns._tcp.example.com","order":10,"preference":0},{"services":"SIPS+D2T","flags":"s","regex":"","replacement":"_sips._tcp.example.com","order":10,"preference":0}]}
```


<span id="resolveptr"></span>
## resolvePtr

将 IP 地址反向解析为 PTR 记录。该方法返回一个对象，该对象的数据结构如下：

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


<span id="示例"></span>
### 示例

```javascript
const data = await net.dns.resolvePtr("xxx.xxx.xxx.xxx");
console.log(JSON.stringify(data));
```


console.log 会输出一个 JSON 字符串，例如：

```json
{"ttl":86399,"name":"xxx.xxx.xxx.xxx.in-addr.arpa","cname":"xxx.xxx.xxx.xxx.in-addr.arpa","domainName":["example.com"]}

```
