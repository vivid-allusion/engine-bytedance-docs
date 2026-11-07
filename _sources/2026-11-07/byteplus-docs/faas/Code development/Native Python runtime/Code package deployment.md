---
title: "Code package deployment"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Native_Python_runtime_Code_package_deployment"
---

Native Python functions support code package deployment. Before conducting code package deployment, the completed code package needs to be packaged into a Zip file. This document introduces how to package Native Python functions.

<span id="limits"></span>
## Limits


* If using Python dependencies, it supports online installation of dependencies and packaging the dependency libraries together with the code for uploading. For more details, refer to [Python Dependency Installation](https://docs.byteplus.com/en/docs/faas/Python_runtime_Dependency_Installation).

* The Function Service console supports uploading Zip format files up to 256 MiB in size.


<span id="procedure"></span>
## Procedure

Execute the following command to package all files in the root directory into a vefaas\-native\-python.zip named .zip compressed file.

```shell
# This example is only illustrated with vefaas-native-python.zip, actual filename is unrestrictedzip -FSr vefaas-native-python.zip .
```


<span id="what-to-do-next"></span>
## What to do next


1. Create a function in the Function Service console, select "Create「Web applications」" and for Deployment method select Upload local file. For specific actions, refer to [Creating Web applications](https://docs.byteplus.com/en/docs/faas/Creating_Web_applications).

2. Release the function code and configurations to the cloud. For specific actions, refer to [Release function](https://docs.byteplus.com/en/docs/faas/Release_function).
