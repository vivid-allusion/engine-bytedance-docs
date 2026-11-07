---
title: "There is an uploaded release; why can't Sourcemap find the uploaded content?"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/There_is_an_uploaded_release_why_can_not_Sourcemap_find_the_uploaded_content"
---

The length of the release field must not exceed 16 bytes, and it should comply with semantic versioning conventions.

If the release exceeds the maximum allowed length, the platform will automatically truncate the excess portion of the release, resulting in the loss of the Sourcemap file.
