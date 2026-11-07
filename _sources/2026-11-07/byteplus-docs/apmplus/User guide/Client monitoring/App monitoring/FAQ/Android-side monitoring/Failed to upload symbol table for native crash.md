---
title: "Failed to upload symbol table for native crash"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Failed_to_upload_symbol_table_for_native_crash"
---


|Upload failure prompts |Cause Analysis |
|---|---|
|Native file is stripped |The uploaded .so file is stripped and does not contain debug_info, so it cannot be used to analyze stack traces. |
|Upload file with error UUID |The uploaded so file is not the not stripped version that matches the UUID of the so file where the crash occurred. Parsing with a mismatched version may result in incorrect information. |
