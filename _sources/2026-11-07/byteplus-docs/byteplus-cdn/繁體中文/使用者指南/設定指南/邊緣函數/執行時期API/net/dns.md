---
title: "dns"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-NET-cn-zh-tw"
---

本文檔介紹 DNS 解析相關的運行時期 API。

<span id="resolvev4"></span>
## resolveV4

將網域名稱解析為 A 記錄。此方法回傳一個物件，資料結構如下：

```json
{
  "ttl": <Number>,
  "address": [
    <String>
  ]
}
```


<span id="範例"></span>
### 範例

```javascript
const data = await net.dns.resolveV4("www.example.com");
console.log("%s", JSON.stringify(data));
```


console.log 會輸出一個 JSON 字串，例如：

```json
{"ttl":122,"address":["203.0.113.1","203.0.113.2"]}
```


<span id="resolvev6"></span>
## resolveV6

將網域名稱解析為 AAAA 記錄。此方法回傳一個物件，資料結構如下：

```json
{
  "ttl": <Number>,
  "address": [
    <String>
  ]
}
```


<span id="範例"></span>
### 範例

```javascript
const data = await net.dns.resolveV6("www.example.com");
console.log("%s", JSON.stringify(data));
```


console.log 會輸出一個 JSON 字串，例如：

```json
{"ttl":87,"address":["2001:db8::abcd:0012","2001:db8::abcd:0014"]}
```


<span id="resolvemx"></span>
## resolveMx

將網域名稱解析為 MX 記錄。此方法回傳一個物件，資料結構如下：

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


<span id="範例"></span>
### 範例

```javascript
const data = await net.dns.resolveMx("www.example.com");
console.log("%s", JSON.stringify(data));
```


console.log 會輸出一個 JSON 字串，例如：

```json
{"ttl":300,"name":"example.com","cname":"example.com","mx":[{"name":"smtp.example.com","priority":10}]}
```


<span id="resolvesrv"></span>
## resolveSrv

將網域名稱解析為 SRV 記錄。此方法回傳一個物件，資料結構如下：

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


<span id="範例"></span>
### 範例

```javascript
const data = await net.dns.resolveSrv("example.com", "imaps","tcp");
console.log("%s", JSON.stringify(data));
```


console.log 會輸出一個 JSON 字串，例如：

```json
{"ttl":86400,"name":"_imaps._tcp.example.com","cname":"_imaps._tcp.example.com","srv":[{"hostname":"imap.example.com","priority":5,"weight":0,"port":993}]}
```


<span id="resolvetxt"></span>
## resolveTxt

將網域名稱解析為 TXT 記錄。此方法回傳一個物件，資料結構如下：

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


<div data-tips="true" data-tips-type="tip">"txt" 陣列成員格式為 <a href="https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer">ArrayBuffer</a>。如需列印內容，需先使用 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Web-standards-cn-zh-tw">TextDecoder</a> 解碼。</div>


<span id="範例"></span>
### 範例

```javascript
const data = await net.dns.resolveTxt("byteplus.com");
console.log(data);
```


console.log 會輸出以下內容：

```javascript
Object {ttl: 922, name: "byteplus.com", cname: "byteplus.com", txt: Array(9)}
```


<span id="resolvenaptr"></span>
## resolveNaptr

將網域名稱解析為 NAPTR 記錄。此方法回傳一個物件，資料結構如下：

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


<span id="範例"></span>
### 範例

```javascript
const data = await net.dns.resolveNaptr("example.com");
console.log(JSON.stringify(data));
```


console.log 會輸出一個 JSON 字串，例如：

```json
{"ttl":565,"name":"example.com","cname":"example.com","srv":[{"services":"RELAY:turn.udp","flags":"s","regex":"","replacement":"_turn._udp.example.com","order":10,"preference":0},{"services":"RELAY:turn.tls","flags":"s","regex":"","replacement":"_turns._tcp.example.com","order":10,"preference":0},{"services":"SIPS+D2T","flags":"s","regex":"","replacement":"_sips._tcp.example.com","order":10,"preference":0}]}
```


<span id="resolveptr"></span>
## resolvePtr

將 IP 位址反向解析為 PTR 記錄。此方法回傳一個物件，資料結構如下：

```json
{
  "ttl": <Number>,
  "name": <String>,
  "cname": <String>,
  "domainName": [
    <String>
  ]
}
```


<span id="範例"></span>
### 範例

```javascript
const data = await net.dns.resolvePtr("xxx.xxx.xxx.xxx");
console.log(JSON.stringify(data));
```


console.log 會輸出一個 JSON 字串，例如：

```json
{"ttl":86399,"name":"xxx.xxx.xxx.xxx.in-addr.arpa","cname":"xxx.xxx.xxx.xxx.in-addr.arpa","domainName":["example.com"]}
```
