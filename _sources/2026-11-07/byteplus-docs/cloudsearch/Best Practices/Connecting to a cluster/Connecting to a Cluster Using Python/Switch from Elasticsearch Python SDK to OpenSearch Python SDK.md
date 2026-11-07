---
title: "Switch from Elasticsearch Python SDK to OpenSearch Python SDK"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Switch_from_Elasticsearch_Python_SDK_to_OpenSearch_Python_SDK"
---

Cloud Search currently supports Elasticsearch 7.10.2 and later versions and OpenSearch 2.9.0 and later versions Instances. If switching from an Elasticsearch 7.10.2 or later Instance to an OpenSearch 2.9.0 or later Instance, you need to switch to the OpenSearch 2.9.0 or later Python SDK when using the Python SDK to connect to the Instance. This topic describes the process of switching to the OpenSearch 2.9.0 or later Python SDK.

<span id="a9d0c89c"></span>
## Switching process

The OpenSearch 2.9.0 and later SDK is mostly compatible with Elasticsearch 7.10.2 and later APIs except for x\-pack, meaning it supports Elasticsearch 7.10.2 and later OSS APIs. Users normally only need to make the following two changes when switching SDKs:


1. Install the OpenSearch Python client.

   ```Bash
   pip install opensearch-py
   ```
   

2. Modify the import paths of related packages in the source code.

   ```Python
   from opensearchpy import OpenSearch
   
   # Create an OpenSearch client connection.
   client = OpenSearch(
                       ......
   ```
