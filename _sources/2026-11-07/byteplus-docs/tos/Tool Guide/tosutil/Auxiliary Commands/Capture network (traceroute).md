---
title: "Capture network (traceroute)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Scraping-the-network-traceroute"
---

You can trace the data network path using the `traceroute` command.

<span id="3ad9a74c"></span>
## Traceroute

<span id="24dcff2d"></span>
## Command syntax


<Tabs>
<Tab zoneid="WRFvjBxc" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

* Domain name


```Bash
./tosutil traceroute domain [-s=1] [-m=1] [-w=1] [-q] [-ipv6] [-n]
```



* IP address


```Bash
./tosutil traceroute ipaddress [-s=1][-m=1] [-w=1] [-q] [-ipv6] [-n]
```





</Tab>
<Tab zoneid="7eIWG26O" title="Windows">
<TabTitle>Windows</TabTitle>

* Establish a network connection to the domain name and measure the elapsed time


```Bash
tosutil traceroute domain [-s=1] [-m=1] [-w=1] [-q] [-ipv6] [-n]
```



* Establish a network connection to the IP address and measure the elapsed time


```Bash
tosutil traceroute ipaddress [-s=1][-m=1] [-w=1] [-q] [-ipv6] [-n]
```





</Tab>
</Tabs>


<span id="845c652e"></span>
## Parameters


|Parameter name |Type |Description |
|---|---|---|
|domain |String |Target host domain name. Supported TOS regions and access domains; see [Region and Endpoint](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint). |
|ipaddress |String |Target host IP address. |
|\-s=1 |String |Packet size in bytes when executing the `traceroute` command, default is 56B. Value range is [1B, 63KB]. |
|\-m=1 |String |Maximum number of probes when executing the `traceroute` command, default is 30. |
|\-w=1 |String |Timeout in seconds for each probe when executing the `traceroute` command, default is 5 seconds. |
|\-q |String |Number of packets sent per probe when executing the `traceroute` command, default is 3, maximum is 10. |
|\-ipv6 |String |Select IPv6 address when resolving domain name. |
|\-n |String |Do not resolve domain names when executing the traceroute command. |


<span id="43f221d8"></span>
## Usage example


* Command


```Plain
./tosutil traceroute tos-cn-beijing.ibytepluses.com.cn.com
```



* Return


```Plain
Warning: tos-cn-beijing.ibytepluses.com.cn has multiple ipv4 addresses; using 100.64.**.**
traceroute to 100.64.**.**, 30 hops max, 56 byte packets

1       100.64.**.** (100.64.**.**)   0 ms
```
