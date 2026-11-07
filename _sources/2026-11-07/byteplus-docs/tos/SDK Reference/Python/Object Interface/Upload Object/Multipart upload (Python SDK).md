---
title: "Multipart upload (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Shard-upload-python-sdk"
---

For larger objects, you can divide them into multiple data blocks (parts) to upload separately, and finally call complete_multipart_upload to merge the uploaded data blocks into one object.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Before initiating multipart uploads, you must have the `tos: PutObject`permission. For details, see [Overview](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* Before canceling multipart uploads, you must have the `tos: AbortMultipartUpload`permission. For details, see [Overview](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* Part numbers start from 1 and go up to 10,000. Except for the last part, all other parts have a minimum size of 4 MiB.

* When uploading an object, the object name must meet certain specifications. For details, see [Common concepts](https://docs.byteplus.com/docs/tos/docs-common-concepts).

* TOS is a distributed object storage product designed for mass storage. The internal partition stores object index data. In order to scale out the maximum throughput when uploading and downloading objects, and reduce the probability of hot partitions, please avoid using lexicographically increasing object naming.

* If an object with the same name already exists in the bucket, the new object will overwrite the existing object. If versioning is enabled in your bucket, the original object is preserved and a new version number is generated to identify the newly uploaded object.


<span id=".5YiG54mH5LiK5Lyg5q2l6aqk"></span>
## Multipart upload steps

Multipart uploading typically involves the following three steps.


1. Initialize a multipart upload: Call the create_multipart_upload method to return the globally unique upload_id created by TOS.

2. Upload parts: Call upload_part method to upload part data.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For the same multipart upload task (identified by <code>upload_id</code>), the part number ( <code>part_number</code>) identifies the relative position of the part throughout the object. If you upload data multiple times through the same part number, the original data source will be overwritten in TOS, and the last uploaded data shall prevail.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When merging parts, you need to specify all part information (part number, ETag) in the current multipart upload task.   </div>
   

3. Complete the multipart upload: When all parts are uploaded, call complete_multipart_upload method to merge all parts into one complete object.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id=".5YiG54mH5LiK5Lyg5a6M5pW06L-H56iL"></span>
### **Complete multipart upload process**

The following code uploads a local file to the `object-test` object in the target bucket `bucket-test` via multipart upload.

```python
import os

import tos

from tos.utils import SizeAdapter


# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"

# Local file full path, for example usr/local/testfile.txt
file_name = '/usr/local/testfile.txt'
total_size = os.path.getsize(file_name)
part_size = 5 * 1024 * 1024
try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)

    # Initialize upload task
    # If you need to set the storage class of the object during initialization of the multipart upload, you can set it using the storage_class field.
    # If you need to set the object ACL during initialization of the multipart upload, you can set it using the acl and grant_full_control fields.
    multi_result = client.create_multipart_upload(bucket_name, object_key, acl=tos.ACLType.ACL_Public_Read,
                                                  storage_class=tos.StorageClassType.Storage_Class_Standard)

    upload_id = multi_result.upload_id
    parts = []

    # Upload chunk data
    with open(file_name, 'rb') as f:
        part_number = 1
        offset = 0
        while offset < total_size:
            num_to_upload = min(part_size, total_size - offset)
            out = client.upload_part(bucket_name, object_key, upload_id, part_number,
                                     content=SizeAdapter(f, num_to_upload, init_offset=offset))
            parts.append(out)
            offset += num_to_upload
            part_number += 1

    # Complete the chunked upload task.
    client.complete_multipart_upload(bucket_name, object_key, upload_id, parts)
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


<span id=".6L-b5bqm5p2h5aSE55CG"></span>
### **Configure progress bar**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For data in the form of strings, bytes, and local files, progress bar functionality is supported. Data of types such as network streams cannot obtain the size of the uploaded content, so the callback does not return the overall size of the object.</div>


The following code is used to add a progress bar feature to the multipart upload process.

```python
import os

import tos
from tos import DataTransferType
from tos.utils import SizeAdapter, MergeProcess


# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"

# Local file full path, for example usr/local/testfile.txt
file_name = '/usr/local/testfile.txt'
total_size = os.path.getsize(file_name)
part_size = 5 * 1024 * 1024
try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)


    def percentage(consumed_bytes: int, total_bytes: int, rw_once_bytes: int, type: DataTransferType):
        if total_bytes:
            rate = int(100 * float(consumed_bytes) / float(total_bytes))
            print("rate:{}, consumed_bytes:{},total_bytes{}, rw_once_bytes:{}, type:{}".format(rate, consumed_bytes,
                                                                                               total_bytes,
                                                                                               rw_once_bytes, type))


    # Configure the progress bar, which is different from regular uploads as the progress of the multipart upload needs to be aggregated.
    data_transfer_listener = MergeProcess(percentage, total_size, (total_size + part_size - 1) // part_size, 0)
    # Initialize the upload task
    # If you need to set the storage class of the object during the initialization of the parts, you can set it through the storage_class field.
    # If you need to set the object ACL during the initialization of the parts, you can set it through the acl, grant_full_control, and other fields.
    multi_result = client.create_multipart_upload(bucket_name, object_key, acl=tos.ACLType.ACL_Public_Read,
                                                  storage_class=tos.StorageClassType.Storage_Class_Standard)

    upload_id = multi_result.upload_id
    parts = []

    # Upload chunk data.
    with open(file_name, 'rb') as f:
        part_number = 1
        offset = 0
        while offset < total_size:
            num_to_upload = min(part_size, total_size - offset)
            out = client.upload_part(bucket_name, object_key, upload_id, part_number,
                                     content=SizeAdapter(f, num_to_upload, init_offset=offset),
                                     data_transfer_listener=data_transfer_listener)
            parts.append(out)
            offset += num_to_upload
            part_number += 1

    # Complete the chunked upload task.
    client.complete_multipart_upload(bucket_name, object_key, upload_id, parts)
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


<span id=".5Y-W5raI5YiG54mH5LiK5Lyg5Lu75Yqh"></span>
### **Cancel multipart uploads**

You can cancel multipart uploads using abort_multipart_upload. When a multipart upload is cancelled, TOS will delete the uploaded part data, and you can no longer perform any operations on the task.

The following code cancels the multipart upload task for the object `object-test` in `bucket-test`.

```python
import os
import tos


# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"
# The upload_id returned by the create_multipart_upload API.
upload_id = "your upload id"
try:
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Cancel the multipart upload event for the specified upload_id, and the uploaded parts will be deleted.
    client.abort_multipart_upload(bucket_name, object_key, upload_id)
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


<span id=".5YiX5Li-5bey5LiK5Lyg55qE5YiG54mH5L-h5oGv"></span>
### **List uploaded parts**

The following code lists the uploaded parts of the object `object-test` in `bucket-test`.

```python
import os
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"
# The upload_id returned by the create_multipart_upload API.
upload_id = "upload_id"
try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)

    # List the uploaded parts information corresponding to the specified upload_id.
    truncated = True
    marker = 0
    while truncated:
        # part_number_marker specifies the starting position of the chunk upload
        # is_truncated is True indicates that there are still unfinished chunks to be listed
        out = client.list_parts(bucket_name, object_key, upload_id, part_number_marker=marker)
        for part in out.parts:
            print('part_number:', part.part_number)
            print('etag:', part.etag)
            print('size', part.size)
        marker = out.next_part_number_marker
        truncated = out.is_truncated
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
## **Related documentation**


* For API documentation on creating a multipart upload task, see [CreateMultipartUpload](https://docs.byteplus.com/docs/tos/reference-createmultipartupload).

* For API documentation on uploading parts, see [UploadPart](https://docs.byteplus.com/docs/tos/reference-uploadpart).

* For API documentation on merging parts, see [CompleteMultipartUpload](https://docs.byteplus.com/docs/tos/reference-completemultipartupload).

* For API documentation on canceling multipart upload tasks, see [AbortMultipartUpload](https://docs.byteplus.com/docs/tos/reference-abortmultipartupload).
