---
title: "Client initialization"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/client_initialization_2"
---

The MySQL Python client provides a series of APIs to interact with MySQL services and manage MySQL database resources. You need to initialize the MySQL Python client before you can send HTTP/HTTPS requests to the MySQL service. This topic describes how to initialize the MySQL Python client.

<span id="prerequisites"></span>
## **Prerequisites**


* A Volcano Engine account has been registered with real name authentication completed.For detailed instructions, please refer to [How to Register an Account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account) and [Real-name authentication](https://docs.byteplus.com/en/docs/byteplus-platform/docs-real-name-registration).

* The Access Key ID (AK) and Secret Access Key (SK) information of the account has been obtained. For specific operations, refer to [Managing Access Keys](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-keys).

* The regions supported by RDS for MySQL have been obtained. Refer to [Endpoints](https://docs.byteplus.com/en/docs/RDS_for_MySQL/request_structure_1#.6YCa5L-h5Y2P6K6u).

* The Python SDK of RDS for MySQL has been downloaded and installed. For specific operation steps, refer to [Download and installation](https://docs.byteplus.com/en/docs/RDS_for_MySQL/download_and_installation_2).


<span id="initializing-the-client"></span>
## **Initializing the Client**

Initialize the client with the following code.

```python
import  volcenginesdkrdsmysqlv2
import  volcenginesdkcore
from  volcenginesdkcore.rest  import  ApiException

if __name__ == "__main__":
    configuration = volcenginesdkcore.Configuration()
    # Set AKSK verification information and region.
    configuration.ak = "Your AK"
    configuration.sk = "Your SK"
    configuration.region = "Your Region"
    try:
        # Create an RDS MySQL SDK client, through which APIs can be called
        api_instance = volcenginesdkrdsmysqlv2.RDSMYSQLV2Api(volcenginesdkcore.ApiClient(configuration))
    except ApiException as e:
        print("Exception: %s\n" % e)
```


&nbsp;
