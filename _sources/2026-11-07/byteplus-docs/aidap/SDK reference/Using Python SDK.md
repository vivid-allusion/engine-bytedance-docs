---
title: "Using Python SDK"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Using_Python_SDK"
---

This topic introduces the usage of the Python SDK for the AI Native BaaS for Supabase.

<span id="ad09RHsP"></span>
## Download and install

<span id="9FBcEqsj"></span>
### Prerequisites

Python 2.7 or above is installed.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can run the <code>python --version</code> command to check the current Python version.</div>


<span id="PosU7ICm"></span>
### SDK download URL

For the Python SDK source code of the AI Native BaaS for Supabase, refer to [SDK source code](https://github.com/volcengine/volcengine-python-sdk/tree/master/volcenginesdkaidap).

<span id="cZsqLNhT"></span>
### **Install SDK**

You can install the SDK using any of the following methods:


* Install via pip.


```Bash
pip install volcengine-python-sdk
```



* Download the Python SDK source code of the AI Native BaaS for Supabase and install it using [Setuptools](http://pypi.python.org/pypi/setuptools):


```Bash
# Run the following command to install the SDK for the specified user.
python setup.py install --user

# Run the following command to install the SDK for all users, installing the SDK in the system global environment with root privileges
sudo python setup.py install
```



If the SDK has already been installed, you can upgrade it using the following command.


```Bash
pip install --upgrade volcengine
```


<span id="L5zBmGXj"></span>
## Initialize client

The AI Native BaaS for Supabase Python client provides a series of interfaces to interact with the Supabase service for managing Supabase resources. You need to initialize the Python client before sending HTTP/HTTPS requests to the Supabase service. This topic introduces how to initialize the Supabase Python client.

<span id="gHjnX35k"></span>
### Prerequisites


* A BytePlus account has been registered and completed verification. For the detailed method, refer to [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* The Access Key ID (AK) and Secret Access Key (SK) information of the account have been obtained. For specific actions, refer to [Managing Access Keys](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-keys).

* The supported regions and corresponding hosts of the AI Native BaaS for Supabase have been obtained. Refer to [Service address](https://docs.byteplus.com/en/docs/aidap/Request_structure?lang=en).

* AI Native BaaS for Supabase Python SDK has been downloaded and installed.


<span id="0mongnXH"></span>
### Initialize client

Initialize the client with the following code.

```Python
import volcenginesdkaidap
import volcenginesdkcore


def get_aidap_client():
    configuration = volcenginesdkcore.Configuration()
    configuration.ak = "Your AK"
    configuration.sk = "Your SK"
    configuration.region = "Your Region"  # For example, cn-beijing
    configuration.host = "Your Endpoint" # AI Native BaaS for Supabase service address
    # Enable client validation: if some fields in the SDK are enums, passing illegal values will report an error early.
    configuration.client_side_validation = True
    volcenginesdkcore.Configuration.set_default(configuration)
    
    return volcenginesdkaidap.AIDAPApi()
```


<span id="jaD7RwUX"></span>
## Sample

<span id="spd7qAnb"></span>
### Request timed out time settings

By default, there is no timeout limit when using the SDK to call the interface. You can specify the request timeout (unit: seconds) by adding the _request_timeout parameter at the end of the code when initiating the interface call request. If the request is not completed within this time, it will be immediately terminated and report a timeout error. For example, when calling the [DescribeWorkspaceDetail](https://docs.byteplus.com/en/docs/aidap/DescribeWorkspaceDetail?lang=en) API, you can use the following code to set the timeout to 10 seconds.

```Python
aidap_api = get_aidap_client()

resp = aidap_api.describe_workspace_detail(
    volcenginesdkaidap.DescribeWorkspaceDetailRequest(
        workspace_id=workspace_id,
    ), 
    _request_timeout=10 # Set the request timeout to 10 seconds
)
```


<span id="QzI1BIjH"></span>
### Create workspace example

For the definitions, value ranges, and other information of the parameters used in the following SDK code, refer to [CreateWorkspace](https://docs.byteplus.com/en/docs/aidap/CreateWorkspace?lang=en).

```Python
from pprint import pprint

import volcenginesdkaidap
from volcenginesdkcore.rest import ApiException

from client.client import get_aidap_client

# Create a workspace
def create_workspace():
    aidap_api = get_aidap_client()
    
    request = volcenginesdkaidap.CreateWorkspaceRequest(
        workspace_name=f"test-workspace",
        engine_version="PostgreSQL_17",
    )

    try:
        resp = aidap_api.create_workspace(request)
        pprint(resp)
        return resp
    except ApiException as e:
        print("Exception when calling AIDAPApi -> create_workspace: %s\n" % e)
        return None
```


The parameters in this example are described in the following table.


|Configuration item |tip |Value |
|---|---|---|
|WorkspaceName |Workspace name. |test\-worksapce |
|EngineVersion |Engine version. Values:<br><br><br>* `PostgreSQL_17`: PostgreSQL 17.<br><br>* `veDB_MySQL_8_0`: veDB MySQL 8.0.<br><br>* `Supabase_1_24`: Supabase 1.24. |PostgreSQL_17 |


<span id="b0hqywOF"></span>
### Query workspace details

For the definitions, value ranges, and other information of the parameters used in the following SDK code, refer to [DescribeWorkspaceDetail](https://docs.byteplus.com/en/docs/aidap/DescribeWorkspaceDetail?lang=en).

```Python
from pprint import pprint

import volcenginesdkaidap
from volcenginesdkcore.rest import ApiException

from client.client import get_aidap_client

# Get workspace details
def describe_workspace_detail(workspace_id: str):
    aidap_api = get_aidap_client()

    try:
        resp = aidap_api.describe_workspace_detail(
            volcenginesdkaidap.DescribeWorkspaceDetailRequest(
                workspace_id=workspace_id,
            ),
            _request_timeout=10
        )
        pprint(resp)
        return resp
    except ApiException as e:
        print("Exception when calling AIDAPApi->describe_workspace_detail: %s\n" % e)
        return None
```


The parameters in this example are described in the following table.


|Configuration item |tip |Value |
|---|---|---|
|WorkspaceId |Workspace id. |test\-worksapce\-id |
