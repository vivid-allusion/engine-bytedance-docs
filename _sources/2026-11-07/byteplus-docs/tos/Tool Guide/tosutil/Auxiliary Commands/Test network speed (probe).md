---
title: "Test network speed (probe)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Test-network-speed-probe"
---

You can use the `probe` command to test single\-stream upload or download speed.

<span id="使用系统存储桶测试"></span>
## Test using the system bucket

When testing network speed with the system bucket, you do not need to configure AK and SK. After installing the tosutil tool, you can use the probe command to test speed.

<span id="命令格式"></span>
### Command format


<Tabs>
<Tab zoneid="tWsYOqfG" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

&nbsp;

```Bash
./tosutil probe [-pt=xxx] [-file=xxx] [-tr=xxx] [-nt=xxx] [-ps=1073741824] [-timeout=30]
```





</Tab>
<Tab zoneid="5OiDF3pF" title="Windows">
<TabTitle>Windows</TabTitle>

&nbsp;

```Bash
tosutil probe [-pt=xxx] [-file=xxx] [-tr=xxx] [-nt=xxx] [-ps=1073741824] [-timeout=30]
```





</Tab>
</Tabs>


<span id="参数说明"></span>
### Parameters


|**Parameter name** |**Type** |**Description** |
|---|---|---|
|\-pt |String |Type of speed test service. Valid values:<br><br><br>* upload (default): test upload service speed.<br><br>* download: test download service speed. |
|\-file |String |Local file path used for upload or download during speed test. If this parameter is not set, tosutil generates data from memory for upload or discards downloaded data directly from memory. |
|\-tr |String |Speed test region covering the main TOS areas. Valid values:<br><br><br>* cn\-beijing (default): North China 2 (Beijing)<br><br>* cn\-guangzhou: South China 1 (Guangzhou)<br><br>* cn\-shanghai: East China 2 (Shanghai)<br><br>* ap\-southeast\-1: Asia Pacific Southeast (Johor) |
|\-nt |String |Network type for speed test; supports specifying public or private network for testing. Valid values:<br><br><br>* public (default): test public network speed.<br><br>* internal: test private network speed. |
|\-ps |String |Test object size in bytes, range: [100MB, 5GB], default is 1GB.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Capacity units supported, for example, 100MB means 104857600 bytes.</div><br> |
|\-timeout |Integer |Speed test timeout in seconds, default is 30. Minimum is 30. |


<span id="使用示例"></span>
### Example

test upload speed using the system bucket


* command


```Plain
./tosutil probe -tr cn-beijing -pt upload
```



* return


```Plain
Start to test the uploading speed for region cn-beijing

Average upload rate: 5.65MB/s

Time consuming details
Resolve dns cost:      13 ms
Build connection cost: 42 ms
Tls handshake cost:    -1 ms
Send request cost:     29945 ms
Wait response cost:    -1 ms
Total cost:            30000 ms
```


<span id="使用自有存储桶测试"></span>
## Test using your own bucket

<span id="命令格式"></span>
### Command format


<Tabs>
<Tab zoneid="GFjOrZzZ" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

&nbsp;

```Bash
./tosutil probe tos://bucket[/prefix] [-pt=xxx] [-file=xxx] [-ps=1073741824] [-timeout=30] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
<Tab zoneid="GBFXsMjJ" title="Windows">
<TabTitle>Windows</TabTitle>

&nbsp;

```Bash
tosutil probe [-pt=xxx] [-file=xxx] [-tr=xxx] [-nt=xxx] [-ps=1073741824] [-timeout=30]
```





</Tab>
</Tabs>


<span id="参数说明"></span>
### Parameters


|**Parameter name** |**Type** |**Description** |
|---|---|---|
|bucket |String |Indicates testing with your own storage bucket. |
|prefix |String |The object name used during speed testing, with the following explanations:<br><br><br>* For upload tests, it represents the object name or object name prefix to upload to the bucket (object names will be generated randomly).<br><br>* For download tests, it represents downloading that object from the bucket.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">   ```Plain Text```<br>```   * for download testing, the selected object must be larger than 20MB.```<br>```   * if the specified object does not exist or is not set, tosutil first performs the upload task before testing the speed. tosutil deletes the uploaded object by default after speed testing, but deletion may fail due to network speed or permissions. In that case, tosutil will report a deletion failure error. It is recommended to delete the test object manually to avoid related storage costs.```<br>```   ```<br>      </div><br>    |
|\-pt |String |Type of speed test service. Valid values:<br><br><br>* upload (default): test upload speed.<br><br>* download: test download speed. |
|\-file |String |Local file path for upload or download during speed testing. If this parameter is not configured, tosutil will generate data from memory for upload or discard the downloaded data directly from memory. |
|\-ps |String |Object size for speed test, in bytes, with a range of [100MB, 5GB], default is 1GB.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Supports configuration with capacity units; for example, setting 100MB means 104,857,600 bytes.</div><br> |
|\-timeout |Integer |Speed test timeout in seconds, default is 30. Minimum is 30. |


<span id="使用示例"></span>
### Example usage

Use `bucket` to test the download rate of an `object` file


* Command


```Plain
./tosutil probe tos://bucket/object -pt download
```



* Return


```Plain
Start to test the uploading speed for region cn-beijing

Average download rate: 3.95MB/s

Time consuming details
Resolve dns cost:      -1 ms
Build connection cost: -1 ms
Tls handshake cost:    -1 ms
Send request cost:     0 ms
Wait response cost:    64 ms
Total cost:            30002 ms
```
