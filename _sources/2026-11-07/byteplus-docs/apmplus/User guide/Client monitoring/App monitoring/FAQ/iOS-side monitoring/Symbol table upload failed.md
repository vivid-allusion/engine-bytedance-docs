---
title: "Symbol table upload failed"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Symbol_table_upload_failed"
---

When uploading the symbol table, you need to use a dSYM file.

A single sym file should be compressed into a zip file before upload; multiple dsym files should be compressed into one zip file for upload.

```Plain Text
zip -r  xxx.zip xxx.dSYM xxxx.dSYM
```


If the dSYM files have been processed by Bugly, they cannot be recognized.

For more information about symbol tables, refer to [Step 4: Upload symbol tables](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_iOS_SDK_app#403a16c4).
