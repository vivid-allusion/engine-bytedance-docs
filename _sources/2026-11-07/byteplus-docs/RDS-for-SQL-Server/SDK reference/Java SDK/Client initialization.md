---
title: "Client initialization"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/Initialize_a_Client"
---

The SQL Server Java SDK supports initializing a client through a Session. An SQL Server client created through a Session reuses underlying HTTP/HTTPS resources, such as connections and requests. When you need to initialize multiple clients, creating them through a Session can improve performance. This topic describes how to initialize a client through a Session.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**


* A BytePlus account has been registered and completed verification. For the detailed method, refer to [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* As per the regulations in the Chinese mainland, you must have completed real name registration before you can activate and use cloud services on nodes in the Chinese mainland through BytePlus.  For more details, refer to [Real name registration](https://docs.byteplus.com/en/docs/byteplus-platform/docs-real-name-registration).

* You have obtained the Access Key ID (AK) and Secret Access Key (SK) for your account. For details, see [Managing an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey).

* You have obtained the Regions supported by RDS for SQL Server. For more information, see [Service address](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/request-structure#service-address).

* You have downloaded and installed the RDS for SQL Server Java SDK. For detailed steps, see [Download and Installation](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/Download_and_Installation).


<span id=".5Yid5aeL5YyW5a6i5oi356uv"></span>
## **Initialize the client**

Use the following code to initialize the client.

```java
package  org.example;

import  com.byteplus.*;
import  com.byteplus.rdsmssql.RdsmssqlApi;
import  com.byteplus.rdsmssql.model.*;
import  com.byteplus.sign.Credentials;

public class Main  {

    public static String ak = "Your AK";
    public static String sk = "Your SK";
    public static String region = "Your Region";

    public static ApiClient apiClient = new ApiClient()
                        .setCredentials(Credentials.getCredentials(ak,sk))
                        .setRegion(region);
    public static RdsmssqlApi rdsmssqlApi = new RdsmssqlApi(apiClient);

}
```
