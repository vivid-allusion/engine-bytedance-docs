---
title: "Install TLS SDK for Java"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/install_tls_sdk_for_java"
---

Before you use a Torch Log Service (TLS) SDK to perform operations, install the SDK. This topic describes how to install TLS SDK for Java.

<span id="前提条件"></span>
## Before you begin


* Create and get a BytePlus AccessKey pair.

* The AccessKey pair has the permissions to access all API actions, resulting in high risks. We recommend that you create and use an IAM user to call API actions or perform routine O&M. Before you perform operations as an IAM user, make sure that the IAM user is granted the permissions to operate TLS resources.


<span id="准备开发环境"></span>
## Preparing a development environment

TLS SDK for Java supports JDK 1.7 and later. Before you install the SDK, make sure that the Java development environment is set up. For more information, visit the [Java official website](http://developers.sun.com/downloads/).

Run the following command to view your Java version:

```bash
java -version
```


<span id="安装-sdk"></span>
## Installing the SDK

We recommend that you load TLS SDK for Java by adding dependencies to your Maven project.

To use TLS SDK for Java in your Maven project, simply add dependencies to the `pom.xml` file. Then, Maven automatically downloads the relevant JAR files. Specify the latest version in the version tag. To view the latest version of TLS SDK for Java, visit [Maven repository](https://central.sonatype.com/artifact/com.volcengine/volc-sdk-java/versions) or [GitHub tags](https://github.com/volcengine/volc-sdk-java/tags).

```XML
<dependency>
    <groupId>com.volcengine</groupId>
    <artifactId>volc-sdk-java</artifactId>
    <version>LATEST_VERSION</version>
</dependency>
```
