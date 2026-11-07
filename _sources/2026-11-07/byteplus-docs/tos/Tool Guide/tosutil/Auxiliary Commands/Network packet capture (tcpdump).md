---
title: "Network packet capture (tcpdump)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Network-packet-capture-tcpdump"
---

You can capture and analyze network traffic using the `tcpdump` command.

<span id="eb84d610"></span>
## Note


* This command is for internal use only. Download the installation package from:

   * Linux

   * Windows

   * macOS

* You must install the `libpcap.so.0.8` dependency before running the command; otherwise, it will not work properly.


<span id="78a52746"></span>
## Command syntax


<Tabs>
<Tab zoneid="p9EqdgJ1" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

* Get all network interfaces


```Bash
./tosutil tcpdump [-sdt=xxx]
```



* Capture packets on the specified network interface


```Bash
./tosutil tcpdump device [-o=xxx] [-bpf=xxx] [-t=1]
```





</Tab>
<Tab zoneid="qa28Nl7n" title="Windows">
<TabTitle>Windows</TabTitle>

&nbsp;

```Bash
tosutil fcp file_url1 file_url2|folder_url2 [-dryRun] [-link] [-tempFileDir=xxx] [-useTempFile] [-u] [-vchecksum] [-dfo] [-fsync] [-rbs=1MB] [-wbs=1MB] [-rdio] [-rmmap] [-wdio] [-wmmap] [-ea=xxx] [-sdk=xxx] [-dek=xxx] [-fr] [-o=xxx]
```





</Tab>
</Tabs>


<span id="c6ac8bae"></span>
## Parameters


|Parameter name |Type |Description |
|---|---|---|
|device |String |Target network interface name. |
|\-sdt |String |Display the device list based on the specified device IP address type. Valid values:<br><br><br>* `all`<br><br>* `ip`<br><br>* `ipv4`<br><br>* `ipv6`<br><br><br>Defaults to `all`. |
|\-o |String |Local file path to store the results when running the `tcpdump` command. |
|\-bpf |String |BPF filter expression specified when executing the `tcpdump` command. |
|\-t |String |Maximum execution time of the `tcpdump` command, in seconds. |


<span id="70b689f2"></span>
## Usage example


* Command


```Plain
./tosutil tcpdump
```



* Return


```Plain
interface 1: eth0
 - ip: 192.168.2.158, mask: ffffff00, broad addr: 192.168.2.255
 - ip: fe80::216:3eff:fe14:78b9

interface 2: nflog

interface 3: nfqueue

interface 4: usbmon1

interface 5: usbmon2

interface 6: usbmon3

interface 7: usbmon4

interface 8: any

interface 9: lo
 - ip: 127.0.0.1
 - ip: ::1
```
