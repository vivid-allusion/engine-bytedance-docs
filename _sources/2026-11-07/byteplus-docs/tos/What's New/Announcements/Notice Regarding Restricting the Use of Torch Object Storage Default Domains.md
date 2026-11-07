---
title: "Notice Regarding Restricting the Use of Torch Object Storage Default Domains"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/2116749"
---

Starting August 1, 2026, to ensure business security and stability, BytePlus Torch Object Storage will restrict the use of buckets' default domain names. Specifically, the direct preview of any type of objects or the download of objects with `.apk`, `.ipa`, or `.hap` suffixes, using default domain names via pre\-signed or anonymous access, will be prohibited.

<span id="rGlyQY5F"></span>
## Estimated Change Time

2026\-08\-01. Please refer to the console for the specific time.

<span id="WPOVOt3I"></span>
## Change Description

For buckets created on or after August 1, 2026, the following changes will apply.


* For pre\-signed or anonymous access to objects using default domain names, TOS will automatically include the `Content-Disposition: attachment` parameter in the response header. This means that objects of any type will download directly to your local device instead of being previewed online.

* Accessing objects with `.apk`, `.ipa`, or `.hap` suffixes using a default domain name or pre\-signed URL will no longer be permitted. Attempting direct access will result in the following error:

   ```JSON
   HTTP/1.1 400 Bad Request
   
   {
       "Code": "ApkDownloadForbidden",
       "RequestId": "c35016853c8ceec656853c8-ac11c259-1r8dDM-LB-cb-tos-front-****",
       "HostId": "TQHYhZZTikZoNVVNxzQdLLRFyBLz****",
       "Message": "The APK file is not allowed to be distributed in a public network using the TOS endpoint, please use CNAME instead."
   }
   ```
   


<span id="vz17xXf3"></span>
## Impacts


* If you want to preview objects directly or download objects with `.apk`, `.ipa`, or `.hap` suffixes, you need to access them through a custom domain. For more information, see [Associating a custom domain](https://docs.byteplus.com/docs/tos/Set-up-a-custom-domain-name).

* The changes do not affect buckets created before August 1, 2026. However, we recommend using custom domain names to access objects in these buckets.
