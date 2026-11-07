---
title: "Download and installation"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/download_and_installation_4"
---

This topic describes how to download and install the Java SDK of RDS for MySQL.

<span id="prerequisites"></span>
## **Prerequisites**

Java JDK v1.7 or higher is required. For more details, refer to [Java Downloads](https://www.oracle.com/java/technologies/downloads/).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div>


<div data-tips="true" data-tips-type="tip">You can check the current version of Java by running the <code>java -version</code> command.</div>


<span id="sdk-download-address"></span>
## **SDK** **download address**

For the Java SDK source code address of RDS for MySQL, refer to .

<span id="install-the-sdk"></span>
## Install the **SDK**

Configure Maven project dependencies. Create a new Maven project and add the following settings into the `POM.XML` under the project directory to introduce service dependencies. After the dependencies are introduced, the Maven project management tool will download the related JAR package automatically.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div>


<div data-tips="true" data-tips-type="tip">If your Java JDK is JDK v9 or higher, you need to add additional <code>javax.annotation-api</code> dependencies. Please add the following content to the <code>pom.xml</code>.</div>


<div data-tips="true" data-tips-type="tip">```shell
<dependency> <groupId>javax.annotation</groupId> <artifactId>javax.annotation-api</artifactId> <version>1.3.2</version> </dependency>
xml
```
</div>


```xml
<dependency>
    <groupId>com.volcengine</groupId>
    <artifactId>volcengine-java-sdk-rdsmysqlv2</artifactId>
    <version>0.1.28</version>
</dependency>
```


&nbsp;
