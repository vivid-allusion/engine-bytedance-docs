---
title: "SDK Installation and Initialization"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/SDK_Installation_and_Initialization"
---

VikingDB vector database supports database operations through Java SDK. Before using the Java SDK, you need to complete the SDK installation and initialization steps first.

<span id="prerequisites"></span>
# Prerequisites


1. Have completed account registration and service activation through [Register Account and Activate Service](https://www.volcengine.com/docs/84313/1254444).

2. Obtain security credentials. Access Key is a security credential for accessing Volcengine services, consisting of Access Key ID (referred to as AK) and Secret Access Key (referred to as SK). You can log in to the Volcengine Console and go to 【Key Management】 to view the AK/SK of the current account. For more details, please refer to [Access Key Management](https://www.volcengine.com/docs/6291/65568).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5ef0f716976d0e2060797391b516a839.png) </span>


<span id="install-sdk"></span>
# Install SDK

To optimize the permission system, the vector database SDK is divided into **control plane** and **data plane**: the control plane is used to manage collections, indexes, and offline tasks; the data plane is used for data writing, retrieval, and vectorization. The control plane also supports operations from the console, please configure dependencies according to your needs.

<span id="_1-control-plane-dependency-configuration"></span>
## 1. Control Plane Dependency Configuration

```XML
<dependency>
    <groupId>com.volcengine</groupId>
    <artifactId>volcengine-java-sdk-vikingdb</artifactId>
    <version>{version}</version>
    <!-- Recommended to use the latest version -->
    <!-- Version number can be found at https://central.sonatype.com/artifact/com.volcengine/volcengine-java-sdk-vikingdb/versions -->
</dependency>
```


Maven Repository:

[https://central.sonatype.com/artifact/com.volcengine/volcengine-java-sdk-vikingdb/versions](https://central.sonatype.com/artifact/com.volcengine/volcengine-java-sdk-vikingdb/versions)

Source Code:

[https://github.com/volcengine/volcengine-java-sdk/tree/master/volcengine-java-sdk-vikingdb](https://github.com/volcengine/volcengine-java-sdk/tree/master/volcengine-java-sdk-vikingdb)

<span id="_2-data-plane-dependency-configuration"></span>
## 2. Data Plane Dependency Configuration

```XML
<dependency>
    <groupId>com.volcengine</groupId>
    <artifactId>vikingdb-java-sdk</artifactId>
    <version>{version}</version>
    <!-- Recommended to use the latest version -->
    <!-- Version number can be found at https://central.sonatype.com/artifact/com.volcengine/vikingdb-java-sdk/versions -->
</dependency>
```


Maven Repository:

[https://central.sonatype.com/artifact/com.volcengine/vikingdb-java-sdk/versions](https://central.sonatype.com/artifact/com.volcengine/vikingdb-java-sdk/versions)

Source Code:

[https://github.com/volcengine/vikingdb-java-sdk](https://github.com/volcengine/vikingdb-java-sdk)

<span id="initialize-sdk"></span>
# Initialize SDK

For private network connection, refer to [Private Network Connection Method](https://docs.byteplus.com/docs/84313/1254445) to configure and obtain the domain name. Currently, private network connection only supports HTTP protocol.

In the code, `your-access-key` and `your-secret-key` need to be replaced with your AK and SK respectively, and `host`, `region`, `scheme` replaced with the domain name, region, and request protocol (HTTP / HTTPS) you are using.


1. **Data Plane (Data / Search / Embedding)** 



|**Region Name** |**Region ID** |Internet Domain Name (Public Network) |Private Network Connection Endpoint Service (**Not a domain name**, please refer to the [Private Network Connection](https://docs.byteplus.com/en/docs/VikingDB/APIV2Upgrade) documentation) |
|---|---|---|---|
|Asia Pacific (Johor) |ap\-southeast\-1 |[api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com](http://api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com/) |[com.bytepluses.privatelink.ap-southeast-1.vikingdb-ann](https://docs.byteplus.com/en/docs/198/com.bytepluses.privatelink.ap-southeast-1.vikingdb-ann) |


```Java
import com.volcengine.vikingdb.runtime.core.auth.AuthWithAkSk;
import com.volcengine.vikingdb.runtime.core.ClientConfig;
import com.volcengine.vikingdb.runtime.enums.Scheme;
import com.volcengine.vikingdb.runtime.vector.service.VectorService;

import java.util.Properties;

public class VikingDBQuickStart {

    public static void main(String[] args) throws Exception {
        String host = "api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com";
        String region = "ap-southeast-1";
        String accessKey = "your-access-key";
        String secretKey = "your-secret-key";

        // Initialize client
        VectorService vectorService = new VectorService(
                Scheme.HTTPS,
                host,
                region,
                new AuthWithAkSk(accessKey, secretKey),
                ClientConfig.builder().build()
        );

        System.out.println("VikingDB client initialized successfully.");

        // Subsequent operations...
    }
}
```



2. **Control Plane (Collection / Index / Task)** 



|**Region Name** |**Region ID** |Internet Domain Name (Public Network) |Private Network Connection Endpoint Service (**Not a domain name**, please refer to the [Private Network Connection](https://docs.byteplus.com/en/docs/VikingDB/APIV2Upgrade) documentation) |
|---|---|---|---|
|Asia Pacific (Johor) |ap\-southeast\-1 |[vikingdb.ap-southeast-1.byteplusapi.com](http://vikingdb.ap-southeast-1.byteplusapi.com/) |com.bytepluses.privatelink.ap\-southeast\-1.api.vikingdb |


```Java
import com.volcengine.ApiClient;
import com.volcengine.sign.Credentials;
import com.volcengine.vikingdb.VikingdbApi;

public class QuickStart {
    public static void main(String[] args) {
        String ak = "your-access-key"; // Replace with your AK
        String sk = "your-secret-key"; // Replace with your SK
        String endpoint = "vikingdb.ap-southeast-1.byteplusapi.com"; // Enter your control plane service domain name
        String region = "ap-southeast-1"; // Enter your service region

        ApiClient apiClient = new ApiClient()
                .setEndpoint(endpoint)
                .setCredentials(Credentials.getCredentials(ak, sk))
                .setRegion(region);

        VikingdbApi api = new VikingdbApi(apiClient);

        // You can now use the 'api' object to call VikingDB API
        // ......
    }
}
```
