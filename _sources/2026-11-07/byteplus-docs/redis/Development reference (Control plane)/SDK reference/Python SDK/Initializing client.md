---
title: "Initializing client"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/client-initialization-python"
---

The Redis Python client provides a series of interfaces to interact with Redis service and manage Redis Database resources. You need to initialize the Redis Python client before you can send HTTP/HTTPS requests to the Redis service. This topic describes how to initialize the Redis Python client.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Downloaded and installed the Redis Python SDK. For specific procedures, refer to [Downloading and installing SDK](https://docs.byteplus.com/en/docs/redis/download-install-python-sdk).

* Before initializing the client, ensure that you have obtained the following information:

   * Access Key ID (AK) and Secret Access Key (SK) for your account. For methods to obtain AKSK information, refer to [Access Key](https://docs.byteplus.com/en/docs/byteplus-platform/reference-access-key).

   * Region information. For the regions supported by Redis, refer to [Service endpoints](https://docs.byteplus.com/en/docs/redis/request-structure#.5pyN5Yqh5Zyw5Z2A).


<span id=".5Yid5aeL5YyW5a6i5oi356uv"></span>
## Initializing client

Use the following code to initialize the client.

```Python
import byteplussdkredis
import byteplussdkcore
from byteplussdkcore.rest import ApiException

if __name__ == "__main__":
    configuration = byteplussdkcore.Configuration()

    # Set access key and secret key verification information and region.
    configuration.ak = "Your AK"
    configuration.sk = "Your SK"
    configuration.region = "Your Region"

    try:
        # Create a Redis SDK client, used to call APIs
        api_instance = byteplussdkredis.REDISApi(byteplussdkcore.ApiClient(configuration))

    except ApiException as e:
        print("Exception: %s\n" % e)
```
