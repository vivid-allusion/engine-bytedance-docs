---
title: "Download and Installation"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/Download_and_Installation"
---

This topic describes how to download and install the Java SDK for RDS for SQL Server.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**

Java JDK 1.8.0_131 or a higher version is installed. For more information, see [Java Downloads](https://www.oracle.com/java/technologies/downloads/).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Run the <code>java -version</code> command to check your current Java version.</div>


<span id=".c2RrLeS4i-i9veWcsOWdgA=="></span>
## **SDK Download Address**

For the source code of the SQL Server Java SDK, see [SQL Server Java SDK](https://github.com/byteplus-sdk/byteplus-java-sdk-v2/tree/main/byteplus-java-sdk-v2-rdsmssql).

<span id=".5a6J6KOFLXNkaw=="></span>
## **Install the SDK**

Configure Maven project dependencies. Create a new Maven project and add the following settings to the `pom.xml` file in the project directory to add the service dependencies. After you add the dependencies, the Maven project management tool automatically downloads the related JAR packages.

```Java
 <dependency>
     <groupId>com.byteplus</groupId>
     <artifactId>byteplus-java-sdk-v2-rdsmssql</artifactId>
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
