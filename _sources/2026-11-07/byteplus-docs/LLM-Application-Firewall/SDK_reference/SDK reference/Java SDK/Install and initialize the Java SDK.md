---
title: "Install and initialize the Java SDK"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Java_installation_and_initialization"
---

The LLM Application Firewall Java SDK allows you to integrate your Java applications with our security service, which protects Large Language Model (LLM) applications from prompt injection, data leakage, and other threats. You should use this SDK when developing a Java\-based application that requires programmatic security checks for its LLM interactions. This document will guide you through the process of downloading, installing, and initializing the SDK for your project.

<span id="3b8e665d"></span>
## Prerequisites


* Obtain the Access Key ID (AK) and Secret Access Key (SK). You have two options:

   * Go to [BytePlus IAM > Access key management](https://console.byteplus.com/iam/keymanage) to find your existing access key pair.

   * Create a RAM user and generate a new AccessKey pair. For details, refer to [Create a user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user).

* In the LLM Application Firewall console, add an asset and configure its protection policies. For details, refer to [Introduction to protection policies](https://docs.byteplus.com/docs/LLM-Application-Firewall/introduction_to_protection_policy).


&nbsp;

<span id="a22a5439"></span>
## Environmental requirements

JDK 1.8 or later versions required.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">Run <code>java -version</code> to check the current Java version.</div>


<span id="801fb1db"></span>
## Important notes

Starting from Java 9 and later versions, `javax.annotation-api` is no longer included as a default component of the JDK. To ensure the program runs properly when using Java 9 or a later version, you need to manually add this dependency.

```XML
<dependency>
    <groupId>javax.annotation</groupId>
    <artifactId>javax.annotation-api</artifactId>
    <version>1.3.2</version>
</dependency>
```


<span id="5a9f24ec"></span>
## Download the SDK

<span id="e74ee148"></span>
### Download the SDK for the current product


1. Create a Maven project.

2. In the `pom.xml` file in the project directory, add the following settings to add the SDK dependency for this product.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After introducing dependencies, the Maven project management tool will automatically download the relevant JAR files.   </div>
   

   ```XML
   <dependency>
     <groupId>com.byteplus</groupId>
     <artifactId>byteplus-java-sdk-v2-llmshield</artifactId>
     <version>0.1.63</version>
   </dependency>
   ```
   


<span id="d2e52490"></span>
### Download SDKs for all products

To introduce all cloud product SDKs already supported by BytePlus, use the BOM method. As shown below, after including `byteplus-java-sdk-v2-bom`, you can then include all supported services.

```XML
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>com.byteplus</groupId>
      <artifactId>byteplus-java-sdk-v2-bom</artifactId>
      <version>0.1.63</version>
      <type>pom</type>
      <scope>import</scope>
    </dependency>
  </dependencies>
</dependencyManagement>
```


<span id="a42eda70"></span>
## Initialization

The following describes the initialization parameters and the corresponding sample code.

<span id="b31f8992"></span>
### Parameter description


|Parameter |Example |Description |
|---|---|---|
|myUrl |https://ap\-southeast\-1.sdk.access\-bp.llm\-shield.omni\-shield.ai<br><br> |* **Parameter description**: The endpoint for the LLM Application Firewall service has the format **`https://`**  **`{region}`**  **`.sdk.access-bp.llm-shield.omni-shield.ai`**, where {region} is the region of your provisioned instance.<br><br>   * ap\-southeast\-1<br><br>   * cn\-hongkong<br><br>* **Finding this value**: You can find the region in the instance management module of the LLM Application Firewall console. |
|ak, sk |* AK : AKLTYWRhNDMw\*\*\*\*<br><br>* SK: TWprNE5XVXlZbc\*\*\*\* |These are the **Access Key ID** and **Secret Access Key** for your BytePlus account. |
|appid |app\-d35p9du8pa51\*\*\*\* |* **Parameter description**: The unique identifier of the asset. After you add an asset in the console, the system automatically generates an AppID.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Caution   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When making SDK calls, only assets integrated via the SDK method are supported.   </div><br>   <br><br>* **Finding this value**: Go to the asset management module in the LLM Application Firewall console to view the AppIDs of assets integrated via SDK. |
|region |ap\-southeast\-1 |* **Parameter description**: This is the region of your LLM Application Firewall instance. It must match the region specified in `myUrl`.<br><br>   * ap\-southeast\-1<br><br>   * cn\-hongkong<br><br>* **Finding this value**: Go to the LLM Application Firewall console instance management module to view the region where the instance is located. |


&nbsp;

&nbsp;

<span id="0f14b268"></span>
### Sample code

The following example shows the complete initialization code:

```Java
package com.demo;
import com.byteplus.llmshield.*;

public class Moderate {
    public static void main(String[] args) {
        // Replace the parameters with the actual values
        String myUrl = "https://ap-southeast-1.sdk.access-bp.llm-shield.omni-shield.ai";  // Endpoint of your LLM Application Firewall instance
        String ak = "YOUR AK";  // Access Key of your BytePlus account
        String sk = "YOUR SK";  // Secret Key of your BytePlus account
        String region = "ap-southeast-1";  // Region of the LLM Application Firewall instance
        String myAppID = "app-d45gff4r7odm2ols****"; // AppId of your asset
        long timeout = 5000; // Timeout (milliseconds)
        ApiClient client = ApiClient.New(myUrl, ak,sk,region, timeout);
```
