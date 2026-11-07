---
title: "Getting started"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/tls_sdk_for_python_getting_started"
---

This topic describes how to use Torch Log Service (TLS) SDK for Python to quickly collect logs, including creating projects, creating topics, writing logs, and querying logs.

<span id="前提条件"></span>
## Before you begin


* Install TLS SDK for Python. For more information, refer to [Install TLS SDK for Python](https://docs.byteplus.com/docs/tls/install_tls_sdk_for_python).

* Add environment variables such as `VOLCENGINE_ACCESS_KEY_ID`. For information on how to configure environment variables, refer to [Configure identity authentication](https://docs.byteplus.com/docs/tls/configuring_identity_authentication).


<span id="6802f269"></span>
## Precautions

When you use TLS SDK for Python to call PutLogs, LZ4 is used by default. However, the lz4a library is not contained in the installation script of TLS SDK for Python due to cross\-platform compatibility considerations. To use LZ4 in the process of uploading logs, install the lz4a library manually in the environment.

```shell
pip install lz4a==0.7.0
```


If you use Windows, or Python 3.10 or later, the SDK is not compatible with LZ4. In this case, skip the step of installing the lz4a library, and specify `compression=zlib` in PutLogsV2Request.

Sample code of using PutLogsV2Request:


* LZ4

   ```Plain
   tls_service.put_logs_v2(PutLogsV2Request(topic_id, logs))
   ```
   

* Zlib

   ```Plain
   tls_service.put_logs_v2(PutLogsV2Request(topic_id, logs, compression="zlib"))
   ```
   


<span id="f5ff275e"></span>
## Initializing the client

Initialize the client instance before you can send requests to TLS. When you initialize the client, we recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard\-coded AccessKey information leads to data security risks.

Initialization code:

```python
from volcengine.tls.TLSService import TLSService

# Note that the endpoint in environment variables does not contain https:// or http://, such as tls-ap-southeast-1.ibytepluses.com.
endpoint = os.environ["VOLCENGINE_ENDPOINT"]
region = os.environ["VOLCENGINE_REGION"]
access_key_id = os.environ["VOLCENGINE_ACCESS_KEY_ID"]
access_key_secret = os.environ["VOLCENGINE_ACCESS_KEY_SECRET"]

tls_service = TLSService(endpoint, access_key_id, access_key_secret, region)
```


<span id="示例代码"></span>
## Sample code

Create a `example_tls.py` file, and call API actions to create a project, topic, and index, and write, consume, and query log data.

Sample code:

```python
# coding=utf-8
from __future__ import absolute_import
from __future__ import division
from __future__ import print_function

import time

from volcengine.tls.TLSService import TLSService
from volcengine.tls.tls_requests import *


if __name__ == "__main__":
    # When you initialize the client, we recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard-coded AccessKey information leads to data security risks. 
    # If you use Security Token Service (STS), use a temporary AccessKey ID and AccessKey secret, and set VOLCENGINE_TOKEN. If you do not use STS, leave VOLCENGINE_TOKEN empty.
    endpoint = os.environ["VOLCENGINE_ENDPOINT"]
    region = os.environ["VOLCENGINE_REGION"]
    access_key_id = os.environ["VOLCENGINE_ACCESS_KEY_ID"]
    access_key_secret = os.environ["VOLCENGINE_ACCESS_KEY_SECRET"]

    # Instantiate the TLS client.
    tls_service = TLSService(endpoint, access_key_id, access_key_secret, region)

    # Create a project.
    create_project_request = CreateProjectRequest(project_name="project-name", region=region,
                                                  description="project-description")
    create_project_response = tls_service.create_project(create_project_request)
    project_id = create_project_response.project_id

    # Create a topic.
    create_topic_request = CreateTopicRequest(topic_name="topic-name", project_id=project_id,
                                              ttl=3650, description="topic-description", shard_count=2)
    create_topic_response = tls_service.create_topic(create_topic_request)
    topic_id = create_topic_response.topic_id

    # Create an index.
    full_text = FullTextInfo(case_sensitive=False, delimiter=",-;", include_chinese=False)
    value_info_a = ValueInfo(value_type="text", delimiter="", case_sensitive=True,
                             include_chinese=False, sql_flag=False)
    value_info_b = ValueInfo(value_type="long", delimiter="", case_sensitive=False,
                             include_chinese=False, sql_flag=True)
    key_value_info_a = KeyValueInfo(key="key1", value=value_info_a)
    key_value_info_b = KeyValueInfo(key="key2", value=value_info_b)
    key_value = [key_value_info_a, key_value_info_b]
    create_index_request = CreateIndexRequest(topic_id, full_text, key_value)
    create_index_response = tls_service.create_index(create_index_request)

    # Write log data.
    logs = PutLogsV2Logs(source="192.168.1.1", filename="sys.log")
    for i in range(100):
        logs.add_log(contents={"key1": "value1-" + str(i + 1), "key2": "value2-" + str(i + 1)},
                     log_time=int(round(time.time())))
    tls_service.put_logs_v2(PutLogsV2Request(topic_id, logs))
    time.sleep(30)

    # Query a cursor.
    describe_cursor_request = DescribeCursorRequest(topic_id, shard_id=0, from_time="begin")
    describe_cursor_response = tls_service.describe_cursor(describe_cursor_request)

    # Consume log data.
    consume_logs_request = ConsumeLogsRequest(topic_id, shard_id=0, cursor=describe_cursor_response.cursor)
    consume_logs_response = tls_service.consume_logs(consume_logs_request)

    # To query and analyze logs, we recommend that you use the search_logs_v2 method in TLS SDK for Python. The following code offers a sample call.
    # Query log data using full-text search.
    search_logs_request = SearchLogsRequest(topic_id, query="error", limit=10,
                                            start_time=1346457600000, end_time=1630454400000)
    search_logs_response = tls_service.search_logs_v2(search_logs_request)

    # Query log data using key-value search.
    search_logs_request = SearchLogsRequest(topic_id, query="key1:error", limit=10,
                                            start_time=1346457600000, end_time=1630454400000)
    search_logs_response = tls_service.search_logs_v2(search_logs_request)

    # Query log data using SQL analysis.
    search_logs_request = SearchLogsRequest(topic_id, query="* | select key1, key2", limit=10,
                                            start_time=1346457600000, end_time=1630454400000)
    search_logs_response = tls_service.search_logs_v2(search_logs_request)

    # Query log data using SQL analysis.
    search_logs_request = SearchLogsRequest(topic_id, query="* | select key1, key2", limit=10,
                                            start_time=1346457600000, end_time=1630454400000)
    search_logs_response = tls_service.search_logs(search_logs_request)
```
