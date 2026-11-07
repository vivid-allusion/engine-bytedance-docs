---
title: "Can't see the symbol table on the platform after uploading it using a script?"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Can_not_see_the_symbol_table_on_the_platform_after_uploading_it_using_a_script"
---

1. First, check the project configuration to see whether the current build generates a symbol table.

&nbsp;

2. Check the order of added scripts in Build Phases.

&nbsp;

3. Check the script output.

   1. appID is not configured. Please refer to the "*Symbol table upload*" section of the integration documentation to configure the appID, then try again.

      <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/62f7a76c6dd34669ad275cd2d0126d06) </span>

   2. By default, the symbol table is not uploaded when compiling with the emulator. Please switch to compiling on a real device or refer to the *symbol table upload* section of the integration documentation for the relevant configuration.

      <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/d48e2aef9cee4b0986e325e913553fcf) </span>

   3. By default, symbol tables are not uploaded in Debug mode. Please modify the build options or refer to the *symbol table upload* section of the integration documentation for the relevant configuration.

      <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/e6c659192f774ea1847309ab0546bc18) </span>

   4. Symbol table upload was successful. If it is still not visible on the platform, please contact technical personnel for troubleshooting.

      <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/b85e1172de144355bb2d44d53019f82f) </span>
