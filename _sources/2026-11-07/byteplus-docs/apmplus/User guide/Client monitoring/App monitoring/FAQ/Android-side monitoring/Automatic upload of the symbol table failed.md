---
title: "Automatic upload of the symbol table failed"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Automatic_upload_of_the_symbol_table_failed"
---

1. Confirm whether to turn on obfuscation. The mapping will only be uploaded if obfuscation is turned on.

   As shown in the figure below, add **minifyEnabled true** to the corresponding build type in buildTypes of the `build.gradle` file in the module directory of the app.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bab29a4eac5c47859e664edcdecc892f~tplv-goo7wpa0wc-image.image) </span>

2. Check whether the token is correct. For details, refer to [How to query AppID and AppToken?](https://docs.byteplus.com/en/docs/apmplus/Query_AppID_and_AppToken).
