---
title: "Initializing the client"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Initializing_the_client"
---

This article describes how to initialize a Java client.

<span id="JqvZHWzH"></span>
## Prerequisites


* Access Key ID (AK) and Secret Access Key (SK) of the account have been obtained. For how to obtain them, refer to [view AK and SK information](https://docs.byteplus.com/en/docs/byteplus-platform/reference-access-key).

* Region information supported by the data transmission service (DTS) has been obtained. For details, refer to [service address](https://docs.byteplus.com/en/docs/DTS/request_structure#.5pyN5Yqh5Zyw5Z2A).

* The data transmission service (DTS) Java SDK has been downloaded and installed. For specific steps, refer to [Downloading and Installing](https://docs.byteplus.com/en/docs/DTS/downloading_and_instaling_the_sdk).


<span id="Z5no02AS"></span>
## Initialize client

Initialize the client with the following code.

```JavaScript
import com.volcengine.ApiClient;
import com.volcengine.sign.Credentials;

public class DtsApiTest {
    DtsApi dtsApi;
    JSON jsonUtil;
    private String taskId = "test_can_be_ignored";
    @Before
    public void init() {
        String AK = "xxxxxxx";
        String SK = "xxxxxxx==";
        ApiClient apiClient = new ApiClient();
        apiClient.setEndpoint("dts.cn-beijing.byteplusapi.com.cn");
        apiClient.setRegion("cn-beijing");
        apiClient.setCredentials(Credentials.getCredentials(AK, SK));
        dtsApi = new DtsApi(apiClient);
        jsonUtil = new JSON();
    }
}
```
