---
title: "Deployment method"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Node_js_runtime_Deployment_method"
---

Node.js functions support both console online editing and code package uploading. When using local Zip file upload, TOS upload method to submit code Zip packages, please follow the following specifications.


* The code package must contain a JavaScript source file named `index.js`.

* The `index.js` file must contain a Node.js function named handler.

* The `index.js` file and related dependency code must comply with the Node.js version specifications.

* If the execution of the main program depends on other local files (such as `config.yaml`), it supports two methods: online installation of dependencies and uploading packaged dependencies with the code. For details, refer to [Dependency installation](https://docs.byteplus.com/en/docs/faas/Node_js_runtime_Dependency_Installation).

* The function Service console supports uploading Zip format files up to 256 MiB in size.
