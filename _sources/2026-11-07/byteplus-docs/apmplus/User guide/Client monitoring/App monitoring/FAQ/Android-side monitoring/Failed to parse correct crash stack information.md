---
title: "Failed to parse correct crash stack information."
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Failed_to_parse_correct_crash_stack_information"
---

**Problem description**

There is an issue with the number of lines parsed from the stack; the correct file information is not being obtained.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_dac465eba0650cb5baf93db9059b0c58.png) </span>

**Questions and answers**

The symbol table has not been uploaded. Upload the corresponding symbol table and then retrace.


* Symbol table extensions

   There are two methods for uploading, and all uploaded symbol tables can be viewed in **Symbol Table Management**.

   1. Scripts are uploaded automatically. Configuration is performed during SDK integration.

   2. On the crash details page, upload the symbol table and associate it with the version to perform stack retrace. In theory, different stack traces from the same version will share the same symbol table for parsing.

      Newly uploaded symbol tables will automatically parse newly reported crashes. By default, stack traces reported before the upload are not processed. To analyze old stacks, you can retrace them manually.

* Retrace extension

   Android Studio provides the command\-line tool retrace. The old stack traces were not successfully parsed after running retrace in the console; you can use this tool to test locally.
