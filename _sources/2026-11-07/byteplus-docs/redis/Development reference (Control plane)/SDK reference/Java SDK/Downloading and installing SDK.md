---
title: "Downloading and installing SDK"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/downloading_and_installing_an_SDK"
---

This topic describes how to download and install Redis Java SDK.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Java JDK 1.8.0_131 or later is required. For more details, refer to [Java Downloads](https://www.oracle.com/java/technologies/downloads/).

<span id=".c2RrLeS4i-i9veWcsOWdgA=="></span>
## SDK download address

For Redis Java SDK source code address, refer to [Redis Java SDK](https://github.com/byteplus-sdk/byteplus-java-sdk-v2/tree/main/byteplus-java-sdk-v2-redis).

<span id=".5a6J6KOFLXNkaw=="></span>
## Install SDK

You need to install the Redis Java SDK by configuring the dependencies of the Maven project.

Create a new Maven project, then add the following settings to the `pom.xml` file in the project directory to include service dependencies. After the dependencies are imported, the Maven project management tool automatically downloads the relevant JAR packages.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If your Java JDK version is 9 or above, you also need to add the <code>javax.annotation-api</code> dependency. Add the following content to <code>pom.xml</code>.</div>


   <div data-tips="true" data-tips-type="tip">   ```XML
   <dependency>
       <groupId>javax.annotation</groupId>
       <artifactId>javax.annotation-api</artifactId>
       <version>1.3.2</version>
   </dependency>
   ```
      </div>
   

* <div data-tips="true" data-tips-type="tip">The version (<code>0.1.55</code>) in the dependencies below are for code example reference only. We recommend visiting <a href="https://github.com/byteplus-sdk/byteplus-java-sdk-v2/releases">BytePlus Java SDK Release</a> to view and use the latest SDK version.</div>



```xml
<dependencies>
  <dependency>
    <groupId>com.byteplus</groupId>
    <artifactId>byteplus-java-sdk-v2-redis</artifactId>
    <version>0.1.55</version>
  </dependency>
</dependencies>
```
