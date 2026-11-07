---
title: "Installing the Java SDK"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Install-java-sdk"
---

Before running the TOS Java SDK, you must first install the SDK. This article outlines the operating environment requirements and provides multiple installation methods for the SDK.

<span id=".546v5aKD5YeG5aSH"></span>
## Environmental Preparation


* The SDK requires JDK version 1.8 or above to run on.

* All example code presented in this article can be executed successfully on IntelliJ IDEA and utilizes Maven version 3.6.3 as the package management tool.


<span id="b361eb03"></span>
## Category

The Java SDK depends on OkHttp. It is recommended to use version 4.x of the OkHttp library. The minimum required version of OkHttp is 3.9.1; using a lower version may result in the SDK failing to compile properly.

<span id=".5LiL6L295Zyw5Z2A"></span>
## Download Link


* Latest source code address: [Source code address](https://github.com/volcengine/ve-tos-java-sdk)

* Revision History: [Revision Record](https://github.com/volcengine/ve-tos-java-sdk/blob/main/CHANGELOG.md)

* Historical version address: [Historical version](https://github.com/volcengine/ve-tos-java-sdk/tags)

* Package Management Address: [Software Package Address](https://central.sonatype.com/artifact/com.volcengine/ve-tos-java-sdk)


<span id=".5a6J6KOF5pa55byP"></span>
## Installation Method

Currently, the TOS Java SDK supports three installation methods: installation via Maven, installation via Gradle, and direct installation using a Jar package. Using SDK version 2.8.8 as an example, the configuration is as follows.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">It is recommended that you use the latest version of the SDK; the latest version is determined by the updates on Git.</div>


<span id=".6YCa6L-HLW1hdmVuLeWuieijhQ=="></span>
### Installation via Maven

Configure as follows in the `pom.xml` file.

```xml
<dependency>
    <groupId>com.volcengine</groupId>
    <artifactId>ve-tos-java-sdk</artifactId>
    <version>2.8.8</version>
</dependency>
```


<span id=".6YCa6L-HLWdyYWRsZS3lronoo4U="></span>
### Installation via Gradle

Configure the `build.gradle` file as follows, and add dependencies in the `dependencies` section.

```apache
implementation 'com.volcengine:ve-tos-java-sdk:2.8.8'
```


<span id=".6YCa6L-HLWphci3ljIXlvJXlhaU="></span>
### Integration via JAR package

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before introducing via the JAR package, please download the latest <a href="https://repo1.maven.org/maven2/com/volcengine/ve-tos-java-sdk/2.8.8/ve-tos-java-sdk-2.8.8.jar">JAR package file</a>.</div>


<span id=".5ZyoLWludGVsbGlqLWlkZWEt5bel56iL6aG555uu5Lit5a-85YWlLXZlLXRvcy1qYXZhLXNkay1qYXIt5YyF44CC"></span>
#### Import the ve\-tos\-java\-sdk JAR package into the IntelliJ IDEA project.


1. Copy the downloaded `ve-tos-java-sdk-2.8.8.jar` file into your project.

2. In IntelliJ IDEA, select your project, right\-click, and choose **File \> Project Structure \> Modules \> Dependencies \> + \> JARs or directories**.

3. Select the `ve-tos-java-sdk-2.8.8.jar` file and import it into **External Libraries**.


<span id=".5ZyoLWVjbGlwc2Ut5bel56iL6aG555uu5Lit5a-85YWlLXZlLXRvcy1qYXZhLXNkay1qYXIt5YyF44CC"></span>
#### Import the ve\-tos\-java\-sdk JAR package into the Eclipse project.


1. Copy the downloaded `ve-tos-java-sdk-2.8.8.jar` file into your project.

2. In Eclipse, select your project and right\-click to choose **Properties \>** . **Java** **Build Path \> Add JARs**.

3. Select the `ve-tos-java-sdk-2.8.8.jar` file and import it into **Libraries**.
