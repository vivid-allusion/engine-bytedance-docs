---
title: "Log configuration (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Logging-configuration-python-sdk"
---

This article introduces example code and sample log content for enabling the Python SDK.

<span id=".5pel5b-X5qC85byP"></span>
## Log Format

The Python SDK logging feature collects various operation logs for TOS and stores them locally as files. The log format is as follows.

```Plain
<time><python file name><level><threadId><message>
```


<span id=".5byA5ZCvLXB5dGhvbi1zZGst5pel5b-X6K6w5b2V5Yqf6IO9"></span>
## Enable Python SDK Logging

The following code demonstrates how to enable logging for the Python SDK.

```python
# -*- coding: utf-8 -*-
import logging

import os
import tos

# The following code demonstrates the enablement of logging feature in Python SDK.

# The complete file path for the log, for example /usr/local/TosClient.log
log_file_path = 'your fog file path'

# Set the log level and log file storage address for the TOS Python SDK using tos.set_logger.
# file_path is the complete file path of the log file.
# format_string is the defined log format.
# level is the log level, with the default being INFO.
# During development and testing, the log level can be set to logging.DEBUG.
tos.set_logger(file_path=log_file_path, level=logging.INFO)

# Get AK and SK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = 'your endpoint'
region = 'your region'
bucket_name = 'your bucket name'
object_key = 'your object key'

# Create a TosClientV2 object to perform operations on buckets and objects.
client = tos.TosClientV2(ak, sk, endpoint, region)

# Create bucket
client.create_bucket(bucket_name)

# Add an object to the bucket.
client.put_object(bucket_name, object_key, content='测试一下')
```


<span id=".5pel5b-X5YaF5a6556S65L6L"></span>
## Log Content Example

When using the default log format, the log content is as follows.

```python
2022-11-22 11:04:40,149 tos.utils [INFO] 4628305408 : after-request: create_multipart_upload exec httpCode: 200, requestId: 6109487c3c48944c637c3c48-ac133580-1oxJaS-CrMU-ccs-front-mtaz-c, usedTime: 0.19967167100000083 s
2022-11-22 11:04:40,903 tos.utils [INFO] 123145364279296 : after-request: upload_part exec httpCode: 200, requestId: 6109487c3c48946f637c3c48-ac133580-1oxJaS-UP-ccs-front-mtaz-c, usedTime: 0.7408098059999997 s
2022-11-22 11:05:05,600 tos.utils [INFO] 123145347489792 : after-request: upload_part exec httpCode: 200, requestId: 6109487c3c489456637c3c48-ac133580-1oxJaS-UP-ccs-front-mtaz-c, usedTime: 25.438498578 s
2022-11-22 11:05:05,665 tos.utils [INFO] 4628305408 : after-request: complete_multipart_upload exec httpCode: 200, requestId: 6109487c3c61a7a8637c3c61-ac133580-1oxJar-CoMU-ccs-front-mtaz-c, usedTime: 0.06059913000000705 s
2022-11-22 11:05:05,764 tos.utils [INFO] 4628305408 : after-request: get_object exec httpCode: 200, requestId: 6109487c3c61a7b1637c3c61-ac133580-1oxJar-GO-ccs-front-mtaz-c, usedTime: 0.05564314099999734 s
```
