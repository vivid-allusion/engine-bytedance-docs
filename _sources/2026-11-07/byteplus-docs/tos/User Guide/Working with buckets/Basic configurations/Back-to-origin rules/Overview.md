---
title: "Overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Overview9"
---

You can set back\-to\-source rules for buckets in the TOS console. When the requested object does not exist in the bucket, TOS will pull the target file from the source station where the rules are set.

<span id="7bea9fde"></span>
## Usage scenario

Mirroring back to the source and redirecting back to the source are suitable for scenarios where data is seamlessly migrated to TOS. During the process of migrating source station data to TOS, you can use the redirecting back to the source or mirroring back to the source function to enable users to access data that has not been migrated to TOS, ensuring that business will not be interrupted and that it will not affect the normal reading of data by users.

After setting the return to the source rule, you can use [HeadObject](https://docs.byteplus.com/docs/tos/reference-headobject) request to obtain object metadata, determine whether the object exists in the source station, and then use [GetObject](https://docs.byteplus.com/docs/tos/reference--getobject) the request to obtain the object, and save the unmigrated data to the TOS. Both mirroring back to the source and redirecting back to the source support saving the object to the TOS. The differences are as follows:


* Mirror back to the source: Pull the file from the source and return it to the requester, and store the file to the TOS to ensure the integrity of the data.

* Redirect back to the source: If you open **whether to pull back to the source file** , after pulling the file from the source station and returning it to the requester, it also supports saving the pulled file into the TOS to ensure the integrity of the data.


<span id="d11b58e5"></span>
## **Precautions**


|**Precautions** |**Description** |
|---|---|
|Back\-to\-Origin rule |* TOS supports the creation of up to 20 return rules. When there are multiple return\-to\-source rules, match them sequentially according to the order in the return\-to\-source rule list. When a rule is hit, subsequent rules are no longer matched. If you want to adjust the order of the back\-to\-source rules, you can use **the move up** or **down** function, For specific steps, please refer to [Other operations](https://docs.byteplus.com/docs/tos/35953#21aa45da).<br><br>* If the corresponding return condition is not matched, the corresponding rule will not be hit. |
|Back\-to\-Origin address |The return address does not support setting as an intranet address. |
|Back\-to\-Origin metadata |When saving a pulled file to TOS using the return\-to\-source rule, the following header returned by the source site is saved as the metadata of the file.<br><br>```Plain```<br>```Content-Language```<br>```Expires```<br>```Content-Disposition```<br>```Content-Encoding```<br>```Cache-Control```<br>```Content-Type```<br> |
|Cost |When using the mirror back to the source or redirect back to the source function to access the source station, the source station will generate outflow traffic from the public network, and the corresponding source station cloud manufacturer will charge corresponding fees. |
|Execution priority |If you configure the return to the source rule and use the static website function to configure the redirect rule, when using a custom domain name to access the TOS triggers a 404 error, the redirect rule of the static website will be executed first, and the return to the source rule will not be executed. |


<span id="7c432c7c"></span>
## Related Documentation


* [Create a Mirroring Back-to-Origin Rule](https://docs.byteplus.com/docs/tos/docs-setting-back-to-origin-rules)

* [Create a Redirection Back-to-Origin Rule](https://docs.byteplus.com/docs/tos/35953)
