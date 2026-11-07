---
title: "How to configure pipeline caching to improve Go project build efficiency"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/How_to_configure_pipeline_caching_to_improve_Go_project_build_efficiency"
---

You need to add the `./.gomod` cache directory to your Go project's pipeline, and include this cache directory in the Go build command. The specific procedure is as follows:


1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp), select **workspace** from the navigation bar on the left, and select the target workspace name from the workspace list.

2. In the pipeline list, select the target pipeline, click **edit**, and by default, you will enter the **edit pipeline** page's **process configuration** tab.

3. Switch to the **Cache directory** tab, click ➕, and add a new cache directory.

   1. Directory: Enter the cache path. Here, set to `./.gomod`.

   2. Description: Customize the description of this Cache directory. Limited to 200 characters.

4. Switch to the **process configuration** tab, click **Go build task**, and in **build command**, enter the following command to add cache directory.

   ```shell
   #  Go 1.13 or above
   go env -w GOMODCACHE=$(pwd)/.gomod
   
   #  Go 1.13 or below
   export GOMODCACHE=$(pwd)/.gomod
   ```
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">You need to add this Cache directory before the build command; otherwise, this Cache directory will not work.   </div>
   

5. Click **Save** to save the pipeline configuration.
