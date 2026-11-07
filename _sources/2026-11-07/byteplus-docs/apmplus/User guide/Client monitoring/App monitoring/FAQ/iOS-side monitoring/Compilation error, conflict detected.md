---
title: "Compilation error, conflict detected"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Compilation_error_conflict_detected"
---

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/d897e6080e7f4e26b625938c73548ed5) </span>

**Solutions**


* Solution 1: Upgrade Pangolin to 3.5.0.0 or later, and upgrade RangersAPM to 1.5.7 or later.

* Option 2: In the Build Settings of the target with compilation errors, set "Dead Code Stripping" to **YES**, and check whether  **\-all_load** is set in "Other Linker Flags". If it is, remove this option or replace it with  **\-force_load**.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/8cbc170a5c8f4233a7f6e97d4814bd06) </span>

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/becad7d6fad844d6b95159fa91704b7b) </span>
