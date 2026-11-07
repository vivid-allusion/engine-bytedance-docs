---
title: "SDK Installation and Initialization"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/sdk_installation_and_initializationv2"
---

Viking DB vector database now provides a Python SDK, which can directly complete authentication, read/write, search, and vectorization operations on the data plane (Data / Search / Embedding). Please complete SDK installation and client initialization before use.

<span id="prerequisites"></span>
# Prerequisites


1. You have completed [account registration and service activation](https://www.volcengine.com/docs/84313/1254444).

2. You have obtained Volcengine AK / SK. For details, refer to [Access Key Management](https://www.volcengine.com/docs/6291/65568).

3. Prepare an available Python 3.9+ runtime environment with permission to install third\-party dependencies.


<span id="install-the-sdk"></span>
# Install the SDK

The Python SDK has been released to PyPI. You can choose to directly install the release version or install in development mode in the source directory.

<span id="_1-data-plane-dependency-configuration"></span>
## 1. Data Plane Dependency Configuration


1. Install the release version using pip


It is recommended to obtain the latest stable version via pip or uv:

```bash
uv add vikingdb-python-sdk
// or 
python3 -m pip install -U vikingdb-python-sdk
```


After installation, you can verify the version with `python3 -m pip show vikingdb-python-sdk`.


2. Install in the source directory


If you need to debug the latest source code, clone the repository and install in editable mode:

```bash
git clone https://github.com/volcengine/vikingdb-python-sdk.git
cd vikingdb-python-sdk
uv sync
uv pip install -e .
```


The SDK depends on `volcengine`, `requests`, `pydantic` and other components. If you are on an offline network, please prepare the corresponding offline packages in advance.

<span id="_2-control-plane-dependency-configuration"></span>
## 2. Control Plane Dependency Configuration


1. Install the release version using pip


It is recommended to obtain the latest stable version via pip or uv:

```bash
uv add volcengine-python-sdk
// or 
python3 -m pip install volcengine-python-sdk
```


After installation, you can verify the version with `python3 -m pip show volcengine-python-sdk`.

<span id="initialize-the-sdk"></span>
# Initialize the SDK

The initialization process consists of three parts: configuring the network egress (domain/Region), preparing authentication information, and constructing a client and sending a request to verify connectivity.

The example code uses environment variables `VIKINGDB_AK` / `VIKINGDB_SK` / `VIKINGDB_HOST` / `VIKINGDB_REGION` / `VIKINGDB_COLLECTION` / `VIKINGDB_INDEX`, etc. Please set the corresponding values before running.


1. **Data Plane (Data / Search / Embedding)** 


The data plane domain is used by `VikingVector`, `CollectionClient`, `IndexClient`, and Embedding interfaces.


|**Region Name** |**Region ID** |Internet Domain (Public Network) |Private Link Endpoint Service (**Not a Domain**) |
|---|---|---|---|
|Asia Pacific (Johor) |ap\-southeast\-1 |[api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com](http://api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com/) |com.bytepluses.privatelink.ap\-southeast\-1.vikingdb\-ann |


```python
import os
from vikingdb import IAM
from vikingdb.vector import SearchByRandomRequest, UpsertDataRequest, VikingVector

client = VikingVector(
    host=os.environ["VIKINGDB_HOST"],
    region=os.environ["VIKINGDB_REGION"],
    auth=IAM(ak=os.environ["VIKINGDB_AK"], sk=os.environ["VIKINGDB_SK"]),
    scheme="https",
)

collection_name=os.environ["VIKINGDB_COLLECTION"]
index_name=os.environ["VIKINGDB_INDEX"]

upsert_resp = client.collection(collection_name=collection_name).upsert(UpsertDataRequest(data=[{"text": "something"}]))
response = client.index(collection_name=collection_name, index_name=index_name).search_by_random(SearchByRandomRequest(limit=5))
hits = len(response.result.data) if response.result else 0
if response.result:
    for item in response.result.data:
        print(item.id, item.score, item.fields.get("text"))
```



2. **Control Plane (Collection / Index / Task)** 


The control plane is used for managing collections, indexes, and task orchestration, and currently still provides services through BytePlus OpenAPI. You can reuse `volcengine-python-sdk` or use a custom HTTP client, just ensure you use the following domains and include the AK/SK authentication signature.


|**Region Name** |**Region ID** |Internet Domain (Public Network) |Private Link Endpoint Service (**Not a Domain**) |
|---|---|---|---|
|Asia Pacific (Johor) |ap\-southeast\-1 |[vikingdb.ap-southeast-1.byteplusapi.com](http://vikingdb.ap-southeast-1.byteplusapi.com/) |com.bytepluses.privatelink.ap\-southeast\-1.api.vikingdb |


Control plane OpenAPI can be called through the generic `ApiClient` of `volcengine-python-sdk`, or you can use `requests` to manually construct the signature. The calling method is consistent with the data plane: set X\-Date, Authorization, then send a JSON request to the HTTPS interface of the above domain.

```python
import volcenginesdkvikingdb as vdb
from volcenginesdkvikingdb.api.vikingdb_api import VIKINGDBApi

client = VIKINGDBApi(
    ak="your_VIKINGDB_AK",
    sk="your_VIKINGDB_SK",
    host="your_VIKINGDB_HOST",
    region="your_VIKINGDB_REGION",
    scheme="https",
)
```
