---
title: "Client initialization"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/client_initialization_4"
---

This topic describes how to initialize the Java client.

<span id="prerequisites"></span>
## Prerequisites


* A Volcano Engine account has been registered with real name authentication completed.For detailed instructions, please refer to [How to Register an Account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account) and [Real-name authentication](https://docs.byteplus.com/en/docs/byteplus-platform/docs-real-name-registration).

* The Access Key ID (AK) and Secret Access Key (SK) information of the account has been obtained. For specific operations, refer to [Managing Access Keys](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-keys).

* The regions supported by RDS for MySQL have been obtained. Refer to [Endpoints](https://docs.byteplus.com/en/docs/RDS_for_MySQL/request_structure_1#.6YCa5L-h5Y2P6K6u).

* The Go SDK of RDS for MySQL has been downloaded and installed. For specific operation steps, refer to [Download and installation](https://docs.byteplus.com/en/docs/RDS_for_MySQL/download_and_installation_4).


<span id="client-initialization"></span>
## Client Initialization

Initialize the client with the following code.

```java
package  org.example;
import  com.volcengine.*;
import  com.volcengine.rdsmysqlv2.RdsMysqlV2Api;
import  com.volcengine.rdsmysqlv2.model.DescribeDBInstanceDetailRequest;
import  com.volcengine.rdsmysqlv2.model.DescribeDBInstanceDetailResponse;
import  com.volcengine.sign.Credentials;
public class Main  {
    // Set AKSK verification information and region.
    public static String ak = "Your AK";
    public static String sk = "Your SK";
    public static String region = "Your Region";
    // Create a MySQL SDK client, which can be used to call the API to perform task requests later.
    public static ApiClient apiClient = new ApiClient()
                        .setCredentials(Credentials.getCredentials(ak,sk))
                        .setRegion(region);
    public static RdsMysqlV2Api rdsmysqlv2api = new RdsMysqlV2Api(apiClient);
}
```


&nbsp;
