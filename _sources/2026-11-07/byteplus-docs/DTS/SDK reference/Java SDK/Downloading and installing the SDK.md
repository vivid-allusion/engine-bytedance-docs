---
title: "Downloading and installing the SDK"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/downloading_and_instaling_the_sdk"
---

This topic introduces how to download and install the DTS Java SDK.

<span id="8ayJcx7U"></span>
## **Prerequisites**

Java JDK 1.8 or above is required. For more details, refer to [Java Downloads](https://www.oracle.com/java/technologies/downloads/).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">After successful installation, execute the <code>java -version</code> command to view the Java version.</div>


<span id="ZBVbngxq"></span>
## **SDK download address**

DTS includes 2 Java SDKs. Refer to [Java SDK 1](https://github.com/volcengine/volcengine-java-sdk/tree/master/volcengine-java-sdk-dts20180101) and [Java SDK 2](https://github.com/volcengine/volcengine-java-sdk/tree/master/volcengine-java-sdk-dts) for their source addresses.

<span id="VplZzACH"></span>
## **Install SDK**

Configure Maven project dependencies. Create a new Maven project and add the following settings in `pom.xml` in the project directory to introduce service dependencies. When a dependency is introduced, the Maven project management tool automatically downloads the relevant JAR package.

```XML
<dependency>
    <groupId>com.volcengine</groupId>
    <artifactId>volcengine-java-sdk-dts</artifactId>
    <version>0.2.54</version>
</dependency>
<dependency>
    <groupId>com.volcengine</groupId>
    <artifactId>volcengine-java-sdk-dts20180101</artifactId>
    <version>0.2.54</version>
</dependency>
```


If your Java JDK version is JDK 9 or later and you need to add additional `javax.annotation-api` dependencies, add the following in `pom.xml`.

```XML
<dependency> 
  <groupId>javax.annotation</groupId>  
  <artifactId>javax.annotation-api</artifactId>  
  <version>1.3.2</version>
</dependency>
```


&nbsp;
