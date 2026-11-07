---
title: "Java SDK"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/java-sdk"
---

This topic introduces how to install and configure Vital Kubernetes Engine (VKE) SDK for Java and demonstrates how to use it to call cloud APIs.

<span id="使用说明"></span>
## Usage notes


* Only Java JDK 1.7 and later are supported. To download the latest version, go to the [Java official website](https://www.oracle.com/java/technologies/downloads/).

* If you use Java 9 or later, `javax.annotation-api` is required.

   In Java 9 or later, `javax.annotation-api` is removed. Therefore, you must add the following dependency to the project file.

   ```xml
   <dependency>
       <groupId>javax.annotation</groupId>
       <artifactId>javax.annotation-api</artifactId>
       <version>1.3.2</version>
   </dependency>
   ```
   


<span id="安装配置"></span>
## Installation settings

It is recommended to manage and use the Java SDK through Maven.


1. Build your project locally using Maven.

2. Add dependencies for the Maven project.

   The ByteDance Maven repository is needed to add dependencies. Edit `conf/setting.xml` in the installation directory of Maven to add the image configuration.

   ```xml
   <mirror>
        <id>bytedanceMaven</id>
        <mirrorOf>my-repo-id</mirrorOf>
        <name>ByteDance Maven repository</name>
        <url>https://artifact.bytedance.com/repository/releases/</url>
   </mirror>
   ```
   

3. Import and configure the pom.xml file.

   ```xml
   <dependencyManagement>
     <dependencies>
       <dependency>
         <groupId>com.volcengine</groupId>
             <artifactId>volcengine-java-sdk-bom</artifactId>
           <version>0.1.6</version>
             <type>pom</type>
         <scope>import</scope>
       </dependency>
     </dependencies>
   </dependencyManagement>
   ```
   

4. Use the SDK Maven module.

   ```xml
   <dependency>
       <groupId>com.volcengine</groupId>
       <artifactId>volcengine-java-sdk-cr</artifactId>
       <version>1.0.75</version>
   </dependency>
   ```
   


<span id="证书配置"></span>
## Certificate settings

For VKE, you can configure a certificate in one of the following two ways:


* Importing it through environment variables

   ```shell
   export VOLCENGINE_ACCESS_KEY=your_ak // Your AccessKey ID
   export VOLCENGINE_SECRET_KEY=your_sk // Your AccessKey secret
   ```
   

* Introducing it in code

   ```shell
   Credentials credentials = Credentials.getCredentials(ak,sk);
   ```
   


<span id="sdk-示例"></span>
## Code sample for using the SDK

This topic uses [ListRegistries](https://docs.byteplus.com/en/docs/cr/listregistries) as an example.

```java
package com.volcengine.cr;

import com.volcengine.ApiClient;
import com.volcengine.ApiException;
import com.volcengine.cr.model.FilterForListRegistriesInput;
import com.volcengine.cr.model.ListRegistriesRequest;
import com.volcengine.cr.model.ListRegistriesResponse;
import com.volcengine.cr.model.StatusForListRegistriesInput;
import com.volcengine.sign.Credentials;

public class test {
    public static void main(String[] args) {
        String ak = "AKLT****"; // Your AccessKey ID
        String sk = "WTJG****";// Your AccessKey secret
        String region = "ap-southeast-1";// The Region where your business resides

        ApiClient apiClient = new ApiClient()
                .setCredentials(Credentials.getCredentials(ak, sk))
                .setRegion(region);
        CrApi crApi = new CrApi(apiClient);

        StatusForListRegistriesInput statusListRregistries = new StatusForListRegistriesInput();
        statusListRregistries.setCondition("Ok");
        statusListRregistries.setPhase("Running");

        ListRegistriesRequest listRegistries = new ListRegistriesRequest();
        listRegistries.setPageNumber((long) 1);
        listRegistries.setPageSize((long) 10);

        // Test case 1: names_null_types_all_status_exist
        FilterForListRegistriesInput filterListRregistries = new FilterForListRegistriesInput();
        filterListRregistries.addTypesItem("Basic");
        filterListRregistries.addTypesItem("Enterprise");
        filterListRregistries.addStatusesItem(statusListRregistries);
        listRegistries.setFilter(filterListRregistries);
        try {
            ListRegistriesResponse respListRegistries = crApi.listRegistries(listRegistries);
            System.out.println(listRegistries);
            System.out.println(respListRegistries);
        } catch (ApiException e) {
            System.out.println(e.getResponseBody());
        }
    }
}
```
