---
title: "Deployment method"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Python_runtime_Deployment_method"
---

Python functions support console online edit and upload code packages simultaneously. When using local Zip file upload, TOS upload method to submit code Zip packages, please follow the following specifications.


* The code package must contain a Python source file named index.py.

* The index.py file must contain a Python function named handler.

* The index.py file and related dependent code must comply with the Python version specification.

* If the execution of the main program depends on other local files (such as config.yaml), it supports two methods: online installation of dependencies and uploading packaged dependencies with the code. For details, refer to [Dependency installation](https://docs.byteplus.com/en/docs/faas/Python_runtime_Dependency_Installation).

* The function Service console supports uploading Zip format files up to 256 MiB in size.
