---
title: "Develop a custom CredentialProvider"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Develop_a_custom_CredentialProvider"
---

To meet complex security and compliance requirements that cannot be satisfied by your current default AK/SK configuration (such as integration with enterprise IAM systems or dynamic token acquisition), you can integrate with the storage service by developing a custom Provider. This document describes the procedure and key configuration points for developing a custom CredentialProvider.

<span id="5883f83b"></span>
# Key operation points

<span id="4796bd0b"></span>
## Environment preparation: Add Proton dependency


1. Obtain the SDK: Go to the [official website](https://www.volcengine.com/docs/6491/149822?lang=zh) to download Proton version 2.3.13.

2. Local import: Manually add the Jar package to the project's `lib` directory or install it into your local Maven private repository.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Set the dependency scope to <code><scope>provided</scope></code> in <code>pom.xml</code>. This is to prevent Proton from being included in the final custom Jar package and to avoid class conflicts with Spark at runtime.   </div>
   

<span id="cddfab11"></span>
## Core development: Implement AbstractCredentialsProvider

The following is the implementation of SimpleCredentialsProvider provided by the proton sdk for your reference. It loads ak, sk, and token from the configuration and returns them.

```Java
/* * ByteDance Volcengine EMR, Copyright 2022. * * Licensed under the Apache License, Version 2.0 (the "License"); * you may not use this file except in compliance with the License. * You may obtain a copy of the License at * *     http://www.apache.org/licenses/LICENSE-2.0 * * Unless required by applicable law or agreed to in writing, software * distributed under the License is distributed on an "AS IS" BASIS, * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. * See the License for the specific language governing permissions and * limitations under the License. */

package io.proton.common.object.auth;

import io.proton.shaded.org.apache.commons.lang3.StringUtils;

import static io.proton.common.conf.ConfKeys.OBJECT_ACCESS_KEY_ID;
import static io.proton.common.conf.ConfKeys.OBJECT_BUCKET_ACCESS_KEY_ID;
import static io.proton.common.conf.ConfKeys.OBJECT_BUCKET_SECRET_ACCESS_KEY;
import static io.proton.common.conf.ConfKeys.OBJECT_BUCKET_SESSION_TOKEN;
import static io.proton.common.conf.ConfKeys.OBJECT_SECRET_ACCESS_KEY;
import static io.proton.common.conf.ConfKeys.OBJECT_SESSION_TOKEN;

public class SimpleCredentialsProvider extends AbstractCredentialsProvider {
  public static final String NAME = SimpleCredentialsProvider.class.getName();

  @Override
  protected ExpirableCredential createCredential() {
    String accessKey = conf().getOr(
        OBJECT_BUCKET_ACCESS_KEY_ID.format(scheme(), bucket()),
        OBJECT_ACCESS_KEY_ID.format(scheme()));
    String secretKey = conf().getOr(
        OBJECT_BUCKET_SECRET_ACCESS_KEY.format(scheme(), bucket()),
        OBJECT_SECRET_ACCESS_KEY.format(scheme()));
    String sessionToken = conf().getOr(
        OBJECT_BUCKET_SESSION_TOKEN.format(scheme(), bucket()),
        OBJECT_SESSION_TOKEN.format(scheme()));

    // Example of obtaining custom configuration: if you need to read business-specific configuration
    // String myConf = conf().get(ConfKey.stringType().key("custom.iam.url").build());
    
    if (StringUtils.isEmpty(sessionToken)) {
      // This is a static ak sk configuration.
      return new ExpirableCredential(accessKey, secretKey);
    } else {
      // For scenarios such as AssumeRole, you can set the expiration time (set to never expire here)
      return new ExpirableCredential(accessKey, secretKey, sessionToken, Long.MAX_VALUE);
    }
  }
}
```


<span id="d103dffd"></span>
# Application example

After completing the preparation of the core development section above, you can compile and package, then deploy to the cluster. The following is an example of using a custom CredentialProvider with ECS Spark.

<span id="d3996115"></span>
## Packaging and cluster deployment

<span id="95f81bba"></span>
### Compilation and packaging specifications


* **Tool selection**: It is recommended to use Maven or Gradle.

*  **⚠️ Prohibited practices**: **Do not include the Proton Jar package in a "thin jar"** . If you use `maven-shade-plugin`, be sure to exclude Proton\-related dependencies. Otherwise, this can easily cause `ObjectStorageException` or class initialization failures.


<span id="a6e6fe53"></span>
### Jar package distribution


* **Recommended path**: Upload the Jar to a dedicated path on the compute node (such as `/usr/lib/emr/custom_auth/`). Avoid placing custom Jars in system component directories to prevent contaminating existing components.

* **Automated configuration \- bootstrap script**:

   * **Existing nodes**: Manually distribute via cluster scripts.

   * **New nodes**: Configure a **bootstrap script (Bootstrap Action)**  to ensure that new nodes can automatically synchronize the Jar package when the cluster is scaled out.

* **Automated configuration \- vePFS mount**: If **vePFS** is mounted, it is recommended to place the Jar directly in the vePFS shared directory for global availability.


<span id="33cd8c48"></span>
## Spark parameter configuration

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To reduce the impact on the global environment, it is recommended to inject the following parameters at the <strong>job level</strong>:</div>


<span id="2c3f8a83"></span>
### Inject into the ClassPath

Ensure that both the Driver and Executor can load your custom Jar:

```Bash
spark.driver.extraClassPath=/path1/*:/path2/*:/{自定义jar路径}/*
spark.executor.extraClassPath=/path1/*:/path2/*:/{自定义jar路径}/*
```


<span id="26db8fde"></span>
### Enable Provider (choose one of two options)


|Method |Configuration parameters |Use cases |
|---|---|---|
|Method 1: Chained fallback (recommended) |```Shell```<br>```spark.hadoop.fs.tos.credentials.provider=io.proton.common.object.tos.auth.DefaultCredentialsProviderChain```<br>```spark.hadoop.fs.tos.credential.provider.custom.classes={自定义CredentialProvider},io.proton.common.object.tos.auth.SimpleCredentialsProvider,io.proton.common.object.tos.auth.FileCredentialsProvider```<br> |**Safer**.<br><br>**Fallback logic**: **When createCredential() of your custom Provider throws an exception, the next provider's createCredential() will be called in sequence** |
|Method 2: Direct specification |```Shell```<br>```spark.hadoop.fs.tos.credentials.provider={自定义CredentialProvider}```<br>```spark.hadoop.{自定义配置1}=xxx```<br>```spark.hadoop.{自定义配置2}=xxx```<br> |**Certain risks** exist, and you need to handle legacy compatibility logic yourself to **avoid upgrade impacts on existing jobs**. |
