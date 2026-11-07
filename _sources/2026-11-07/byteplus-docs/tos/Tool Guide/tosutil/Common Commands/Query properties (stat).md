---
title: "Query properties (stat)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Query-properties-stat"
---

You can use the `stat` command to query bucket properties or object properties.

<span id=".5p-l6K-i5qG25bGe5oCn"></span>
## Query bucket properties

<span id=".5ZG95Luk6K-t5rOV"></span>
### Command syntax


<Tabs>
<Tab zoneid="cAz63Odl" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

&nbsp;

```Bash
./tosutil stat tos://bucket [-acl] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
<Tab zoneid="jLPiKTn3" title="Windows">
<TabTitle>Windows</TabTitle>

&nbsp;

```Bash
tosutil stat tos://bucket [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
</Tabs>


<span id="X6UKC0hr"></span>
### Parameters

For descriptions of common optional parameters, see [General parameters](https://docs.byteplus.com/docs/tos/Command-format#.6YCa55So5Y-v6YCJ5Y-C5pWw).


|**Parameter name** |**Type** |**Description** |
|---|---|---|
|bucket |String |Bucket name. |
|\-acl |Bool |Query bucket properties and bucket access policy simultaneously. |


<span id=".5L2_55So56S65L6L"></span>
### Example

The following command queries the properties of the **bucketname** bucket.


* Command


```Plain
./tosutil stat tos://bucketname
```



* Output


```Plain
Start at 2022-10-27 10:42:49.230198 +0000 UTC
 
Bucket:
  tos://bucketname
Region:
  cn-beijing
StorageClass:
  STANDARD
```


<span id=".5p-l6K-i5a-56LGh5bGe5oCn"></span>
## Query object properties

<span id=".5ZG95Luk6K-t5rOV"></span>
### Command syntax


<Tabs>
<Tab zoneid="gK8aWooUwz" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

&nbsp;

```Bash
./tosutil stat tos://bucket/key [-acl] [-versionId=xxx] [-sbh] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
<Tab zoneid="OcA3pOztj5" title="Windows">
<TabTitle>Windows</TabTitle>

&nbsp;

```Bash
tosutil stat tos://bucket/key [-acl] [-versionId=xxx] [-sbh] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
</Tabs>


<span id=".5Y-C5pWw6K-05piO"></span>
### Parameters

for the description of general optional parameters, see [General parameters](https://docs.byteplus.com/docs/tos/Command-format#.6YCa55So5Y-v6YCJ5Y-C5pWw).


|**Parameter** |**Type** |**Description** |
|---|---|---|
|bucket |String |Bucket name. |
|key |String |Object name. |
|\-acl |Bool |Query object properties and access policies simultaneously. |
|\-versionId |String |Specify the object version when querying object properties. |
|\-sbh |Bool |Display the object’s HTTP basic headers when querying the object properties. |


<span id=".5L2_55So56S65L6L"></span>
### Example

the following command queries the properties of the **object1.png** object in the **bucketname** bucket, including HTTP basic header fields.


* Command


```Plain
./tosutil stat tos://bucketname/object1.png -sbh
```



* Output


```Plain
Start at 2022-10-27 10:43:24.667148 +0000 UTC
 
Key:
  tos://bucketname/object1.png
LastModified:
  2022-08-29 08:50:54 +0000 UTC
Size:
  29098
StorageClass:
  STANDARD
VersionID:
  57CE0809CDADB97E0EFC
HashCrc64ecma:
  644630079489775590
ETag:
  cbd8273ce352dfac24d5d65fa3f81dc0
ContentType:
  image/png
ContentDisposition:
  attachment;filename="test.png"
ContentLanguage:
  en
Type:
  file
```
