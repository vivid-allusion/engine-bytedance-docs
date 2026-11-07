---
title: "Core process"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Core_process"
---

<span id="core-process"></span>
# Core process

Complete the following preparatory steps as instructed in the "Preparation" topic:


1. Register an account and enable the service.

2. Obtain an access key.

3. Construct and save a signature generation function named volc_auth.py.


Then, you can call API operations to perform tasks such as creating a collection, writing data to a collection, creating an index, and searching data.

This topic provides several examples of calling API operations in Python to perform tasks in VikingDB. The following **domain names** are used.

[https://api-vikingdb.mlp.cn-hongkong.bytepluses.com](https://api-vikingdb.mlp.cn-hongkong.bytepluses.com) **(for** **Hong Kong)** 

[https://api-vikingdb.mlp.ap-mya.byteplus.com ](https://api-vikingdb.mlp.ap-mya.byteplus.com) **(for Johor)** 

Due to cross\-border network access latency, product performance in overseas environments may vary slightly from the standard product performance provided in China. For more information, refer to [VikingDB FAQ](https://docs.byteplus.com/en/docs/VikingDB/FAQs_about_performance).

<span id="2c6eae24"></span>
# Create a collection

Before running the following code, make sure that you have saved the volc_auth.py file (containing the code for signature generation) in the same directory as the following code. For more information, refer to the "3. Construct and save a signature generation function (in Python)" section in the "Preparation" topic.

```Python
import requests 
from volc_auth import prepare_request 
# Note: If `volc_auth` is highlighted in red and an error occurs, do not use `pip install volc_auth`. 
# This is because `volc_auth.py` is not an installation package, but a local Python file. 
# Make sure that you have saved the `volc_auth.py` file (refer to the "Preparation" topic) in the same directory as the following code. 
# For more information, refer to the "3. Construct and save a signature generation function (in Python)" section in the "Preparation" topic. 

AK = "*" 
SK = "*" 
DOMAIN = "api-vikingdb.mlp.ap-mya.byteplus.com" 

# Create a collection. 
request_params = { 
    "collection_name": "your_collection", 
    "description": "this is an example", 
    # Set a primary key. 
    "primary_key": "id", 
    # Specify fields. 
    "fields": [ 
        { 
            "field_name": "id", 
            "field_type": "int64", 
            "default_val": 0, 
        }, 
        {"field_name": "vector_field", "field_type": "vector", "dim": 64} 
        # Specify other fields as you need. 
    ], 
} 

# Call the prepare_request function to generate a request and add a signature. 
info_collection_req = prepare_request( 
    method="POST", 
    path="/api/collection/create", 
    ak=AK, 
    sk=SK, 
    data=request_params, 
) 
# Complete the request. 
r = requests.request( 
    method=info_collection_req.method, 
    url="https://{}{}".format(DOMAIN, info_collection_req.path), 
    headers=info_collection_req.headers, 
    params=info_collection_req.query, 
    data=info_collection_req.body, 
) 

# Print the response. 
print(r.text)
```


<span id="ab0d85cc"></span>
# Write data to a collection

Before running the following code, make sure that you have saved the volc_auth.py file (containing the code for signature generation) in the same directory as the following code. For more information, refer to the "3. Construct and save a signature generation function (in Python)" section in the "Preparation" topic.

```Python
import random 
import requests 
from volc_auth import prepare_request 
# Note: If `volc_auth` is highlighted in red and an error occurs, do not use `pip install volc_auth`. 
# This is because `volc_auth.py` is not an installation package, but a local Python file. 
# Make sure that you have saved the `volc_auth.py` file (refer to the "Preparation" topic) in the same directory as the following code. 
# For more information, refer to the "3. Construct and save a signature generation function (in Python)" section in the "Preparation" topic. 

def gen_random_vector(dim): 
    res = [ 
        0, 
    ] * dim 
    for i in range(dim): 
        res[i] = random.random() - 0.5 
    return res 


AK = "*" 
SK = "*" 
DOMAIN = "api-vikingdb.mlp.ap-mya.byteplus.com" 

# Write data to the collection. 
request_params = { 
    "collection_name": "your_collection", 
    "fields": [ 
        { 
            "id": 1, 
            # The vector dimension should be consistent with the value of the dim parameter specified during creation. 
            "vector_field": gen_random_vector(64), 
        }, 
        { 
            "id": 2, 
            # The vector dimension should be consistent with the value of the dim parameter specified during creation. 
            "vector_field": gen_random_vector(64), 
        }, 
        { 
            "id": 3, 
            # The vector dimension should be consistent with the value of the dim parameter specified during creation. 
            "vector_field": gen_random_vector(64), 
        }, 
    ], 
} 

# Call the prepare_request function to generate a request and add a signature. 
info_collection_req = prepare_request( 
    method="POST", 
    path="/api/collection/upsert_data", 
    ak=AK, 
    sk=SK, 
    data=request_params, 
) 
# Complete the request. 
r = requests.request( 
    method=info_collection_req.method, 
    url="https://{}{}".format(DOMAIN, info_collection_req.path), 
    headers=info_collection_req.headers, 
    data=info_collection_req.body, 
) 

# Print the response. 
print(r.text)
```


<span id="980b1466"></span>
# Query data in a collection

Before running the following code, make sure that you have saved the volc_auth.py file (containing the code for signature generation) in the same directory as the following code. For more information, refer to the "3. Construct and save a signature generation function (in Python)" section in the "Preparation" topic.

```Python
import requests 
from volc_auth import prepare_request 
# Note: If `volc_auth` is highlighted in red and an error occurs, do not use `pip install volc_auth`. 
# This is because `volc_auth.py` is not an installation package, but a local Python file. 
# Make sure that you have saved the `volc_auth.py` file (refer to the "Preparation" topic) in the same directory as the following code. 
# For more information, refer to the "3. Construct and save a signature generation function (in Python)" section in the "Preparation" topic. 

AK = "*" 
SK = "*" 
DOMAIN = "api-vikingdb.mlp.ap-mya.byteplus.com" 

# Query data in a collection. 
request_params = {"collection_name": "your_collection", "primary_keys": 1} 

# Call the prepare_request function to generate a request and add a signature. 
info_collection_req = prepare_request( 
    method="GET", 
    path="/api/collection/fetch_data", 
    ak=AK, 
    sk=SK, 
    data=request_params, 
) 
# Complete the request. 
r = requests.request( 
    method=info_collection_req.method, 
    url="https://{}{}".format(DOMAIN, info_collection_req.path), 
    headers=info_collection_req.headers, 
    data=info_collection_req.body, 
) 

# Print the response. 
print(r.text)
```


<span id="f44908c2"></span>
# Create an index

Before running the following code, make sure that you have saved the volc_auth.py file (containing the code for signature generation) in the same directory as the following code. For more information, refer to the "3. Construct and save a signature generation function (in Python)" section in the "Preparation" topic.

```Python
import requests 
from volc_auth import prepare_request 
# Note: If `volc_auth` is highlighted in red and an error occurs, do not use `pip install volc_auth`. 
# This is because `volc_auth.py` is not an installation package, but a local Python file. 
# Make sure that you have saved the `volc_auth.py` file (refer to the "Preparation" topic) in the same directory as the following code. 
# For more information, refer to the "3. Construct and save a signature generation function (in Python)" section in the "Preparation" topic. 

AK = "*" 
SK = "*" 
DOMAIN = "api-vikingdb.mlp.ap-mya.byteplus.com" 

# Create an index. 
request_params = { 
    "collection_name": "your_collection", 
    "index_name": "your_index", 
    "description": "test", 
    "vector_index": { 
        "index_type": "hnsw", 
        "distance": "ip", 
        "quant": "int8", 
    }, 
} 

# Call the prepare_request function to generate a request and add a signature. 
info_req = prepare_request( 
    method="POST", 
    path="/api/index/create", 
    ak=AK, 
    sk=SK, 
    data=request_params, 
) 
# Complete the request. 
r = requests.request( 
    method=info_req.method, 
    url="https://{}{}".format(DOMAIN, info_req.path), 
    headers=info_req.headers, 
    data=info_req.body, 
) 

# Print the response. 
print(r.text)
```


<span id="ab78e71d"></span>
# Query index data

Before running the following code, make sure that you have saved the volc_auth.py file (containing the code for signature generation) in the same directory as the following code. For more information, refer to the "3. Construct and save a signature generation function (in Python)" section in the "Preparation" topic.

```Python
import requests 
from volc_auth import prepare_request 
# Note: If `volc_auth` is highlighted in red and an error occurs, do not use `pip install volc_auth`. 
# This is because `volc_auth.py` is not an installation package, but a local Python file. 
# Make sure that you have saved the `volc_auth.py` file (refer to the "Preparation" topic) in the same directory as the following code. 
# For more information, refer to the "3. Construct and save a signature generation function (in Python)" section in the "Preparation" topic. 

AK = "*" 
SK = "*" 
DOMAIN = "api-vikingdb.mlp.ap-mya.byteplus.com" 

# Query index data. 
request_params = { 
    "collection_name": "your_collection", 
    "index_name": "your_index", 
    "primary_keys": 1, 
} 

# Call the prepare_request function to generate a request and add a signature. 
info_req = prepare_request( 
    method="GET", 
    path="/api/index/fetch_data", 
    ak=AK, 
    sk=SK, 
    data=request_params, 
) 
# Complete the request. 
r = requests.request( 
    method=info_req.method, 
    url="https://{}{}".format(DOMAIN, info_req.path), 
    headers=info_req.headers, 
    data=info_req.body, 
) 

# Print the response. 
print(r.text)
```


<span id="59e76edf"></span>
# Search an index

Before running the following code, make sure that you have saved the volc_auth.py file (containing the code for signature generation) in the same directory as the following code. For more information, refer to the "3. Construct and save a signature generation function (in Python)" section in the "Preparation" topic.

```Python
import random 
import requests 
from volc_auth import prepare_request 
# Note: If `volc_auth` is highlighted in red and an error occurs, do not use `pip install volc_auth`. 
# This is because `volc_auth.py` is not an installation package, but a local Python file. 
# Make sure that you have saved the `volc_auth.py` file (refer to the "Preparation" topic) in the same directory as the following code. 
# For more information, refer to the "3. Construct and save a signature generation function (in Python)" section in the "Preparation" topic. 

AK = "*" 
SK = "*" 
DOMAIN = "api-vikingdb.mlp.ap-mya.byteplus.com" 

def gen_random_vector(dim): 
    res = [0] * dim 
    for i in range(dim): 
        res[i] = random.random() + 3 
    return res 

# Search an index. 
request_params = { 
    "collection_name": "your_collection", 
    "index_name": "your_index", 
    "search": { 
        # Search by using vectors 
        "order_by_vector": {"vectors": [gen_random_vector(64)]}, 
        "limit": 2, 
    }, 
} 

# Call the prepare_request function to generate a request and add a signature. 
info_req = prepare_request( 
    method="POST", 
    path="/api/index/search", 
    ak=AK, 
    sk=SK, 
    data=request_params, 
) 
# Complete the request. 
r = requests.request( 
    method=info_req.method, 
    url="https://{}{}".format(DOMAIN, info_req.path), 
    headers=info_req.headers, 
    data=info_req.body, 
) 

# Print the response. 
print(r.text)
```
