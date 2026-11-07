---
title: "Initializing client"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/client-initialization-python"
---

The MongoDB Python client provides a series of APIs to interact with MongoDB services and manage MongoDB database resources. You need to initialize the MongoDB Python client before you can send HTTP/HTTPS requests to the MongoDB service. This topic describes how to initialize the MongoDB Python client.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite


* The MongoDB Python SDK has been downloaded and installed. For the specific procedure, refer to [Downloading and installing SDK](https://docs.byteplus.com/en/docs/mongodb/download-install-python-sdk).

* Before initializing the client, ensure that you have obtained the following information:

   * The Access Key ID (AK) and Secret Access Key (SK) of the account. For methods to obtain AKSK information, refer to [Access Key](https://docs.byteplus.com/en/docs/byteplus-platform/reference-access-key).

   * Region information. For regions supported by MongoDB, refer to [Service endpoints](https://docs.byteplus.com/en/docs/mongodb/request-structure#9TeFSOVO).


<span id=".5Yid5aeL5YyW5a6i5oi356uv"></span>
## Initializing the client

Initialize the client with the following code.

```Python
import byteplussdkmongodb
import byteplussdkcore
from pprint import pprint

if __name__ == '__main__':
    configuration = byteplussdkcore.Configuration()
    configuration.ak = "Your AK"
    configuration.sk = "Your SK"
    configuration.region = "Your Region"
     
    # set default configuration
    byteplussdkcore.Configuration.set_default(configuration)

    # use global default configuration
    api_instance = byteplussdkmongodb.MONGODBApi()
```
