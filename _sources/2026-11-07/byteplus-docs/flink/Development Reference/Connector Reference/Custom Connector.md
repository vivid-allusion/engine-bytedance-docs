---
title: "Custom Connector"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Custom_Connector"
---

Stream computing Flink provides a variety of commonly used built\-in connectors; if these do not meet your needs, you can opt for a custom connector. Currently, the Flink console supports dynamically loading and invoking your custom connectors during task execution by adding dependency files.

<span id="7b7a0030"></span>
## Step One: Build Custom Connector Source Code

When developing a custom connector, you must adhere to the community\-defined connector standards for Flink to recognize and use it, so you need to clearly define the connector's metafile and declare the Factory class. For more information on custom connector development, see [User-defined Sources & Sinks](https://nightlies.apache.org/flink/flink-docs-release-1.11/dev/table/sourceSinks.html).

It is recommended to refer to the built\-in connector projects, modify the `pom.xml` configuration file, introduce the necessary dependencies, and then build the JAR package through Maven.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To avoid class conflicts between your custom\-built connector JAR package and the Flink platform, it is recommended to package the dependencies using the Shade method. For details on Shade packaging, please refer to <a href="https://maven.apache.org/plugins/maven-shade-plugin/index.html">Apache Maven Shade Plugin</a>.</div>


<span id="dd01440b"></span>
## Step Two: Upload Connector JAR Package

Once you have completed building your custom connector JAR package, you can upload the JAR package to the Flink platform's repository for unified management.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4feb5f7695184dd2a427bbfe8f74fc2a~tplv-goo7wpa0wc-image.image) </span>

<span id="124bfd5c"></span>
## Step Three: Reference Flink Parameters in the Connector JAR Package

In the Flink parameters of the target task, you can add your custom connector's JAR package as a dependency file, which will be dynamically loaded and invoked during runtime.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/adf6a3b2dec64e179eb3915dfdee62c8~tplv-goo7wpa0wc-image.image) </span>
