---
title: "Code examples"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/Code_examples"
---

The code examples for the Python SDK of RDS for SQL Server in this topic are for reference only.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have downloaded and installed the SDK. For detailed instructions, see [Download and installation](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/Download_and_install).

* You have initialized the client. For detailed instructions, see [Client initialization](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/Initialize_the_client).


<span id=".6K-35rGC6LaF5pe25pe26Ze06K6-572u"></span>
## **Set the request timeout**

When calling the SQL Server interface using the SDK, there is no default timeout setting. You can add the `_request_timeout` parameter at the end of your code when initiating an API request to specify the request timeout period (in seconds). If the request is not completed within that time, it will be immediately terminated and return a timeout error. For example, when calling the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstances) interface, you can set the timeout to `10` seconds using the following code:

```Python
response = mssql_api.describe_db_instances(byteplussdkrdsmssql.DescribeDBInstancesRequest(
    _configuration=config,
), _request_timeout=10)
```


<span id=".5Yib5bu6LXNxbC1zZXJ2ZXIt5a6e5L6L"></span>
## **Create a SQL Server instance**

For information about the parameters in the following SDK code, such as their definitions and value ranges, see [CreateDBInstance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/createdbInstance).

```Python
from pprint import pprint
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
        response = mssql_api.create_db_instance(byteplussdkrdsmssql.CreateDBInstanceRequest(
            db_engine_version="SQLServer_2019_Std",
            instance_type="HA",
            zone_id="cn-shanghai-a",
            node_spec="rds.mssql.3il.s2.medium.s2",
            storage_space=30,
            vpc_id = "vpc-22j7ap46unq4g7r2qr2******",
            subnet_id = "subnet-3qdpntaawf0u87prml0******",
            super_account_password="******",
            db_time_zone="China Standard Time",
            server_collation="Chinese_PRC_CI_AS",
            charge_info=byteplussdkrdsmssql.ChargeInfoForCreateDBInstanceInput(
            charge_type="PostPaid",
            auto_renew=False,
            ),
            _configuration=config,
        ), _request_timeout=10)
        pprint(response)
    except ApiException as e:
        print("Exception: %s\n" % e)
```


<span id=".5p-l6K-iLXNxbC1zZXJ2ZXIt5a6e5L6L5L-h5oGv"></span>
## **Query SQL Server instance information**

For information about the parameters in the following SDK code, such as their definitions and value ranges, see [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstances).

```Python
from pprint import pprint
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
        response = mssql_api.describe_db_instances(byteplussdkrdsmssql.DescribeDBInstancesRequest(
            page_size=10,
            page_number=1,
            _configuration=config,
        ), _request_timeout=10)
        pprint(response)
    except ApiException as e:
        print("Exception: %s\n" % e)
```
