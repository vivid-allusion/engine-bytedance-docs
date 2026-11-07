---
title: "Download and installation"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Java_Download_and_installation"
---

This topic describes how to download and install the Cloud Search Java SDK.

<span id="GlYFORyS"></span>
## **Prerequisites**

You need Java JDK 1.8.0_131 or a later version. For more details, refer to [Java Downloads](https://www.oracle.com/java/technologies/downloads/).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Run the <code>java -version</code> command to check the current Java version.</div>


<span id="IRaDFi8D"></span>
## **SDK download address**

For the source code of the Cloud Search Service Java SDK, refer to [Cloud Search Java SDK](https://github.com/byteplus-sdk/byteplus-java-sdk-v2/tree/main/byteplus-java-sdk-v2-escloud).

<span id="qIg6YCuE"></span>
## **Install the SDK**

Configure Maven project dependencies. Create a new Maven project and add the following settings to the `pom.xml` file in the project directory to import the service dependencies. After the dependencies are imported, the Maven project management tool automatically downloads the relevant JAR packages.

```XML
 <dependency>
     <groupId>com.byteplus</groupId>
     <artifactId>byteplus-java-sdk-v2-escloud</artifactId>
     <version>0.1.29</version>
 </dependency>
 
 <dependency>
     <groupId>com.byteplus</groupId>
     <artifactId>byteplus-java-sdk-v2-core</artifactId>
     <version>0.1.29</version>
 </dependency>
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If your Java JDK version is 9 or later, you also need to add the <code>javax.annotation-api</code> dependency. Add the following content to the <code>pom.xml</code> file.</div>


<div data-tips="true" data-tips-type="tip">```xml
<dependency> 
    <groupId>javax.annotation</groupId> 
    <artifactId>javax.annotation-api</artifactId> 
    <version>1.3.2</version> 
</dependency>
```
</div>
