---
title: "Download and installation"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Download_and_installation_java"
---

This topic describes how to download and install the Java SDK of NDB for MySQL.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Java JDK 1.7 or above is required.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can run the <code>java -version</code> command to check the version of the current Java.</div>


<span id=".c2RrLeS4i-i9veWcsOWdgA=="></span>
## SDK download address

Java SDK source code address, see [BytePlus SDK for Java](https://github.com/byteplus-sdk/byteplus-java-sdk-v2/tree/main/byteplus-java-sdk-v2-vedbm).

<span id=".5a6J6KOFLXNkaw=="></span>
## Install the SDK

Configure Maven project dependencies. Create a new Maven project and add the following settings in `pom.xml` in the project directory to introduce service dependencies. When a dependency is introduced, the Maven project management tool automatically downloads the relevant JAR package.

```xml
<dependency>
    <groupId>com.byteplus</groupId>
    <artifactId>byteplus-java-sdk-v2-vedbm</artifactId>
    <version>0.1.26</version>
</dependency>
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If your Java JDK version is JDK 9 or later and you need to add additional <code>javax.annotation-api</code> dependencies, add the following in <code>pom.xml</code>.</div>


<div data-tips="true" data-tips-type="tip">```xml
<dependency>
        <groupId>javax.annotation</groupId>
        <artifactId>javax.annotation-api</artifactId>
        <version>1.3.2</version>
</dependency>
```
</div>
