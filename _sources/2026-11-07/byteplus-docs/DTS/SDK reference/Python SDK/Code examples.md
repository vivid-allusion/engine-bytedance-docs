---
title: "Code examples"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/code_examples"
---

This document describes how to quickly call APIs using the Database Transmission Service (DTS) Python SDK to create data transmission tasks and query task information.

<span id="prerequisites"></span>
## Prerequisites


1. [Download and install the SDK](../DTS/downloading_and_installing_an_sdk

2. [Initialize the client](../DTS/client_initialization


<span id="creating-data-transmission-tasks"></span>
## Creating data transmission tasks

<span id="querying-data-transmission-task-information"></span>
## Querying data transmission task information

```python
import json

from volcengine.dts.dts_service import DtsService

if __name__ == '__main__':
    access_key = 'your_ak_here'
    secret_key = 'your_sk_here'
    region_str = 'region_str_here'
    task_id_str = 'task_id_str'

    dts_service = DtsService(region=region_str)

    dts_service.set_ak(access_key)
    dts_service.set_sk(secret_key)

    params = {}
    body = {
        'TaskId': task_id_str
    }

    resp = dts_service.describe_transmission_task_info(params, body)
    print(json.dumps(resp, ensure_ascii=False, sort_keys=True, indent=4, separators=(',', ':')))
```


<span id="suspending-a-data-transmission-task"></span>
## Suspending a data transmission task

```python
import json

from volcengine.dts.dts_service import DtsService

if __name__ == '__main__':
    access_key = 'your_ak_here'
    secret_key = 'your_sk_here'
    region_str = 'region_str_here'
    task_id_str = 'task_id_str'

    dts_service = DtsService(region=region_str)

    dts_service.set_ak(access_key)
    dts_service.set_sk(secret_key)

    params = {}
    body = {
        'TaskId': task_id_str
    }

    resp = dts_service.suspend_transmission_task(params, body)
    print(json.dumps(resp, ensure_ascii=False, sort_keys=True, indent=4, separators=(',', ':')))
```


<span id="starting-a-data-transmission-task"></span>
## Starting a data transmission task

```python
import json

from volcengine.dts.dts_service import DtsService

if __name__ == '__main__':
    access_key = 'your_ak_here'
    secret_key = 'your_sk_here'
    region_str = 'region_str_here'
    task_id_str = 'task_id_str'

    dts_service = DtsService(region=region_str)

    dts_service.set_ak(access_key)
    dts_service.set_sk(secret_key)

    params = {}
    body = {
        'TaskId': task_id_str
    }

    resp = dts_service.start_transmission_task(params, body)
    print(json.dumps(resp, ensure_ascii=False, sort_keys=True, indent=4, separators=(',', ':')))
```


<span id="retrying-a-data-transmission-task"></span>
## Retrying a data transmission task

```python
import json

from volcengine.dts.dts_service import DtsService

if __name__ == '__main__':
    access_key = 'your_ak_here'
    secret_key = 'your_sk_here'
    region_str = 'region_str_here'
    task_id_str = 'task_id_str'

    dts_service = DtsService(region=region_str)

    dts_service.set_ak(access_key)
    dts_service.set_sk(secret_key)

    params = {}
    body = {
        'TaskId': task_id_str
    }

    resp = dts_service.retry_transmission_task(params, body)
    print(json.dumps(resp, ensure_ascii=False, sort_keys=True, indent=4, separators=(',', ':')))
```


<span id="resuming-a-data-transmission-task"></span>
## Resuming a data transmission task

```python
import json

from volcengine.dts.dts_service import DtsService

if __name__ == '__main__':
    access_key = 'your_ak_here'
    secret_key = 'your_sk_here'
    region_str = 'region_str_here'
    task_id_str = 'task_id_str'

    dts_service = DtsService(region=region_str)

    dts_service.set_ak(access_key)
    dts_service.set_sk(secret_key)

    params = {}
    body = {
        'TaskId': task_id_str
    }

    resp = dts_service.resume_transmission_task(params, body)
    print(json.dumps(resp, ensure_ascii=False, sort_keys=True, indent=4, separators=(',', ':')))
```


<span id="stopping-a-data-transmission-task"></span>
## Stopping a data transmission task

```python
import json

from volcengine.dts.dts_service import DtsService

if __name__ == '__main__':
    access_key = 'your_ak_here'
    secret_key = 'your_sk_here'
    region_str = 'region_str_here'
    task_id_str = 'task_id_str'

    dts_service = DtsService(region=region_str)

    dts_service.set_ak(access_key)
    dts_service.set_sk(secret_key)

    params = {}
    body = {
        'TaskId': task_id_str
    }

    resp = dts_service.stop_transmission_task(params, body)
    print(json.dumps(resp, ensure_ascii=False, sort_keys=True, indent=4, separators=(',', ':')))
```


<span id="deleting-a-data-transmission-task"></span>
## Deleting a data transmission task

```python
import json

from volcengine.dts.dts_service import DtsService

if __name__ == '__main__':
    access_key = 'your_ak_here'
    secret_key = 'your_sk_here'
    region_str = 'region_str_here'
    task_id_str = 'task_id_str'

    dts_service = DtsService(region=region_str)

    dts_service.set_ak(access_key)
    dts_service.set_sk(secret_key)

    params = {}
    body = {
        'TaskId': task_id_str
    }

    resp = dts_service.delete_transmission_task(params, body)
    print(json.dumps(resp, ensure_ascii=False, sort_keys=True, indent=4, separators=(',', ':')))
```


<span id="faq"></span>
## FAQ

<span id="what-should-i-do-if-i-encounter-the-error-can-t-connect-to-https-url-because-the-ssl-module-is-not-available-when-sending-requests-using-the-python-sdk"></span>
### What should I do if I encounter the error "Can't connect to HTTPS URL because the SSL module is not available" when sending requests using the Python SDK?

Possible cause: The SSL module was not properly installed when installing the Python SDK.

Solution: Reinstall Python and ensure that the SSL module is included during the installation process.
