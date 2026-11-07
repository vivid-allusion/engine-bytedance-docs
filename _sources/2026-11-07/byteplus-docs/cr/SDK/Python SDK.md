---
title: "Python SDK"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/python-sdk"
---

This topic introduces how to install and configure Container Registry (CR) SDK for Python and demonstrates how to use it to call cloud APIs.

<span id="使用说明"></span>
## Usage notes

Only Python 2.7 and later are supported.

<span id="安装配置"></span>
## Installation settings

Install [volcengine-python-sdk](https://pypi.org/project/volcengine-python-sdk/).

<span id="sdk-示例"></span>
## Code sample for using the SDK

This topic uses [ListRegistries](https://docs.byteplus.com/en/docs/cr/listregistries) as an example.

```python
import volcenginesdkcore
import volcenginesdkcr
from pprint import pprint
from volcenginesdkcr.models.filter_for_list_registries_input import FilterForListRegistriesInput
from volcenginesdkcr.models.status_for_list_registries_input import StatusForListRegistriesInput

if __name__ == '__main__':
    configuration = volcenginesdkcore.Configuration()
    configuration.host = "Address for API calls" # The address for API calls
    configuration.ak = "AKLT****" # Your AccessKey ID
    configuration.sk = "WTJG****" # Your AccessKey secret
    configuration.region = "ap-southeast-1"

    # create an instance of the API class
    api_instance = volcenginesdkcr.CRApi(
        volcenginesdkcore.ApiClient(configuration))

    registry = "enterprise-1"
    status_list_registry = StatusForListRegistriesInput(
        condition='Ok', phase='Running')
    filter_list_registry = FilterForListRegistriesInput(
        types=['Basic', 'Enterprise'], statuses=[status_list_registry])
    body_list_registry = volcenginesdkcr.ListRegistriesRequest(
        filter_list_registry)
    pprint(body_list_registry)
    resp_list_registry = api_instance.list_registries(
        body_list_registry)
    print("resp_list_registry\n", resp_list_registry, "\n")
```
