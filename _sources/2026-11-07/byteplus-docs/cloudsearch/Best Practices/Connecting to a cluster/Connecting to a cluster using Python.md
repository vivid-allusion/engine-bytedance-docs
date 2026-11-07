---
title: "Connecting to a cluster using Python"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/connecting-cluster-Python"
---

Open source Elasticsearch and the community have rolled out SDKs in various programming languages for your convenience. This topic describes how to connect to an ES instance by using Python and provides you with sample code and precautions.

<span id="16bc736e"></span>
## Preparation


* Create an ES instance and make sure that it runs normally. For more information, refer to [Creating instance](https://docs.byteplus.com/en/docs/cloudsearch/creating-an-instance-2).


8 Make sure that the server running Python code can communicate with the ES instance.


* If the server running Python code is in the same virtual private cloud (VPC) as the ES instance, the ES instance can be connected using its private endpoint. Before connecting to the ES instance, make sure that the private IP address of the server is added to the private IP allowlist. By default, the private IP allowlist only contains 0.0.0.0/0. For more information, refer to [Configuring a private IP allowlist for an instance](https://docs.byteplus.com/en/docs/cloudsearch/IPallowlist-for-instance).

* If the server running Python code is in the internet environment, the ES instance can be connected using its public endpoint. Before connecting to the ES instance, enable internet\-facing access to the instance and add the public IP address of the server to the public IP allowlist. For more information, refer to [Enabling public network access to an instance](https://docs.byteplus.com/en/docs/cloudsearch/enabling-public-access) and [Configuring a public IP allowlist for an instance](https://docs.byteplus.com/en/docs/cloudsearch/public-IPallowlist-for-instance).


<span id="b0857147"></span>
## Installing an Elasticsearch Python client

We recommend that you use an Elasticsearch Python client whose version is consistent with that of the ES instance.

For example, if the version of the ES instance you want to access is 7.10.2, install Elasticsearch Python client version 7.10.

Run the following command to install an Elasticsearch Python client:

```Python
pip install Elasticsearch==7.10
```


<span id="d31733c6"></span>
## Connecting to the HTTP cluster

This scenario applies to Cloud Search instances that must be connected over HTTP.

Sample code:

```Python
from elasticsearch import Elasticsearch

# Connect the client to the ES cluster.
es = Elasticsearch(['{INSTANCE_CONN_ADDR}', '9200'],
                   http_auth=('{INSTANCE_USER}', '{PASSWORD}')
                   )

# Create an index and configure settings, mappings, and fields as needed.
index_name = '{INDEX_NAME}'
index_body = {
    'settings': {
        'number_of_shards': 3,
        'number_of_replicas': 1
    },
    'mappings': {
        'properties': {
            'name': {
                'type': 'text'
            },
            'age': {
                'type': 'integer'
            }
        }
    }
}

response = es.indices.create(index=index_name, body=index_body)
print(response)
```


Run the program. Information similar to the following is returned:

```JSON
{'acknowledged': True, 'shards_acknowledged': True, 'index': 'custom-index'}
```


<span id="4c4a0424"></span>
## Connecting to the HTTPS cluster

<span id="9e697008"></span>
### With certificate verification

This scenario applies to Cloud Search instances that must be connected over HTTPS and require HTTPS certificate verification during the connection process.

Sample code:

```Python
from elasticsearch import Elasticsearch
from ssl import create_default_context

# Create an SSL context and load the certificate.
ssl_context = create_default_context(cafile='{CERT_PATH}')

# Connect the client to the ES cluster.
es = Elasticsearch(['{INSTANCE_CONN_ADDR}', '9200'],
                   ssl_context=ssl_context,
                   scheme="https",
                   http_auth=('{INSTANCE_USER}', '{PASSWORD}')
)

# Create an index and configure settings, mappings, and fields as needed.
index_name = '{INDEX_NAME}'
index_body = {
    'settings': {
        'number_of_shards': 3,
        'number_of_replicas': 1
    },
    'mappings': {
        'properties': {
            'name': {
                'type': 'text'
            },
            'age': {
                'type': 'integer'
            }
        }
    }
}

response = es.indices.create(index=index_name, body=index_body)
print(response)
```


Run the program. Information similar to the following is returned:

```JSON
{'acknowledged': True, 'shards_acknowledged': True, 'index': 'custom-index'}
```


<span id="42e1a243"></span>
### Without certificate verification

This scenario applies to Cloud Search instances that must be connected over HTTPS and do not verify HTTPS certificates during the connection process.

Sample code:

```Python
from elasticsearch import Elasticsearch
import ssl

# Create an SSL context and set the verification mode to CERT_NONE, which means that the certificate is not verified.
ssl_context = ssl.create_default_context()
ssl_context.check_hostname = False
ssl_context.verify_mode = ssl.CERT_NONE


# Connect the client to the ES cluster.
es = Elasticsearch(['{INSTANCE_CONN_ADDR}', '9200'],
                   ssl_context=ssl_context,
                   scheme="https",
                   http_auth=('{INSTANCE_USER}', '{PASSWORD}')
)

# Create an index and configure settings, mappings, and fields as needed.
index_name = '{INDEX_NAME}'
index_body = {
    'settings': {
        'number_of_shards': 3,
        'number_of_replicas': 1
    },
    'mappings': {
        'properties': {
            'name': {
                'type': 'text'
            },
            'age': {
                'type': 'integer'
            }
        }
    }
}

response = es.indices.create(index=index_name, body=index_body)
print(response)
```


Run the program. Information similar to the following is returned:

```JSON
{'acknowledged': True, 'shards_acknowledged': True, 'index': 'custom-index'}
```
