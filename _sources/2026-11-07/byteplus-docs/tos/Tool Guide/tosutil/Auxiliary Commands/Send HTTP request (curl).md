---
title: "Send HTTP request (curl)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Send-http-request-curl"
---

You can send HTTP requests and receive responses using the `curl` command.

<span id="b048c772"></span>
## Curl

<span id="18946e32"></span>
## Command syntax


<Tabs>
<Tab zoneid="WFWIzRuG" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

&nbsp;

```Bash
./tosutil curl http(s)_url [-m=xxx] [-v] [-rb=xxx] [-fb=xxx] [-h=aaa:bbb#ccc:ddd] [-at=xxx] [-i=xxx] [-k=xxx] [-t=xxx]
```





</Tab>
<Tab zoneid="CXIswhw8" title="Windows">
<TabTitle>Windows</TabTitle>

&nbsp;

```Bash
tosutil curl http(s)_url [-m=xxx] [-v] [-rb=xxx] [-fb=xxx] [-h=aaa:bbb#ccc:ddd] [-at=xxx] [-i=xxx] [-k=xxx] [-t=xxx]
```





</Tab>
</Tabs>


<span id="6d1adc3d"></span>
## Parameters


|Parameter name |Type |Description |
|---|---|---|
|http(s)_url |String |The target URL for sending the HTTP request. |
|\-m |String |Request method name when executing curl command. Valid values:<br><br><br>* `GET`<br><br>* `PUT`<br><br>* `POST`<br><br>* `DELETE`<br><br>* `HEAD`<br><br><br>Default is `GET`. |
|\-v |String |Print detailed request and response information when executing the `curl` command. |
|\-rb |String |Request body when executing the `curl` command, valid only for `PUT`, `POST`, or `DELETE` methods. |
|\-fb |String |Use a local file as the request body and specify the local file path when executing the `curl` command, valid only for `PUT`, `POST`, or `DELETE` methods. |
|\-h=aaa:bbb#ccc:ddd |String |Request header fields when executing the `curl` command. |
|\-at |String |Include the signature and specify the signature algorithm when executing the `curl` command. Valid values:<br><br><br>* `tos` |
|\-i |String |The signature algorithm's **Access Key ID.**  |
|\-k |String |**Secret Access Key** for the signature algorithm. |
|\-t |String |STS token for the signature algorithm.  |


<span id="c2e42363"></span>
## Example


* command


```Plain
./tosutil curl https://console.byteplus.com/home
```



* response


```Plain
* Status code: 302, Response Body:

* The response is truncated, total length: 93, consumed length: 93
Redirecting to <a href="/auth/login?redirectURI=%2Fhome">/auth/login?redirectURI=%2Fhome</a>.
```
