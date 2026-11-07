---
title: "Code examples"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/code-example-python"
---

This topic provides sample code for the MongoDB Python SDK for your reference.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite


1. [Downloading and installing](https://docs.byteplus.com/en/docs/mongodb/download-install-python-sdk)

2. [Initializing the client](https://docs.byteplus.com/en/docs/mongodb/client-initialization-python)


<span id=".6K6-572u6K-35rGC6LaF5pe25pe26Ze0"></span>
## Configure request timeout

There is no established timeout by default when calling the MongoDB API with the Python SDK.

When you initiate the API call request, add the `_request_timeout=${timeout}` parameter to specify the request timeout (in seconds) at the end of the code. If the request is not completed within this time, it will be terminated with an error reported.

For example, you can set the established timeout to 10 seconds with the following code when calling the CreateDBInstance API.

```Python
resp = api_instance.create_db_instance(
        byteplussdkmongodb.CreateDBInstanceRequest(
            count=1, vpc_id="vpc-13f24t16guqdc3n6nu4k5****", zone_id="cn-beijing-a", 
            node_spec="mongo.1c2g", storage_space_gb=100,
            subnet_id="subnet-rr96lovl7f28v0x58tv****"
        )
    ), _request_timeout=10)
    pprint(resp)
```


<span id=".5Yib5bu6LW1vbmdvZGIt5a6e5L6L"></span>
## Creating a MongoDB instance

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the definitions, value ranges, and other information of parameters used in the following SDK code, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/createdbinstance">CreateDBInstance</a>.</div>



<Tabs>
<Tab zoneid="W6AAbSYYef" title="Example 1">
<TabTitle>Example 1</TabTitle>

Create a sharding cluster instance with the sample code below and configure it as follows:


* The availability zone where the instance is located: China (Beijing) \- availability zone A.

* Storage capacity: 100 GiB.

* Node specifications:

   * Include 2 Mongos nodes, each with 2 cores 4 GiB.

   * Include 2 shards (each includes 3 nodes by default), and the specifications of the nodes in each shard is 2 cores 4 GiB.


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
    
    # create an MonogoDB instance
    resp = api_instance.create_db_instance(
        byteplussdkmongodb.CreateDBInstanceRequest(
            vpc_id="vpc-13f24t16guqdc3n6nu4k5****", zone_id="cn-beijing-a", 
            node_spec="mongo.shard.2c4g", storage_space_gb=100,
            subnet_id="subnet-rr96lovl7f28v0x58tv****",instance_name="python_sdk_test_shard",
            mongos_node_spec="mongo.mongos.2c4g",instance_type="ShardedCluster",
            shard_number=2,mongos_node_number=2
        )
    )
    pprint(resp)
```



</Tab>
<Tab zoneid="dLx5Nzme2i" title="Example 2">
<TabTitle>Example 2</TabTitle>

Create a replica set instance (containing three nodes by default) with the configuration code below and configure it as follows:


* The availability zone where the instance is located: China (Beijing) \- availability zone A.

* Storage capacity: 100 GiB.

* Node specification: 2 cores 4 GiB.


```python
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
    
    # create an MonogoDB instance
    resp = api_instance.create_db_instance(
        byteplussdkmongodb.CreateDBInstanceRequest(
            vpc_id="vpc-13f24t16guqdc3n6nu4k5****", zone_id="cn-beijing-a",
            node_spec="mongo.2c4g", storage_space_gb=100,
            subnet_id="subnet-rr96lovl7f28v0x58tv****",instance_name="python_sdk_test_replica"
        )
    )
    pprint(resp)
```



</Tab>
</Tabs>


<span id="z4yPFKam"></span>
## Querying MongoDB instances

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the definitions, value ranges, and other information of parameters used in the following SDK requests, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/describedbinstancedetail">DescribeDBInstanceDetail</a>.</div>


```python
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
    
    # query MongoDB instance information
    resp = api_instance.describe_db_instance_detail(
        byteplussdkmongodb.DescribeDBInstanceDetailRequest(
            instance_id="mongo-replica-e649ae42****"
        )
    )
    pprint(resp)
```
