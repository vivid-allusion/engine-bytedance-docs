---
title: "Initializing client"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Initializing_client_java"
---

This article describes how to initialize a Java client.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A BytePlus account has been registered. For account registration, refer to [How to Register an Account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* The Access Key ID (AK) and Secret Access Key (SK) information of the account have been obtained. 

* The Regions supported by NDB for MySQL have been obtained. For more information, refer to [Service endpoints](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Request_structure#.5pyN5Yqh5Zyw5Z2A).

* The NDB for MySQL Java SDK has been downloaded and installed. For the specific procedure, refer to [Downloading and installing SDK](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Download_and_installation_java).


<span id=".5Yid5aeL5YyW5a6i5oi356uv"></span>
## Initializing client

Initialize the client with the following code.

```java
import com.byteplus.ApiClient;
import com.byteplus.ApiException;
import com.byteplus.sign.Credentials;

public class VedbmApiObj {
    private VedbmApi VeDBMClient;

    public void initClient() {
        String ak = "your ak";
        String sk = "your sk";
        String region = "your region";
        String host = "service host";

        Credentials credentials = Credentials.getCredentials(ak, sk);

        ApiClient client = new ApiClient()
                .setCredentials(credentials)
                .setRegion(region)
                .setEndpoint(host);

        VeDBMClient = new VedbmApi(client);
    }
}
```
