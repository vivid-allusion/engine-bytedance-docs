---
title: "How can the image version number be dynamically updated"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/How_can_the_image_version_number_be_dynamically_updated"
---

You can dynamically update the image version number using environment variables. The specific method is as follows:


* Method 1: Use a predefined variable${DATETIME}

   In the image packaging and pushing task, set **image version** to `${DATETIME}` to enable the version number to change dynamically with the timestamp.

* Method 2: Use custom variables

   1. On the pipeline environment variable page, set the custom variable `version`, enter the default value, and turn on **dynamic settings**.

   2. In the task of packaging the image and pushing it to the image repository, **image version** is `${version}`.

   3. Save the pipeline configuration.

   4. For each subsequent manual run of the pipeline, you can dynamically update the version number by modifying the value of version.
