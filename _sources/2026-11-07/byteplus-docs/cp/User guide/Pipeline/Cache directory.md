---
title: "Cache directory"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Cache_directory"
---

This article introduces the usage scenarios, purpose, and methods for using the cache directory, as well as other related content.

<span id=".5qaC6L-w"></span>
## Overview

When executing pipeline tasks, Code Pipeline creates a new build environment for each task node and destroys it after the build is complete. To address the issue of repeatedly downloading build dependencies when running the same pipeline task multiple times, Code Pipeline provides a custom cache feature. This feature allows users to store required build dependencies in the cache directory, enabling cache sharing across multiple runs of pipeline tasks and improving pipeline build efficiency.

For example, when a Node.js build task runs `npm install`, it generates `./node_modules` in the project. You can save `./node_modules` as a cache directory to speed up future downloads.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The cache is a task\-level cache. The cache for different tasks in different pipelines is isolated and can only be shared among different execution instances of the same task.</div>


* <div data-tips="true" data-tips-type="tip">The cache is retained for 365 days by default and will be cleared automatically if not used.</div>


* <div data-tips="true" data-tips-type="tip">The total size of cached resources allowed per account is limited to a total size of up to and including 5 GB. If this limit is exceeded, a message is displayed indicating that caching has failed.</div>



<span id=".6aKE572u57yT5a2Y55uu5b2V"></span>
## The preset cache directory

Code Pipeline by default provides the following cache directories to improve build efficiency. It is recommended that you turn on the required cache directory based on the compilation language.


|Package management tools |Cache directory |
|---|---|
|Java Maven |$(CP_WORKSPACE)/.m2 |
|Java Gradle |$(CP_WORKSPACE)/.gradle/caches |
|Node.js NPM |$(CP_WORKSPACE)/node_modules |


<span id=".6Ieq5a6a5LmJ57yT5a2Y55uu5b2V"></span>
## Custom cache directory

Supports customizing the cache directory for a task based on business requirements. This section explains how to set a custom cache directory.


1. Go to the cache directory tab of the pipeline.

   1. Log in to [Code Pipeline Console](https://console.byteplus.com/cp).

   2. Select **workspace** in the left navigation bar.

   3. Click the target workspace name to enter the current workspace.

   4. Select **Pipeline** in the left navigation bar. You will enter the pipeline page.

   5. In the pipeline list, select the target pipeline, and click  **`...`**  Click  **\> Edit** to enter the process orchestration tab of the current pipeline.

   6. Click **Cache directory** to switch to the Cache directory tab.

2. Click **Add Cache directory** to add a new cache directory. Supports adding multiple cache directories.

   
   |Configuration Item |Descriptions |
   |---|---|
   |Name |Customize the name of the current cache directory. |
   |Contents |Set the specific cache path. For example: `$(CP_WORKSPACE)/demo`.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The cache path must be a path under the <code>$(CP_WORKSPACE)</code> directory; otherwise, the shared cache feature will not function.</div><br> |
   |Description |Enter a description or remarks related to the cache directory. Up to 200 characters allowed. |
   

3. After the cache directory configuration is complete, click the **Save** at the bottom right to save the pipeline configuration.


<span id=".5riF55CG57yT5a2Y"></span>
## Clear cache

Manual clearing of the cache related to a specific pipeline is supported. After the cache is cleared, the cache will not be available when a pipeline\-related task is run for the first time.


1. Go to the cache directory tab of the pipeline.

   1. Log in to [Code Pipeline Console](https://console.byteplus.com/cp).

   2. Select **workspace** in the left navigation bar.

   3. Click the name of the target workspace to enter that workspace.

   4. Select **Pipeline** in the left navigation bar to enter the pipeline page.

   5. In the pipeline list, select the target pipeline, and click  **`...`**  Click  **\> Edit** to go to the process orchestration tab for the current pipeline.

   6. Click **Cache directory** to switch to the Cache directory tab.

2. Click **Clear cache** in the upper right corner. In the confirmation dialog that appears, click **confirm** to clear all cache for the current pipeline.
