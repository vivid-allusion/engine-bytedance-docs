---
title: "Code examples"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Python_Code_examples"
---

The code examples for the Cloud Search Python SDK are for reference only.

<span id="f7GRPvLu"></span>
## **Prerequisites**


* You have [downloaded and installed](https://docs.byteplus.com/en/docs/cloudsearch/Python_Download_and_installation) the SDK.

* You have [initialized the client](https://docs.byteplus.com/en/docs/cloudsearch/Python_Client_initialization).


<span id="wlzlmmVb"></span>
## **Set the request timeout**

When calling the SQL Server interface using the SDK, there is no default timeout setting. You can add the `_request_timeout` parameter at the end of your code when initiating an API request to specify the request timeout period (in seconds). If the request is not completed within that time, it will be immediately terminated and return a timeout error. For example, when calling the DescribeInstances interface, you can set the timeout to `10` seconds using the following code:

```Python
resp = escloud_api.describe_instance(
    byteplussdkescloud.DescribeInstanceRequest(
        instance_id="escloud-",
        _configuration=configuration,
    ),
    _request_timeout=10
)
```


<span id="aEcWh0DK"></span>
## **Create an instance**

For information about the parameters in the following SDK code, such as their definitions and value ranges, see [CreateDBInstance](https://docs.byteplus.com/en/docs/cloudsearch/CreateInstance).

```Python
from __future__ import print_function

import sys

import byteplussdkcore
import byteplussdkescloud as escloud_sdk
from byteplussdkcore.rest import ApiException

if __name__ == '__main__':
    # Create an instance
    configuration = byteplussdkcore.Configuration()
    configuration.ak = "xxx"
    configuration.sk = "xxx"
    configuration.region = "cn-beijing"
    configuration.endpoint = "escloud.cn-beijing.byteplusapi.com"
    configuration.connect_timeout = 3
    configuration.read_timeout = 3
    byteplussdkcore.Configuration.set_default(configuration)

    # use global default configuration
    api_instance = escloud_sdk.ESCLOUDApi()
    ins_config = escloud_sdk.InstanceConfigurationForCreateInstanceInOneStepInput(
        instance_name="test-create-by-python",
        admin_password="sdk@es",
        charge_type="PostPaid",
        enable_https=True,
        version="OPEN_SEARCH_2_9",
        region_id="cn-beijing",
        zone_id="cn-beijing-a",
        vpc=escloud_sdk.VPCForCreateInstanceInput(vpc_name="es-vpc", vpc_id="test-vpc-id", ),
        subnet=escloud_sdk.SubnetForCreateInstanceInput(subnet_name="es-subnet",
                                                        subnet_id="test-subnet-id",),
        node_specs_assigns=[escloud_sdk.NodeSpecsAssignForModifyNodeSpecInOneStepInput(
            type="Hot",
            number=3,
            resource_spec_name="es.x2.medium",
            storage_spec_name="es.volume.essd.pl0",
            storage_size=20
        )]
    )
    tags = [escloud_sdk.TagForCreateInstanceInOneStepInput(key="key1", value="value1")]
    create_request = escloud_sdk.CreateInstanceInOneStepRequest(instance_configuration=ins_config, tags=tags)


    try:
        resp = api_instance.create_instance_in_one_step(create_request)
        print(resp)
    except ApiException as e:
        print("Exception when calling api: %s\n" % e)

    
```


<span id="YoAKEs4Z"></span>
## Query instance information

For information about the parameters in the following SDK code, such as their definitions and value ranges, see DescribeInstance.

```python
from __future__ import print_function

import sys

import byteplussdkcore
import byteplussdkescloud as escloud_sdk
from byteplussdkcore.rest import ApiException


def describe_instance():
    # Query instance information
    configuration = byteplussdkcore.Configuration()
    configuration.ak = "xxx"
    configuration.sk = "xxx"
    configuration.region = "cn-beijing"
    configuration.endpoint = "escloud.cn-beijing.byteplusapi.com"
    configuration.connect_timeout = 3
    configuration.read_timeout = 3
    byteplussdkcore.Configuration.set_default(configuration)

    api_instance = escloud_sdk.ESCLOUDApi()
    describe_instance_request = escloud_sdk.DescribeInstanceRequest(
        instance_id="o-xx"
    )

    try:
        resp = api_instance.describe_instance(describe_instance_request)
        print(resp)
    except ApiException as e:
        print("Exception when calling api: %s\n" % e)
```
