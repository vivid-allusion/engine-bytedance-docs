---
title: "Determine whether the server allows the upload of memory files"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Determine_whether_the_server_allows_the_upload_of_memory_files"
---

You can use the following methods to determine whether the server allows uploading memory files:


* View DebugLog.

   * If the logs contain `MemoryGraph file is uploading...`, this means that the memory file is allowed to be uploaded this time.

   * If the Logs contain `Upload MemoryGraph -- server check failed.`, this indicates that the memory file cannot be uploaded.

* Use Charles to capture packets and view the return value of the API endpoint: https://apmplus.volces.com/monitor/collect/c/ios_memory_upload_check.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/56f599a56480441eb32e4bab688558e7) </span>

   * If the response result of this interface is `true`, it indicates that the current memory file is allowed to upload.

   * If the access returned by this interface is `false`, uploading the memory file for this session is not allowed.
