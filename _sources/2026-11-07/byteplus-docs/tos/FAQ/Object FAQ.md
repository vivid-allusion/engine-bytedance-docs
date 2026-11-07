---
title: "Object FAQ"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/File-management"
---

##

|Category |FAQ |
|---|---|
|Uploading objects<br><br> |* [Why does uploading objects via the console feel slow?](https://docs.byteplus.com/en/docs/tos/File-management?lang=en#.5Li65LuA5LmI5Zyo5o6n5Yi25Y-w5LiK5Lyg5a-56LGh5oSf6KeJ6YCf546H6L6D5oWi77yf)<br><br>* [How does TOS limit the type and size of uploaded objects?](https://docs.byteplus.com/en/docs/tos/File-management?lang=en#evpm5rf1)<br><br>* [Does TOS support resumable upload?](https://docs.byteplus.com/en/docs/tos/File-management?lang=en#P702aBgp)<br><br>* [Does TOS support batch file upload?](https://docs.byteplus.com/en/docs/tos/File-management?lang=en#V3MuMmhC)<br><br>* [Why do I receive a 400 error when uploading objects with the multipart upload method?](https://docs.byteplus.com/en/docs/tos/File-management?lang=en#iFYqCyZb) |
|Downloading objects |[Does TOS support batch file download?](https://docs.byteplus.com/en/docs/tos/File-management?lang=en#fHGiqI5f) |
|Managing objects |* [Can deleted or overwritten TOS objects be recovered?](https://docs.byteplus.com/en/docs/tos/File-management?lang=en#hVYDpQtH)<br><br>* [How to recover TOS objects deleted by mistake?](https://docs.byteplus.com/en/docs/tos/File-management?lang=en#22A7mjEY)<br><br>* [What is the difference between a prefix and a folder?](https://docs.byteplus.com/en/docs/tos/File-management?lang=en#prvixSjk)<br><br>* [Does TOS support batch file deletion?](https://docs.byteplus.com/en/docs/tos/File-management?lang=en#BqC57DwX)<br><br>* [How to modify the file sharing expiration period when sharing files via URL?](https://docs.byteplus.com/en/docs/tos/File-management?lang=en#d3nGorG9)<br><br>* [How to set the validity period for public read files?](https://docs.byteplus.com/en/docs/tos/File-management?lang=en#d22093b1)<br><br>* [How can I list the objects in a specific directory?](https://docs.byteplus.com/en/docs/tos/File-management?lang=en#33d4a579) |

## Uploading objects

### Why does uploading objects via the console feel slow?

TOS does not limit your upload or download speed. If uploading objects through the console feels slow, possible reasons include:

* When uploading a single object, if it is large (MB\-level size), the TOS console relies on your browser to upload over the public network. The speed depends on your local network bandwidth from the public internet to the TOS service. Poor local network conditions (such as uploading via a browser on mobile with weak or slow networks) can cause longer upload times.

* When uploading in batches, the console is limited by the browser’s concurrency restrictions (for example, Chrome limits concurrency to 6), preventing high concurrent upload requests and resulting in slower overall batch uploads.

If you want to speed up object uploads, we recommend using TOS tools like [tosutil](https://docs.byteplus.com/docs/tos/overview) and [TOS Browser](https://docs.byteplus.com/docs/tos/Overview3).

### How does TOS limit the type and size of uploaded objects?

TOS supports a maximum direct upload of 5 GiB and a maximum multipart upload of 48.8 TiB.

There is no restriction on object types. If additional limits are needed, they must be implemented on the application side.

### Does TOS support resumable upload?

The support of resumable upload by various TOS management tools is shown in the following table.

|TOS management tool |Resumable upload |
|---|---|
|Console |Not supported |
|tosutil |Supported |
|TOS Browser |Supported |
|API |Not supported |
|SDK |* [Java](https://docs.byteplus.com/docs/tos/Breakpoint-resumption-java-sdk): supported<br><br>* [Python](https://docs.byteplus.com/docs/tos/Breakpoint-resumption-python-sdk): supported<br><br>* [Go](https://docs.byteplus.com/docs/tos/Breakpoint-resumption-go-sdk): supported<br><br>* [C++](https://docs.byteplus.com/docs/tos/Breakpoint-resumption-c-sdk): supported<br><br>* [Node.js](https://docs.byteplus.com/docs/tos/Breakpoint-resumption-node-js-sdk): supported<br><br>* [Browser.js](https://docs.byteplus.com/docs/tos/Breakpoint-resume-upload-browser-js-sdk): supported<br><br>* PHP: not supported<br><br>* iOS: Not supported<br><br>* [Android](https://docs.byteplus.com/docs/tos/Breakpoint-resume--android-sdk): Supported |

### Does TOS support batch file upload?

The support of batch file upload by various TOS management tools is shown in the following table.

|TOS management tool |Batch upload |
|---|---|
|Console |Supported |
|tosutil |Supported |
|TOS Browser |Supported |
|API |Not supported |
|SDK |Not supported |

### Why do I receive a 400 error when uploading objects with the multipart upload method?

One possible cause is that the part size does not meet the minimum requirement. When using multipart upload, all parts except the last one must be at least 4 MB. We recommend adjusting the part size.

## Downloading objects

### Does TOS support batch file download?

The support of batch file download by various TOS management tools is shown in the following table.

|TOS management tool |Batch download |
|---|---|
|Console |Not supported |
|tosutil |Supported |
|TOS Browser |Supported |
|API |Not supported |
|SDK |Not supported |

## Managing objects

### Can deleted or overwritten TOS objects be recovered?

* If version control is enabled, deleted objects can be restored.

* If version control is not enabled, deleted objects cannot be restored. Please operate with caution.

### How to recover TOS objects deleted by mistake?

To prevent accidental deletion, we recommend enabling version control. After enabling this feature, TOS automatically saves historical versions of your original data when you delete or overwrite data. In case of accidental operations, you can restore the data to a previous version to avoid data loss or unwanted changes. For more information, see [version control](https://docs.byteplus.com/docs/tos/docs-overview).

### What is the difference between a prefix and a folder?

Object storage uses a flat structure and does not have folders. However, you can simulate folders using prefixes, such as `a/b`. In object storage, a folder is a special type of prefix that ends with a slash (`/`).

### Does TOS support batch file deletion?

The support of batch file deletion by various TOS management tools is shown in the following table.

> **tip**

> When batch deleting files, the console is limited by the browser’s concurrency and memory restrictions, causing the overall batch deletion to be slow. We recommend using TOS Browser or tosutil to perform batch deletions.

|TOS management tool |Batch deletion |
|---|---|
|Console |Supported |
|tosutil |Supported |
|TOS Browser |Supported |
|API |Not supported |
|SDK |Not supported |

### How to modify the file sharing expiration period when sharing files via URL?

The maximum file sharing expiration period is 7 days. After generating the URL, it cannot be modified. If the file sharing period is about to expire, it is recommended to regenerate the pre\-signed URL. For detailed operation, please refer to [URL containing signature](https://docs.byteplus.com/docs/tos/reference-including-a-signature-in-the-url).

### How to set the validity period for public read files?

The validity period for public read files is long\-term. If you want to set a validity period, it is recommended to regularly batch set the files’ validity to private.

### How can I list the objects in a specific directory?

You can use the bucket inventory feature for this purpose. For more information, see [Bucket inventory](https://docs.byteplus.com/docs/tos/Bucket-inventory). Alternatively, you can use the `ls` command in tosutil. For more information, see [List objects or list multi-version objects in the bucket](https://docs.byteplus.com/docs/tos/List-the-resources-under-the-account-ls).

###
