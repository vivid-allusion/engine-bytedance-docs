---
title: "Java application hosting overview"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Java_application_hosting_overview"
---

Code Pipeline supports hosting Java applications as containers in Kubernetes clusters. You do not need to understand Kubernetes internals or learn how to build container images or complex YAML syntax. You can deploy applications to containers and manage the entire lifecycle of your application within containers.

<span id=".5a6e546w5Y6f55CG"></span>
## Implementation principles

After you upload a JAR or WAR package, Code Pipeline automatically creates a Dockerfile, builds a container image from the application package, and uploads the image to Container Registry (CR). At the same time, create a YAML configuration file for the application, and then deploy the application to the Kubernetes cluster.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6e4a9c661ee7b2a8e0f8d01e2fb4d5b7.png) </span>
