---
title: "Why are some stack traces still unresolved after uploading the symbol table?"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Why_are_some_stack_traces_still_unresolved_after_uploading_the_symbol_table"
---

* Click **Retry retrace** to attempt to parse again.

&nbsp;

* If you rely on other third\-party SDKs, please check whether these SDKs include dynamic libraries. The symbol table for the dynamic library itself must be uploaded separately. Please request the symbol table from the provider of the dynamic library. You can refer to the following methods to determine whether a library is a dynamic library:

   ```PowerShell
   cd libName.framework
   file libName
   ```
   

   If the command line output contains \*`dynamically linked shared library`\*, it is a dynamic library.
