---
title: "Measure network latency (ping)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Measuring-network-latency-ping"
---

You can use the ping command to test host connectivity with TOS and measure network latency.

<span id="8cb2b5f9"></span>
## Command syntax


<Tabs>
<Tab zoneid="fKf6GhkH" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

* Test network connectivity with domain name


```Bash
./tosutil ping domain [-s=1] [-t=1] [-count=1] [-ipv6]
```



* Test network connectivity with IP address


```Bash
./tosutil ping ipaddress [-s=1] [-t=1] [-count=1] [-ipv6]
```





</Tab>
<Tab zoneid="ZZN0MAeh" title="Windows">
<TabTitle>Windows</TabTitle>

* for domain


```Bash
tosutil ping domain [-s=1] [-t=1] [-count=1] [-ipv6]
```



* for IP address


```Bash
tosutil ping ipaddress [-s=1] [-t=1] [-count=1] [-ipv6]
```





</Tab>
</Tabs>


<span id="af4ed998"></span>
## Parameters


|parameter name |Type |Description |
|---|---|---|
|domain |String |target host domain name. Supported regions and access domains of TOS, see [Region and Endpoint](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint). |
|ipaddress |String |target host IP address. |
|\-s |String |packet size for the ping command, in bytes, default is 56B. value range is [1B, 63KB]. |
|\-t |String |maximum execution time for the ping command, in seconds. |
|\-count |String |Count of send or receive rounds during ping execution. |
|\-ipv6 |String |Select IPv6 address when resolving domain name. |


<span id="aaeefd88"></span>
## Example usage

<span id="59f4ca31"></span>
### Test connectivity with domain names

The following command tests host connectivity with the Beijing region, with 5 rounds of testing.


* Command


```Plain
./tosutil ping tos-cn-beijing.ibytepluses.com.cn -count=5
```



* Response


```Plain
PING tos-cn-beijing.ibytepluses.com.cn (100.64.153.11): 56 data bytes
64 bytes from 100.64.**.**: icmp_seq=0 time=0 ms
64 bytes from 100.64.**.**: icmp_seq=1 time=0 ms
64 bytes from 100.64.**.**: icmp_seq=2 time=0 ms
64 bytes from 100.64.**.**: icmp_seq=3 time=0 ms
64 bytes from 100.64.**.**: icmp_seq=4 time=0 ms

--- tos-cn-beijing.ibytepluses.com.cn ping statistics ---
5 packets transmitted, 5 packets received, 0% packet loss
round-trip min/avg/max/stddev = 0/0/0/0 ms
```


<span id="c13312a0"></span>
### Test connectivity with IP addresses

The following command tests network connectivity between the host and **100.64.** .\*\*\*\* with a packet size of **100b**.


* Command


```Plain
./tosutil ping 100.64.**.** -s=100 -count=5
```



* Response


```Plain
PING 100.64.**.** (100.64.**.**): 100 data bytes
108 bytes from 100.64.**.**: icmp_seq=0 time=0 ms
108 bytes from 100.64.**.**: icmp_seq=1 time=0 ms
108 bytes from 100.64.**.**: icmp_seq=2 time=0 ms
108 bytes from 100.64.**.**: icmp_seq=3 time=0 ms
108 bytes from 100.64.**.**: icmp_seq=4 time=0 ms

--- 100.64.**.** ping statistics ---
5 packets transmitted, 5 packets received, 0% packet loss
round-trip min/avg/max/stddev = 0/0/0/0 ms
```
