---
title: "Create folder (mkdir)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Create-folder-mkdir"
---

You can create folders locally or in the cloud using the `mkdir` command.

<span id="9413cc56"></span>
## Command syntax


<Tabs>
<Tab zoneid="K8cKX7Ap6o" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

&nbsp;

```Bash
./tosutil mkdir tos://bucket/clouder_folder [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
<Tab zoneid="i2RiznJK2g" title="Windows">
<TabTitle>Windows</TabTitle>

&nbsp;

```Bash
tosutil mkdir tos://bucket/clouder_folder [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
</Tabs>


<span id="b357ecad"></span>
## Parameters

For descriptions of common optional parameters, see [general parameters](https://docs.byteplus.com/docs/tos/Command-format#.6YCa55So5Y-v6YCJ5Y-C5pWw).


|**Parameter name** |**Type** |**Description** |
|---|---|---|
|bucket |String |Bucket name. Bucket naming rules, see [common concepts](https://docs.byteplus.com/docs/tos/docs-common-concepts#bucket). |
|clouder_folder |String |Cloud folders support multi\-level directories, such as `a/b/c/`, with trailing forward slashes added automatically. |


<span id="cd771e05"></span>
## Usage examples


* Command

   ```Bash
   ./tosutil mkdir tos://bucketname/a/b/c
   ```
   

* Return

   ```Bash
   Start at 2024-03-19 12:34:58.745421 +0000 UTC
   
   Create cloud folder [a/b/c/] in bucket [bucketname] successfully, request id [2f8e01f98672b6b065f98672-ac1d9c55-1rmYgE-PuO-cgb-tos]
   ```
