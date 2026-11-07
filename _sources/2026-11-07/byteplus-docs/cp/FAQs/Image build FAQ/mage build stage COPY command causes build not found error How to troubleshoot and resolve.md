---
title: "mage build stage COPY command causes build not found error How to troubleshoot and resolve"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/mage_build_stage_COPY_command_causes_build_not_found_error_How_to_troubleshoot_and_resolve"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue phenomenon

When running the image build and push task in the pipeline, the compile build step completes successfully, but the step for building and pushing the image to the repository fails. The run log displays: `ERROR: "/build": not found`.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis


1. The log indicates that the build directory cannot be found. First, confirm whether the build directory has been created. In the build step, print the list of files generated after the build and confirm that the build directory has been created.

2. Further investigate whether the build directory is hidden or ignored. Troubleshooting revealed that the build directory was included in the `.dockerignore` file, causing it to be excluded from the image during the build process.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>.dockerignore</code> is located in the root directory of the Docker build context and is used to exclude files or directories that do not need to be sent to the Docker daemon.</div>


<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution


1. Modify the `.dockerfile` file in the code repository, and remove the build directory from the `.dockerignore` file.

2. Rerun the pipeline.
