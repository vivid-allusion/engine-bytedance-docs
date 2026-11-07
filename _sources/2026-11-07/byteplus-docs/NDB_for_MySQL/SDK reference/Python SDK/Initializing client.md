---
title: "Initializing client"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Initializing_client_python"
---

The NDB for MySQL Python client provides a series of interfaces to interact with the NDB for MySQL service and manage NDB for MySQL database resources. You need to initialize the Python client side before you can send HTTP/HTTPS requests to the NDB for MySQL service. This article describes how to initialize the NDB for MySQL Python client.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A BytePlus account has been registered. For account registration, refer to [How to Register an Account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* The Access Key ID (AK) and Secret Access Key (SK) information of the account have been obtained. 

* The Regions supported by NDB for MySQL have been obtained. For more information, refer to [Service endpoints](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Request_structure#.5pyN5Yqh5Zyw5Z2A).

* The NDB for MySQL Python SDK has been downloaded and installed. For the specific procedure, refer to [Downloading and installing SDK](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Downloading_and_installing_SDK_python).


<span id=".5Yid5aeL5YyW5a6i5oi356uv"></span>
## Initializing client

Initialize the client with the following code.

```python
import byteplussdkcore
import byteplussdkvedbm
from byteplussdkvedbm import VEDBMApi

def init_client():
    configuration = byteplussdkcore.Configuration()

    configuration.client_side_validation = True
    configuration.schema = "https"
    configuration.debug = False
    configuration.logger_file = "sdk.log"

    configuration.region = "your region"
    configuration.ak = "your ak"
    configuration.sk = "your sk"
    configuration.host = "service host"

    byteplussdkcore.Configuration.set_default(configuration)

    return VEDBMApi(byteplussdkcore.ApiClient(configuration))
```
