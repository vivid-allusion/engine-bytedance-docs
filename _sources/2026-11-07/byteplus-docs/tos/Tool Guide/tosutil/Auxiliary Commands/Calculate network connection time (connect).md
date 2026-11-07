---
title: "Calculate network connection time (connect)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Calculate-network-connection-time-connect"
---

You can use the `connect` command to establish a TCP connection to a domain name or IP address and measure the connection time.

<span id="417b7165"></span>
## Command syntax


<Tabs>
<Tab zoneid="iZJyFVEJ" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

* establish a network connection to the domain and measure the time taken


```Bash
./tosutil connect domain
```



* establish a network connection to the IP address and measure the time taken


```Bash
./tosutil connect ipaddress
```





</Tab>
<Tab zoneid="XI8R3yXc" title="Windows">
<TabTitle>Windows</TabTitle>

* to domain


```Bash
tosutil connect domain
```



* to IP address


```Bash
tosutil connect ipaddress
```





</Tab>
</Tabs>


<span id="9d0a8c67"></span>
## Parameters


|Parameter name |Type |Description |
|---|---|---|
|domain |String |target host domain name. regions and access domains supported by TOS. see [Region and Endpoint](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint). |
|ipaddress |String |target host IP address. |


<span id="56e7d2b6"></span>
## Usage example

<span id="6139c3ba"></span>
### Calculate network connection time to a domain name

The following command measures the connection time between the host and the Beijing region.


* Command


```Plain
./tosutil connect tos-cn-beijing.ibytepluses.com.cn
```



* Return


```Plain
Resolve dns cost:      2 ms
Build connection cost: 2 ms
Total cost:            4 ms

Resolved ip list:
1: 100.64.**.**
2: 100.64.**.**
3: 100.64.**.**
```


<span id="ca383e09"></span>
### Calculate network connection time to an IP address


* Command


```Plain
./tosutil connect 100.64.**.**
```



* return


```Plain
Resolve dns cost:      -1 ms
Build connection cost: 1 ms
Total cost:            1 ms
```
