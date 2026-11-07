---
title: "Code package deployment"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Native_runtime_Code_package_deployment"
---

Native functions support two deployment methods: code package deployment and image deployment. Before proceeding with the code package deployment, the completed code package needs to be packaged into a Zip file. This topic introduces how to package Native functions.

<span id="limits"></span>
## Limits


* If the execution of the main program depends on other local files (such as config.yaml), it is necessary to package the dependent files together, and files are referenced through relative positions in the code.

* The function Service console supports uploading Zip format files up to 256 MiB in size.


<span id="procedure"></span>
## Procedure


1. If you are using a compiled language such as Golang for development, you need to write a compilation script build.sh before packaging, to compile the code. The code example for the compilation script build.sh is as follows.

   ```bash
   #! /bin/bash
   set -ex
   cd `dirname $0`
   
   go mod tidy
   
   # Note: the binary should be compiled using linux env so as to run on FaaS Platform XD.
   GOOS=linux GOARCH=amd64 go build -v -ldflags '-w -extldflags "-static"' -o main
   ```
   

2. In the current directory of the program, execute the following commands to compile and package.

   ```shell
   ./build.sh
   
   zip -FSr vefaas-native-default.zip .
   ```
   


<span id="what-to-do-next"></span>
## What to do next


1. Create a function in the Function Service console, select to create "Web Application," and select local upload of a Zip package for Deployment. For detailed actions, refer to [Creating Web applications](https://docs.byteplus.com/en/docs/faas/Creating_Web_applications).

2. Release your function code and configurations to the cloud. For detailed actions, refer to [Release function](https://docs.byteplus.com/en/docs/faas/Release_function).
