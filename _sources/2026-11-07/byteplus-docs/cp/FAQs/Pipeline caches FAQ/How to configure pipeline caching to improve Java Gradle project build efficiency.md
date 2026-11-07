---
title: "How to configure pipeline caching to improve Java Gradle project build efficiency"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/How_to_configure_pipeline_caching_to_improve_Java_Gradle_project_build_efficiency"
---

You need to add the `./.gradle` cache directory to the pipeline for your Java Gradle project. The specific steps are as follows:


1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp), in the left navigation bar, select the **workspace**, and then select the target workspace name from the workspace list.

2. In the pipeline list, select the target pipeline, click **edit**. By default, this opens the **Edit pipeline** page, with the **Process configuration** tab selected.

3. Switch to the **Cache directory** tab, click ➕, and add a new cache directory.

   1. Directory: Specify the cache path. Set it to `./.gradle` here.

   2. Description: Customize the description for this cache directory. Maximum 200 characters.

4. Click **Save** to save the pipeline configuration.
