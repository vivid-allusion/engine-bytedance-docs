---
title: "Pull only the code source of the latest version of the code source"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Pull_only_the_code_source_of_the_latest_version_of_the_code_source"
---

By configuring the clone depth of the input code source, you can choose to pull only the latest version or several recent versions when running the pipeline, which avoids pulling the entire input source and improves pipeline execution efficiency. This document describes how to set the clone depth for the input source in a pipeline.

<span id=".5Yqf6IO95LuL57uN"></span>
## Feature introduction

The clone depth value is the number of the most recent versions fetched by the pipeline.


* `0`Fetch all versions of the input source.

* `1`Pull the most recent 1 version.

* `2`Pull the latest two versions, and so on.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A code source has already been created in Code Pipeline. For operation details, refer to [Integrate code source](https://docs.byteplus.com/en/docs/cp/Create_a_code_source).

* The pipeline has been created. For operation details, refer to [Create a pipeline](https://docs.byteplus.com/en/docs/cp/Create_pipelines).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp).

2. Select **workspace** from the left navigation bar, and enter the **workspace** page.

3. Select the name of the target workspace in the workspace list to enter that workspace.

4. In the pipeline list, select the target pipeline, click **edit**. By default, the **edit pipeline** page opens to the **process configuration** tab.

5. On the **code source & trigger** tab, click **Add \> Code source**.

6. In the pop\-up **configure input source** dialog box, enter the clone depth value.


7. Click **confirm** to complete the operation.
