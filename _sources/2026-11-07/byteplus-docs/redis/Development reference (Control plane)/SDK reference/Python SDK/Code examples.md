---
title: "Code examples"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/code-example-python"
---

This topic provides code examples for the Redis Python SDK for your reference.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


1. [Downloading and installing SDK](https://docs.byteplus.com/en/docs/redis/download-install-python-sdk)

2. [Initializing client](https://docs.byteplus.com/en/docs/redis/client-initialization-python)


<span id=".6K-35rGC6LaF5pe25pe26Ze06K6-572u"></span>
## Configure request timeout

When using the Python SDK to call Redis interfaces, there is no default timeout.

When you make an API call, you can add the `_request_timeout` parameter at the end of the code to specify the request timeout in seconds. If the request does not complete within this period, it terminates and a timeout error is reported.

For example, when calling the DescribeDBInstanceDetail API, you can set the timeout to 10 seconds with the following code.

```Python
resp = api_instance.describe_db_instance_detail(byteplussdkredis.DescribeDBInstanceDetailRequest(
    instance_id="redis-cn04giei8c91*****",
), _request_timeout=10)
```


<span id=".5Yib5bu6LXJlZGlzLeWunuS-iw=="></span>
## Creating Redis instance

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the definitions, value ranges, and other information of the parameters used in the following SDK code, refer to <a href="https://docs.byteplus.com/en/docs/redis/createdbinstance">CreateDBInstance</a>.</div>



<Tabs>
<Tab zoneid="bKsbzHLH1g" title="Example 1">
<TabTitle>Example 1</TabTitle>

Use the following example code to create a Redis instance with sharding cluster enabled, configured as follows:


* Database version number: 5.0.

* Available memory: 8 GiB (i.e. 8192 MiB).

* Number of shards: 2.

* Number of nodes in each shard: 3.

* In the China (Beijing) region, multi\-availability zone deployment is used, in which the primary node is deployed in the availability zone A, and both secondary nodes are deployed in the availability zone B.

* Associate with two allowlists: `acl-cq014ioqkm9zt5j****` and `acl-cq015pp15v8buvl****`.

* Associate with two tags: `department:game` and `owner:Alice`.

* Billing type: Subscription, expected to be used for 3 months, and auto\-renewal is disabled.


```Python
import byteplussdkredis
import byteplussdkcore
from byteplussdkcore.rest import ApiException
from pprint import pprint

if __name__ == "__main__":
    configuration = byteplussdkcore.Configuration()

    configuration.ak = "Your AK"
    configuration.sk = "Your SK"
    configuration.region = "Your Region"

    try:
        api_instance = byteplussdkredis.REDISApi(byteplussdkcore.ApiClient(configuration))
        resp = api_instance.create_db_instance(byteplussdkredis.CreateDBInstanceRequest(
            region_id="cn-beijing",
            multi_az="enabled",
            configure_nodes=[
                byteplussdkredis.ConfigureNodeForCreateDBInstanceInput(az="cn-beijing-a"),
                byteplussdkredis.ConfigureNodeForCreateDBInstanceInput(az="cn-beijing-b"),
                byteplussdkredis.ConfigureNodeForCreateDBInstanceInput(az="cn-beijing-c"),
              ], 
            instance_name="python_sdk_shardedcluster_test",
            sharded_cluster=1,
            password="Pwd@12****",
            node_number=2,
            shard_number=2,
            shard_capacity=8192,
            engine_version="5.0",
            vpc_id="vpc-1g0ckv3hu4s1s8ibuxwqe****",
            subnet_id="subnet-1g0ckvr67hfr48ibuxxgr****",
        ))
        pprint(resp)
    except ApiException as e:
        print("Exception when calling REDISApi->create_db_instance: %s\n" % e)
```





</Tab>
<Tab zoneid="Gvbwa5W6Qt" title="Example 2">
<TabTitle>Example 2</TabTitle>

Use the following example code to create a Redis instance with sharding cluster disabled, configured as follows:


* Database version number: 5.0.

* Available memory: 8 GiB (i.e. 8192 MiB).

* Number of nodes: 2.

* Use single\-availability\-zone deployment in the China (Beijing) region, and all nodes are deployed in availability zone A.


```Python
import byteplussdkredis
import byteplussdkcore
from byteplussdkcore.rest import ApiException
from pprint import pprint

if __name__ == "__main__":
    configuration = byteplussdkcore.Configuration()

    configuration.ak = "Your AK"
    configuration.sk = "Your SK"
    configuration.region = "Your Region"

    try:
        api_instance = byteplussdkredis.REDISApi(byteplussdkcore.ApiClient(configuration))
        resp = api_instance.create_db_instance(byteplussdkredis.CreateDBInstanceRequest(
            region_id="cn-beijing",
            multi_az="disabled",
            configure_nodes=[
                byteplussdkredis.ConfigureNodeForCreateDBInstanceInput(az="cn-beijing-a"),
            ], 
            instance_name="python_sdk_test",
            sharded_cluster=0,
            password="Pwd@12****",
            node_number=2,
            shard_capacity=8192,
            engine_version="5.0",
            vpc_id="vpc-1g0ckv3hu4s1s8ibuxwqe****",
            subnet_id="subnet-1g0ckvr67hfr48ibuxxgr****",
        ))
        pprint(resp)
    except ApiException as e:
        print("Exception when calling REDISApi->create_db_instance: %s\n" % e)
```





</Tab>
</Tabs>


<span id=".5p-l6K-iLXJlZGlzLeWunuS-i-S_oeaBrw=="></span>
## Querying Redis instance information

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the definitions, value ranges, and other information of the parameters used in the following SDK code, refer to <a href="https://docs.byteplus.com/en/docs/redis/describedbinstancedetail">DescribeDBInstanceDetail</a>.</div>


```Python
import byteplussdkredis
import byteplussdkcore
from byteplussdkcore.rest import ApiException
from pprint import pprint

if __name__ == "__main__":
    configuration = byteplussdkcore.Configuration()

    configuration.ak = "Your AK"
    configuration.sk = "Your SK"
    configuration.region = "Your Region"

    try:
        api_instance = byteplussdkredis.REDISApi(byteplussdkcore.ApiClient(configuration))
        # Querying information about specified Redis instance
        resp = api_instance.describe_db_instance_detail(byteplussdkredis.DescribeDBInstanceDetailRequest(
            instance_id="redis-cn04giei8c91*****",
        ))
        pprint(resp)
    except ApiException as e:
        print("Exception when calling REDISApi->describe_db_instance_detail: %s\n" % e)
```
