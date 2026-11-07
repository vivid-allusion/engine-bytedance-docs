---
title: "How to resolve slow or failed base image pulls during image build"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/How_to_resolve_slow_or_failed_base_image_pulls_during_image_build"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue phenomenon

When the pipeline executes the task of building an image and pushing it to the image repository, pulling the required base image is slow and may even fail. Build error: `error: failed to solve: failed to compute cache key: failed to read expected number of bytes: unexpected EOF`.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

Possible causes are as follows:


* Network connectivity between the base image repository and the build cluster is poor, for example, across borders.

* The repository's rate limiting mechanism was triggered; for example, Dockerhub restricts the number of image pulls.


<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution

It is recommended to store your base image in the BytePlus image repository CR, and download the base image from the image repository CR in your Dockerfile.
