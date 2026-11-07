---
title: "Client initialization"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/Initialize_the_client"
---

The SQL Server Python client provides a series of interfaces for interacting with the SQL Server service to manage SQL Server database resources. You need to initialize the SQL Server Python client before sending HTTP/HTTPS requests to the SQL Server service. This topic describes how to initialize the SQL Server Python client.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A BytePlus account has been registered and completed verification. For the detailed method, refer to [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* As per the regulations in the Chinese mainland, you must have completed real name registration before you can activate and use cloud services on nodes in the Chinese mainland through BytePlus.  For more details, refer to [Real name registration](https://docs.byteplus.com/en/docs/byteplus-platform/docs-real-name-registration).

* You have obtained the Access Key ID (AK) and Secret Access Key (SK) for your account. For details, see [Managing an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey).

* You have obtained the Regions supported by RDS for SQL Server. For more information, see [Service address](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/request-structure#service-address).

* You have downloaded and installed the Python SDK for RDS for SQL Server. For detailed steps, see [Download and installation](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/Download_and_install).


<span id=".5Yid5aeL5YyW5a6i5oi356uv"></span>
## Initialize the client

Use the following code to initialize the client.

```Python
import byteplussdkcore
import byteplussdkrdsmssql
from byteplussdkcore.rest import ApiException

if __name__ == "__main__":
    config = byteplussdkcore.Configuration()
    config.ak = "Your AK"
    config.sk = "Your SK"
    config.region = "Your Region"
    try:
        mssql_api = byteplussdkrdsmssql.RDSMSSQLApi(byteplussdkcore.ApiClient(config))
    except ApiException as e:
        print("Exception: %s\n" % e)
```
