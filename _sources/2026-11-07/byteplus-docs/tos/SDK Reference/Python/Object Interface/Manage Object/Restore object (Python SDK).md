---
title: "Restore object (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Restore-objects-python-sdk"
---

Restore a cold archive object. After restoration, the object can be accessed through the download object interface. You can specify different retrieval methods through parameters.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* The first call to the restore_object interface returns 202. If the file is being restored, calling the restore_object interface again will return a 409 error. If the object has been restored, calling the restore_object interface again will return 200 OK.

* For buckets with versioning enabled, you can restore a specific version of the object by specifying `version_id`. If `version_id` is not specified, the current object is restored by default.


<span id=".56S65L6L5Luj56CB"></span>
## Example code

The following code restores an object.

```python
import os
import tos
from tos.enum import TierType
from tos.models2 import RestoreJobParameters

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"
try:
    # Create a TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)
    client.restore_object(bucket=bucket_name, key=key, days=1,
                          restore_job_parameters=RestoreJobParameters(TierType.Tier_Expedited))
except tos.exceptions.TosClientError as e:
    # Operation failed, catch client error, usually caused by invalid request parameters or network issues
    print('fail with client error, message:{}, cause: {}'.format(e.message, e.cause))
except tos.exceptions.TosServerError as e:
    # Operation failed, catch server error, detailed error information can be obtained from the response
    print('fail with server error, code: {}'.format(e.code))
    # request id can be used to locate specific issues, it is strongly recommended to save it in the log.
    print('error with request id: {}'.format(e.request_id))
    print('error with message: {}'.format(e.message))
    print('error with http code: {}'.format(e.status_code))
    print('error with ec: {}'.format(e.ec))
    print('error with request url: {}'.format(e.request_url))
except Exception as e:
    print('fail with unknown error: {}'.format(e))
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For a detailed description of the restore object interface, see [RestoreObject](https://docs.byteplus.com/docs/tos/reference-restoreobject).
