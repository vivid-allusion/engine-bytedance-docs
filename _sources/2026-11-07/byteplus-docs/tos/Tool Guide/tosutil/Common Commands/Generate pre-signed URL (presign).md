---
title: "Generate pre-signed URL (presign)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Generate-pre-signed-url-presign"
---

A pre\-signed URL enables temporary authorization for others to access private resources without exposing object permissions. During the validity period, any user may download files via a pre\-signed link. You can use the `presign` command to generate a pre\-signed URL for downloading objects, enabling secure and convenient sharing of private objects.

<span id="6b29a390"></span>
## Command Syntax


<Tabs>
<Tab zoneid="yg3awwN3wW" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

* Generate a pre\-signed URL for a single object

   ```Bash
   ./tosutil presign tos://bucket/key [-vp=xxx] [-qp=xxx] [-versionId=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
   ```
   

* Batch generate pre\-signed URLs for objects with a specified prefix

   ```Bash
   ./tosutil presign tos://bucket/[prefix] -r [-vp=xxx] [-qp=xxx] [-include=*.xxx] [-exclude=*.xxx] [-d] [-v] [-marker=xxx] [-versionIdMarker=xxx] [-limit=1] [-bt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
   ```
   


</Tab>
<Tab zoneid="MlRSPZt6dX" title="Windows">
<TabTitle>Windows</TabTitle>

* Generate a pre\-signed URL for a single object

   ```Bash
   tosutil presign tos://bucket/key [-vp=xxx] [-qp=xxx] [-versionId=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
   ```
   

* Batch generate pre\-signed URLs for objects with a specified prefix

   ```Bash
   tosutil presign tos://bucket/[prefix] -r [-vp=xxx] [-qp=xxx] [-include=*.xxx] [-exclude=*.xxx] [-d] [-v] [-marker=xxx] [-versionIdMarker=xxx] [-limit=1] [-bt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
   ```
   


</Tab>
</Tabs>


<span id="5a3e4a98"></span>
## Parameter Description

For an explanation of general optional parameters, please refer to [General optional parameters](https://docs.byteplus.com/docs/tos/Command-format#.6YCa55So5Y-v6YCJ5Y-C5pWw).


|**Parameter** |**Type** |**Description** |
|---|---|---|
|\-vp |String |The validity period of a pre\-signed URL: Once configured, the pre\-signed URL will automatically expire after the specified duration. The valid period ranges from 1 minute to 7 days. If you configure the tosutil tool using a temporary access key, the maximum selectable validity period for the authorization code will be consistent with the expiration time of the temporary access key.<br><br>The default value is 1 day, indicating that the generated authorization code will expire after 1 day. This parameter supports the following configuration methods:<br><br><br>* w: Indicates that the unit is set to week.<br><br>* d: Indicates that the unit is set to days.<br><br>* h: Indicates that the unit is set to hours.<br><br>* min: Indicates that the unit is minutes.<br><br>* s: Indicates that the unit is seconds.<br><br><br>For example, `1d` indicates a validity period of 1 day, `1w` indicates a validity period of 1 week, and `1h` indicates a validity period of 1 hour.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you do not select a time unit, the default unit is seconds. For example, <code>2400</code> indicates a validity period of 2400 seconds.</div><br> |
|\-qp |String |Query parameters contained in the pre\-signed URL. |
|\-versionId |String |The version number of the single object for which the pre\-signed URL is to be generated; by default, the latest version of the object is used. |
|\-r |String |Batch generate pre\-signed URLs based on the specified object prefix. |
|\-include |String |When generating pre\-signed URLs in batches, use a name matching pattern to specify the objects authorized for access. The following characters are supported:<br><br><br>* `?`: Matches any single character.<br><br>* `*`: Matches multiple arbitrary characters.<br><br>* `#`: as a delimiter.<br><br><br>For example, `-include=*.png#*.txt` includes all objects ending with `.png` and `.txt`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To avoid parsing failures and similar issues caused by the operating system escaping special characters, it is recommended that you use quotation marks when setting the name matching pattern.</div><br> |
|\-exclude |String |When batch generating pre\-signed URLs, use a name matching pattern to exclude specified objects. The following characters are supported:<br><br><br>* `?`: Matches any single character.<br><br>* `*` : Matches multiple arbitrary characters.<br><br>* `#`: used as a separator.<br><br><br>For example, `-exclude=*.png#*.txt` excludes all objects ending with `.png` and `.txt`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To avoid parsing failures and related issues caused by the operating system escaping special characters, it is recommended to use quotation marks when configuring name matching patterns.</div><br> |
|\-d |String |Generate presigned URLs only for objects in the current directory, rather than recursively for all objects. |
|\-v |String |Generate pre\-signed URLs for multi\-version objects within the bucket; the generated result includes both the latest version and historical versions of the objects. |
|\-marker |String |The starting position of the object when generating pre\-signed URLs in batches. The system will sort objects in lexicographical order by their names and sequentially generate pre\-signed URLs for all objects following this parameter. |
|\-versionIdMarker |String |When batch\-generating pre\-signed URLs, you must use the `-marker` parameter to specify the starting position for multi\-version objects.<br><br>The system will sort objects by object name and version number in lexicographical order, and then individually generate pre\-signed URLs for all objects after this parameter. |
|\-limit |String |The maximum number of results returned when generating pre\-signed URLs in batches is 1,000 by default. |
|\-bt |String |Type of storage bucket. The value descriptions are as follows:<br><br><br>* `fns`: FNS bucket.<br><br>* `hns`: HNS bucket.<br><br><br>If the bucket type is not specified, the bucket type will be obtained from the bucket metadata by default. |


<span id="6f940e2c"></span>
## Usage Example

**Generate a pre\-signed URL for the object object.png in the bucket bucketname, valid for 2 hours.** 


* Command

   ```Bash
   ./tosutil presign tos://bucketname/object.png -vp=2h
   ```
   

* Return

   ```Bash
   https://bucketname.tos-cn-beijing.bytepluses.com.cn/object.png?X-Tos-Algorithm=TOS4-HMAC-SHA256&X-Tos-Credential=AKLTYWFkMGU0YjJkZGFjNGUwMTkxNTEwMzQzYzk0YzFmMWM%2F20250916%2Fcn-beijing%2Ftos%2Frequest&X-Tos-Date=20250916T071704Z&X-Tos-Expires=7200&X-Tos-Signature=76403344452b78c7e933fe54f109fb78bab6b233c53f9118dd29036****&X-Tos-SignedHeaders=host
   ```
   


**Generate a pre\-signed URL valid for 2 hours for objects in the bucket 'bucketname' with the prefix 'prefix'.** 


* Command

   ```Bash
   ./tosutil presign tos://bucketname/prefix -r -vp=2h
   ```
   

* Return

   ```Bash
   tos://bucketname/prefix-new.png
   https://bucketname.tos-cn-beijing.bytepluses.com.cn/prefix-new.png?X-Tos-Algorithm=TOS4-HMAC-SHA256&X-Tos-Credential=AKLTYWFkMGU0YjJkZGFjNGUwMTkxNTEwMzQzYzk0YzFmMWM%2F20250916%2Fcn-beijing%2Ftos%2Frequest&X-Tos-Date=20250916T071945Z&X-Tos-Expires=7200&X-Tos-Signature=3dc7be30794ee2ad5543fd194bbf18ca3f70a26da96b4567b9da32011****&X-Tos-SignedHeaders=host
   
   tos://bucketname/prefix-new.pptx
   https://bucketname.tos-cn-beijing.bytepluses.com.cn/prefix-new.pptx?X-Tos-Algorithm=TOS4-HMAC-SHA256&X-Tos-Credential=AKLTYWFkMGU0YjJkZGFjNGUwMTkxNTEwMzQzYzk0YzFmMWM%2F20250916%2Fcn-beijing%2Ftos%2Frequest&X-Tos-Date=20250916T071945Z&X-Tos-Expires=7200&X-Tos-Signature=137a2b25c6dab44c8c0e1dad93f8dbdbd50e2340b0b17a94bf68f426****&X-Tos-SignedHeaders=host
   ```
