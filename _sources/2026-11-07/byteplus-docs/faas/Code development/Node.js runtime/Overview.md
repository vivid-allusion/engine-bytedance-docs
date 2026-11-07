---
title: "Overview"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Node_js_runtime_Overview"
---

When using Node.js runtime to develop functions in Function Service (FaaS), it is necessary to comply with the Node.js runtime specifications of BytePlus.

<span id="runtime-environment"></span>
## Runtime environment

The current Node.js runtime versions supported by the Function Service are as follows; you can select the desired runtime environment when creating a function.


* Node.js 14.x

* Node.js 20.x


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you wish to use another version of Node.js, you can achieve this through the deployment method using <a href="https://docs.byteplus.com/en/docs/faas/Native_runtime">Native runtime</a> image: import the runtime of the corresponding development language into the Dockerfile, package it with the image, and deploy using the image.</div>


<span id="file-system-restrictions"></span>
## File system restrictions

Only write operations are allowed in the /tmp directory within the container; default temporary storage space is 512 MiB. If the capacity limit is exceeded, the Service will be evicted and restarted.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">User local data written to disk is not persistent; data will be deleted when the container is destroyed, so use with caution. For persistent storage solutions, refer to <a href="https://docs.byteplus.com/en/docs/faas/Function_storage_selection">Function storage selection</a>.</div>
