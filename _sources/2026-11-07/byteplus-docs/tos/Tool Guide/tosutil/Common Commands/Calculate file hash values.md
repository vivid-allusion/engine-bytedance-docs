---
title: "Calculate file hash values"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Calculate_file_hash_values"
---

You can use the `hash` command to calculate the CRC64 or MD5 hash values of local files or folders.

<span id="命令语法"></span>
## Command syntax


<Tabs>
<Tab zoneid="XBoyiGHy" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

* Calculate the hash value of a single local file


```Bash
./tosutil hash file_url [-type=xxx] [-conf=xxx]
```



* Batch calculate hash values for files within a local folder


```Bash
./tosutil hash folder_url -r [-type=xxx] [-conf=xxx]
```



* Batch calculate the hash values of files in a local folder and save the results to a local file


```Bash
./tosutil hash folder_url file_url|folder_url -r [-type=xxx] [-conf=xxx]
```





</Tab>
<Tab zoneid="YJd0VGcC" title="Windows">
<TabTitle>Windows</TabTitle>

* Calculate the hash value of a single local file


```Bash
tosutil hash file_url [-type=xxx] [-conf=xxx]
```



* Batch calculate the hash values of files in a local folder


```Bash
tosutil hash folder_url -r [-type=xxx] [-conf=xxx]
```



* Batch calculate the hash values of files in a local folder and save the results to a local file


```Bash
tosutil hash folder_url file_url|folder_url -r [-type=xxx] [-conf=xxx]
```





</Tab>
</Tabs>


<span id="1A3zgxTg"></span>
## Parameter description


|Parameter name |Type |Description |
|---|---|---|
|\-r |Bool |Batch calculate the hash values of all files in a local folder. |
|\-type |String |The algorithm used to calculate the hash value. Supported values are as follows:<br><br><br>* `crc64` (default)<br><br>* `md5`<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the algorithm is <code>md5</code>, the result includes both the Hex and Base64 encoded md5 values.</div><br> |


<span id="使用示例"></span>
## Usage example

Calculate the MD5 value of the local `/root/test` file.


* Command


```Plain
./tosutil hash ./test -type md5
```



* Return


```Plain
file-path:          /root/test
  hex-md5:          bb7c682dddea36e5ece23fb196ff****
  base64-md5:       u3xoLd3qNuXs4j+xlv/4****
```
