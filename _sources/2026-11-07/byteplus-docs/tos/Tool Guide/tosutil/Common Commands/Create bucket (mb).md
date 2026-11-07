---
title: "Create bucket (mb)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Create-bucket"
---

You can create a bucket using the `mb` command.

<span id=".5ZG95Luk6K-t5rOV"></span>
## Command syntax


<Tabs>
<Tab zoneid="Sz5lSuG0Ev" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

&nbsp;

```Bash
./tosutil mb tos://bucket [-acl=xxx] [-sc=xxx] [-az=xxx] [-bt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
<Tab zoneid="GGTFEPDrpk" title="Windows">
<TabTitle>Windows</TabTitle>

&nbsp;

```Bash
tosutil mb tos://bucket [-acl=xxx] [-sc=xxx] [-az=xxx] [-bt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
</Tabs>


<span id=".5Y-C5pWw6K-05piO"></span>
## Parameters

For descriptions of common optional parameters, see [general parameters](https://docs.byteplus.com/docs/tos/Command-format#.6YCa55So5Y-v6YCJ5Y-C5pWw).


|**Parameter name** |**Type** |**Description** |
|---|---|---|
|bucket |String |Bucket name. For bucket naming rules, see [common concepts](https://docs.byteplus.com/docs/tos/docs-common-concepts#bucket). |
|\-acl |Enum |Predefined access policies that can be specified when creating a bucket. Valid values:<br><br><br>* `private`: private, the default value.<br><br>* `public-read`: public read access.<br><br>* `public-read-write`: public read and write access.<br><br>* `authenticated-read`: authenticated user read.<br><br>* `bucket-owner-read`: bucket owner read.<br><br>* `bucket-owner-full-control`: bucket owner full control. |
|\-sc |Enum |The default storage type of the bucket, possible options:<br><br><br>* `STANDARD`: standard storage, default value.<br><br>* `IA`: infrequent access storage.<br><br>* `ARCHIVE_FR`: archive flash recovery storage.<br><br>* `ARCHIVE`: archive storage.<br><br>* `COLD_ARCHIVE`: cold archive storage.<br><br>* `DEEP_COLD_ARCHIVE`: deep cold archive storage.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Currently, only North China 2 (Beijing), East China 2 (Shanghai), and South China 1 (Guangzhou) support cold archive storage.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Currently, only North China 2 (Beijing), East China 2 (Shanghai), and South China 1 (Guangzhou) support deep cold archive, all in invitation\-only beta. Contact your account manager to use this storage type.</div><br> |
|\-az |Enum |The bucket’s availability zone redundancy type can be specified when creating a bucket. Valid values:<br><br><br>* `single-az`: single AZ redundancy, default.<br><br>* `multi-az`: multi\-AZ redundancy. |
|\-bt |Enum |The type of bucket that can be specified when creating a bucket. Valid values:<br><br><br>* `fns`: flat bucket.<br><br>* `hns`: hierarchical bucket.<br><br><br>For details, see [bucket types](https://docs.byteplus.com/docs/tos/Bucket-type). |


<span id="5e70df1f"></span>
## Example

The following command creates a bucket named **bucketname** with a private ACL (**private**) and storage type set to standard storage (**STANDARD**).


* Command


```Bash
./tosutil mb tos://bucketname -acl=private -sc=STANDARD
```



* Return


```Bash
Start at 2022-10-27 09:33:41.47976 +0000 UTC
 
Create bucket [bucketname] successfully, request id [9202485a5075b07a635a5075-ac10722e-1onzGf-CB-cb-tos-bj]
```
