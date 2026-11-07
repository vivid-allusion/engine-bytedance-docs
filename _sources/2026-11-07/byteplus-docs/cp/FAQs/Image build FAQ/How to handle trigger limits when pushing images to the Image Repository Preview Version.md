---
title: "How to handle trigger limits when pushing images to the Image Repository Preview Version"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/How_to_handle_trigger_limits_when_pushing_images_to_the_Image_Repository_Preview_Version"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue phenomenon

Failed to build and push the image to the image repository (preview edition); the runtime log error indicates that the quota limit for the preview edition was reached.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The Image Repository trial version is no longer available. To continue using the service, please log in to the <a href="https://console.byteplus.com/cr/region:cr+cn-beijing/instances/create">console purchase page</a> to purchase another version.</div>


The BytePlus image repository trial version is subject to limitations on **storage capacity**, **data volume per image layer**, and **number of concurrent requests**. For specific values, see [Image repository trial version usage limits](https://docs.byteplus.com/en/docs/cr/limits).


* When the storage capacity limit is reached, an error will be reported in the pipeline run log: `exceed the configured upper limit of xx GiB`.

* If the data size limit for a single image layer is exceeded, the pipeline run log will report the error `image layer size too large`.

* If the request concurrency limit is triggered, the pipeline run log will report an error `429 Too Many Requests`.


<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution

The standard edition of the image repository does not have the above limitations and supports secure hosting and large\-scale distribution. We recommend that you migrate your image repository to the standard edition.
