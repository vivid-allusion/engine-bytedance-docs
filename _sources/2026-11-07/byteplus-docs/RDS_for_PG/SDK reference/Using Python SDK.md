---
title: "Using Python SDK"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/use_python_sdk"
---

This topic describes the download, installation, and client initialization information of the Python SDK for RDS for PostgreSQL.

<span id=".5LiL6L295LiO5a6J6KOF"></span>
## Download and install

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites

Python 2.7 or above is installed.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can run the <code>python --version</code> command to check the current Python version.</div>


<span id=".U0RLIOS4i-i9veWcsOWdgA=="></span>
### SDK download URL

For the source code address of the Python SDK for RDS for PostgreSQL, see the [SDK list](https://docs.byteplus.com/en/docs/RDS_for_PG/sdk_overview).

<span id=".5a6J6KOFIFNESw=="></span>
### Install SDK

You can install the SDK using any of the following methods:


* Run the following command to install the SDK for the specified user.

   ```python
   python setup.py install --<username>
   ```
   

* Run the following command to install the SDK for all users.

   ```python
   sudo python setup.py install
   ```
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the SDK has already been installed, you can upgrade it using the following command.</div>


<div data-tips="true" data-tips-type="tip">```python
pip install byteplus-python-sdk-v2==3.0.10
```
</div>


<span id=".5Yid5aeL5YyW5a6i5oi356uv"></span>
## Initialize client

The PostgreSQL Python client provides a series of interfaces to interact with the PostgreSQL service for managing PostgreSQL database resources. You need to initialize the PostgreSQL Python client before sending HTTP/HTTPS requests to the PostgreSQL service.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites


* A BytePlus account has been registered and completed verification. For the detailed method, refer to [Sign up and verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* The Access Key ID (AK) and Secret Access Key (SK) information of the account have been obtained. For specific operations, refer to [Managing an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey).

* The supported Regions and corresponding Hosts for RDS for PostgreSQL have been retrieved. See [service address](https://docs.byteplus.com/en/docs/RDS_for_PG/request_structure#.5pyN5Yqh5Zyw5Z2A).

* The RDS for PostgreSQL Python SDK has been downloaded and installed. For specific steps, see [Download and Install](https://docs.byteplus.com/en/docs/RDS_for_PG/use_python_sdk#.5LiL6L295LiO5a6J6KOF).


<span id=".5Yid5aeL5YyW5a6i5oi356uv"></span>
### Initialize client

Initialize the client using the following code.

```python
import volcenginesdkcore
import volcenginesdkrdspostgresql as pg
from volcenginesdkcore.rest import ApiException
if __name__ == "__main__":
    configuration = volcenginesdkcore.Configuration()
    # Set AKSK authentication information and Region
    configuration.ak = "Your AK"
    configuration.sk = "Your SK"
    configuration.region = "Your Region"
    configuration.host = "Your Host"
    try:
        # Create PostgreSQL SDK client; all interface calls need to be executed through this client
        api_instance = pg.RDSPOSTGRESQLApi(volcenginesdkcore.ApiClient(configuration))
    except ApiException as e:
        print("Exception: %s\n" % e)
```


<span id=".5Luj56CB56S65L6L"></span>
## Sample

<span id=".6K-35rGC6LaF5pe25pe26Ze06K6-572u"></span>
### Request timed out time settings

When calling the PostgreSQL interface with the SDK, there is no timeout limit by default. You can specify the request timeout (unit: seconds) by adding the `_request_timeout` parameter at the end of the code when initiating the interface call request. If the request is not completed within this time, it will be immediately terminated and report a timeout error. For example, you can set the timeout to 10 seconds with the following code when calling the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances) interface.

```python
resp = api_instance.describe_db_instances(pg.DescribeDBInstancesRequest(
    page_number=1,
    page_size=10,
), _request_timeout=10)
```


<span id=".5Yib5bu6IFBvc3RncmVTUUwg5a6e5L6L"></span>
### Creating PostgreSQL instance

For information about the definition, range, and other parameters used in the following SDK code, see [CreateDBInstance](https://docs.byteplus.com/en/docs/RDS_for_PG/CreateDBInstance).

```python
from pprint import pprint
import volcenginesdkcore
import volcenginesdkrdspostgresql as pg
from volcenginesdkcore.rest import ApiException
if  __name__ ==  "__main__":
        configuration = volcenginesdkcore.Configuration()
        configuration.ak =  "Your AK"
        configuration.sk =  "Your SK"
        configuration.region =  "Your Region"
        configuration.host = "Your Host"
    try:
        api_instance = pg.RDSPOSTGRESQLApi(volcenginesdkcore.ApiClient(configuration))
        resp = api_instance.create_db_instance(pg.CreateDBInstanceRequest(
            db_engine_version="PostgreSQL_12",
            node_info=[
                pg.NodeInfoForCreateDBInstanceInput(
                    zone_id="cn-beijing-a",
                    node_type="Primary",
                    node_spec="rds.postgres.1c2g",
                    node_operate_type="Create"
                ),
                pg.NodeInfoForCreateDBInstanceInput(
                    zone_id="cn-beijing-a",
                    node_type="Secondary",
                    node_spec="rds.postgres.1c2g",
                    node_operate_type="Create"
                ),
            ],
            storage_type="LocalSSD",
            storage_space=20,
            vpc_id="vpc-2bzo8w6m87v282dx0eemg****",
            subnet_id="subnet-2d6b6byrhtts058ozfenq****",
            charge_info=pg.ChargeInfoForCreateDBInstanceInput(charge_type="PostPaid"),
            instance_name="testname",
        ))
        pprint(resp)
    except  ApiException  as  e:
        print("Exception: %s\n"  % e)
```


The parameter configuration in this example is shown in the table below.


|Configuration item |Note |Value |
|---|---|---|
|DBEngineVersion |Instance version. |PostgreSQL_12 |
|NodeInfo |Instance specification configuration. |[{<br><br>"ZoneId": "cn\-beijing\-a",<br><br>"NodeSpec": "rds.postgres.1c2g",<br><br>"NodeType": "Primary",<br><br>"NodeOperateType": "Create"<br><br>}, {<br><br>"ZoneId": "cn\-beijing\-a",<br><br>"NodeSpec": "rds.postgres.1c2g",<br><br>"NodeType": "Secondary",<br><br>"NodeOperateType": "Create"<br><br>}] |
|StorageType |Storage type. |LocalSSD |
|StorageSpace |Instance storage space. |20 |
|VpcId |A proprietary network (VPC) ID. |vpc\-2bzo8w6m87v282dx0eemg\*\*\*\* |
|SubnetId |Subnet ID. |subnet\-2d6b6byrhtts058ozfenq\*\*\*\* |
|InstanceName |Storage type. |testname |
|ChargeInfo |Billing method. |{<br><br>"ChargeType": "PostPaid"<br><br>} |


<span id=".5p-l6K-iIFBvc3RncmVTUUwg5a6e5L6L5L-h5oGv"></span>
### Query PostgreSQL instance information

```python
from pprint import pprint
import volcenginesdkcore
import volcenginesdkrdspostgresql as pg
from volcenginesdkcore.rest import ApiException
if  __name__ ==  "__main__":
        configuration = volcenginesdkcore.Configuration()
        configuration.ak =  "Your AK"
        configuration.sk =  "Your SK"
        configuration.region =  "Your Region"
        configuration.host = "Your Host"
        try:
            # Create PostgreSQL SDK client; all interface calls need to be executed through this client
            api_instance = pg.RDSPOSTGRESQLApi(volcenginesdkcore.ApiClient(configuration))
            resp = api_instance.describe_db_instance_detail(pg.DescribeDBInstanceDetailRequest(
                instance_id="Your InstanceId",
            ))
            print(resp)
        except ApiException as e:
            print("Exception: %s\n" % e)
```


&nbsp;
