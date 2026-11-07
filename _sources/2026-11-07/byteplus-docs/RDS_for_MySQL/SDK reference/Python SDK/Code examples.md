---
title: "Code examples"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/code_examples_2"
---

The sample code for the Java SDK of RDS for MySQL provided here is only for reference.

<span id="prerequisites"></span>
## **Prerequisites**


* of the SDK has been completed.

* [Client initialization](https://docs.byteplus.com/en/docs/RDS_for_MySQL/client_initialization_2) has been completed.


<span id="set-the-established-timeout-for-requests"></span>
## **Set the established timeout for requests**

There is no established timeout by default when calling the MySQL API with the SDK. When you initiate the API call request, add the `_request_timeout` parameter to specify the request timeout (in seconds) at the end of the code. If the request is not completed within this time, it will be terminated with an error reported. For example, you can call [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances) to set the request established timeout of the client to 10 seconds.

```python
resp = api_instance.describe_db_instance(volcenginesdkrdsmysqlv2.DescribeDBInstanceRequest(
    instance_id="mysql-",
    _configuration=configuration,
), _request_timeout=10)
python
```


<span id="create-a-mysql-instance"></span>
## \*\*Create a \*\* **MySQL** **instance**

For the definitions, value ranges, and other information of parameters used in the following SDK code, refer to [CreateDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdbinstance1).

```python
from  pprint  import  pprint

import volcenginesdkrdsmysqlv2

import volcenginesdkcore

from volcenginesdkcore.rest import ApiException

if  __name__ ==  "__main__":
        configuration = volcenginesdkcore.Configuration()
        configuration.ak =  "Your AK"
        configuration.sk =  "Your SK"
        configuration.region =  "Your Region"
    try:
        api_instance = volcenginesdkrdsmysqlv2.RDSMYSQLV2Api(volcenginesdkcore.ApiClient(configuration))
        resp = api_instance.create_db_instance(volcenginesdkrdsmysqlv2.CreateDBInstanceRequest(
            db_engine_version="MySQL_5_7",
            node_info=[
                {
                    "NodeType": "Primary",
                    "ZoneId": "cn-beijinga",
                    "NodeSpec": "rds.mysql.1c2g",
                },
                {
                    "NodeType": "Secondary",
                    "ZoneId": "cn-beijinga",
                    "NodeSpec": "rds.mysql.1c2g",
                },
            ],
            storage_type="LocalSSD",
            storage_space=100,
            vpc_id="vpc-****",
            subnet_id="subnet-****",
            charge_info={
                "ChargeType": "PostPaid"
            },
            _configuration=configuration,
        ))
        pprint(resp)
    except  ApiException  as  e:
        print("Exception: %s\n"  % e)
```


The parameters in this example are described in the following table.


|**Configuration Item** |**Description** |**Value** |
|---|---|---|
|DBEngineVersion |Instance name. |Your Instance Name |
|NodeInfo |Instance specification configuration. |[<br><br>{<br><br>"NodeType": "Primary",<br><br>"ZoneId": "cn\-beijinga",<br><br>"NodeSpec": "rds.mysql.1c2g"<br><br>},<br><br>{<br><br>"NodeType": "Secondary",<br><br>"ZoneId": "cn\-beijinga",<br><br>"NodeSpec": "rds.mysql.1c2g"<br><br>},<br><br>{<br><br>"NodeType": "ReadOnly",<br><br>"ZoneId": "cn\-beijinga",<br><br>"NodeSpec": "rds.mysql.1c2g"<br><br>}<br><br>] |
|StorageType |Instance storage type. |LocalSSD |
|StorageSpace |Instance storage space. |100 |
|VpcId |The Virtual Private Cloud (VPC) ID. |vpc\-\*\*\*\* |
|SubnetId |Subnet ID. |Subnet123456 |
|InstanceName |Instance name. |Your Instance Name |
|SuperAccountName |Privileged account name. |Test1 |
|SuperAccountPassword |Password of privileged account. |Test@123456 |
|LowerCaseTableNames |Whether the table name is case\-sensitive. |1 |
|DBTimeZone |Time zone. |UTC +08:00 |
|DBParamGroupId |Parameter template ID. |ParamGroup123456 |
|ProjectName |Project of the instance. |Test |
|ChargeInfo |Billing method. |{<br><br>"ChargeType": "PostPaid"<br><br>} |
|InstanceTags |Instance tag. |{<br><br>"Key": ""aa,<br><br>"Value":"aa"<br><br>} |
|Number |Number of purchased instances. |1 |


<span id="query-mysql-instance-information"></span>
## Query MySQL instance information

```python
from  pprint  import  pprint

import volcenginesdkrdsmysqlv2

import volcenginesdkcore

from volcenginesdkcore.rest import ApiException

if  __name__ ==  "__main__":
        configuration = volcenginesdkcore.Configuration()
        configuration.ak =  "Your AK"
        configuration.sk =  "Your SK"
        configuration.region =  "Your Region"
        try:
            # Create an RDS MySQL SDK client, through which APIs can be called
            api_instance = volcenginesdkrdsmysqlv2.RDSMYSQLV2Api(volcenginesdkcore.ApiClient(configuration))
            resp = api_instance.describe_db_instance_detail(volcenginesdkrdsmysqlv2.DescribeDBInstanceDetailRequest(
                instance_id="Your InstanceId",
            ))
            print(resp)
        except ApiException as e:
            print("Exception: %s\n" % e)
```
