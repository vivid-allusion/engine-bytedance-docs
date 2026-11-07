---
title: "How to preview objects in a browser?"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/How-to-preview-objects-in-a-browser"
---

If you encounter forced file download when accessing TOS files in a browser. You can check TOS and file metadata as follows, then take corresponding actions based on the results to enable file preview in the browser.


| Abnormal reason |Solution |
|---|---|
|When accessing web files in buckets created before 23:59:59 on January 3, 2024, or any type of files in buckets created after 23:59:59 on January 3, 2024, using the default domain name, TOS will automatically add the `Content-Disposition: attachment` parameter in the response header, causing the browser to forcibly download the file instead of previewing it. |* Access the object using a custom domain. For details, see [Set up a custom domain](https://docs.byteplus.com/docs/tos/Set-up-a-custom-domain-name).<br><br>* Access the object using BytePlus CDN or DCDN domain names. For details, see [Add a domain](https://docs.byteplus.com/docs/byteplus-cdn/domain-management_en). |
|When accessing files in a browser, the browser determines how to open the file based on the Content\-Type. If the Content\-Type declared in the HTTP response header does not match the actual file type, the browser cannot recognize the content structure correctly and can only force the file to be downloaded. |Set the correct Content\-Type according to the file type. For details, see [Manage file metadata](https://docs.byteplus.com/docs/tos/docs-managing-file-metadata). |
|If the `Content-Disposition` in the HTTP response header is set to `attachment`, the browser will download the file upon access. |Change `Content-Disposition` to `inline`. For details, see [Manage file metadata](https://docs.byteplus.com/docs/tos/docs-managing-file-metadata). |
