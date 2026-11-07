---
title: "Delete breakpoint record files (clear)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Delete-breakpoint-log-file-clear"
---

You can use the `clear` command to delete breakpoint record files in the specified folder and perform cloud cleanup.

<span id=".5ZG95Luk6K-t5rOV"></span>
## Command syntax


<Tabs>
<Tab zoneid="7aHTcufU" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

&nbsp;

```Bash
./tosutil clear [checkpoint_dir] [-u] [-d] [-c] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
<Tab zoneid="cKPmfJ02" title="Windows">
<TabTitle>Windows</TabTitle>

&nbsp;

```Bash
tosutil clear [checkpoint_dir] [-u] [-d] [-c] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
</Tabs>


<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter description

For details on common optional parameters, see [general parameters](https://docs.byteplus.com/docs/tos/Command-format#.6YCa55So5Y-v6YCJ5Y-C5pWw).


|**Parameter name** |**Type** |**Description** |
|---|---|---|
|checkpoint_dir |String |Specifies the folder for breakpoint resume record files. The default is the `defaultCheckpointDir` in the configuration file. |
|\-u |Bool |Delete all breakpoint record files for shard upload tasks. |
|\-d |Bool |Delete all breakpoint record files of segmented download tasks |
|\-c |Bool |Delete all breakpoint record files for shard replication tasks. |


<span id=".6L-Q6KGM56S65L6L"></span>
## Example run


* Command


```Plain
./tosutil clear -u
```



* Return


```Plain
Clear checkpoint files for uploading in folder [/Users/.tosutil_checkpoint/upload]
Start at 2022-08-11 06:57:56.183432 +0000 UTC

[----------------------------------------------------------------------------------------------------] 100.00% 1/1 129ms
Succeed files is:   1         Failed files is:    0
```
