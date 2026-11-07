---
title: "Quick start (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Quick-start-python-sdk"
---

This article explains how to use the TOS Python SDK to perform common operations such as creating buckets, uploading objects, downloading objects, and deleting objects.

<span id="36f9f34a"></span>
## Notice

In multi\-process scenarios, create a separate TosClient for each process. Do not share the same TosClient across processes to avoid concurrency and data corruption issues in read/write requests.

<span id=".5a6J6KOF5ZKM5Yid5aeL5YyW"></span>
## Installation and initialization

<span id=".5a6J6KOFLXB5dGhvbi1kZXZlbA=="></span>
### Install python\-devel

You need to install the python\-devel package.

The TOS Python SDK relies on crcmod to calculate CRC checksums. The C extension mode of crcmod depends on the Python.h file from the python\-devel package. If Python.h is missing, crcmod’s C extension mode installation fails, causing crcmod to run in pure Python mode. The pure Python mode has much lower CRC calculation performance than the C extension mode, resulting in inefficient upload and download operations.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If enabling CRC checksum causes poor upload or download performance, you can disable CRC64 checksum.</div>


<span id=".6aqM6K-BLWNyY21vZC3mqKHlvI8="></span>
### Verify crcmod mode

Enter the Python environment and type `import crcmod._crcfunext`.


* If the following error message appears, it means the C extension mode of the crcmod library failed to install; the crcmod library is operating in pure Python mode. The reason is that when compiling crcmod, _crcfunext.so depends on the Python.h file, which is missing in the system, causing the _crcfunext.so library to fail to generate.


```Plain
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
ImportError: No module named _crcfunext
```



* If no error message appears, it means the C extension mode of the crcmod library installed successfully.


If an error appears, you can resolve it as follows:


1. Uninstall crcmod.

   ```Plain
   pip uninstall crcmod
   ```
   

2. Install python\-devel.

   * If you are using Windows or Mac OS X, the Python\-dependent header files install automatically with Python, so you do not need to install python\-devel.

   * If you are using CentOS, RHEL, or Fedora, you can install it using the following command:

      ```Plain
      # Python2.x version
      yum install python-devel
      
      # Python3.x version
      yum install python3-devel
      ```
      

   * If you use Debian or Ubuntu, install it with the following command:

      ```Plain
      # Python2.x version
      apt-get install python-dev
      
      # Python3.x version
      apt-get install python3-dev
      ```
      

3. Reinstall crcmod.

   ```Plain
   pip install crcmod
   ```
   


<span id=".5a6i5oi356uv6YCa55So56S65L6L"></span>
## Client general example

The following code is a general template using the TOS Python SDK.

```python
import os
import tos

# Obtain AK and SK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket = "bucket-test"
key = "object-test"
data = "Hello world"

try:
    # Create a TosClientV2 object
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Call the API to request TOS service, for example, uploading an object
    resp = client.put_object(bucket, key, content=data)
    print('success, request id {}'.format(resp.request_id))
except tos.exceptions.TosClientError as e:
    #  Operation failed, client exception caught, usually due to invalid request parameters or network issues
    print('fail with client error, message:{}, cause: {}'.format(e.message, e.cause))
except tos.exceptions.TosServerError as e:
    # Operation failed, server exception caught, detailed error information can be obtained from the response
    print('fail with server error, code: {}'.format(e.code))
    # The request ID can be used to pinpoint specific issues; it is highly recommended to log and store it
    print('error with request id: {}'.format(e.request_id))
    print('error with message: {}'.format(e.message))
    print('error with http code: {}'.format(e.status_code))
    print('error with ec: {}'.format(e.ec))
    print('error with request url: {}'.format(e.request_url))
except Exception as e:
    print('fail with unknown error: {}'.format(e))
```


<span id=".5Yib5bu65qG2"></span>
## Create a bucket

A bucket is a globally unique namespace in TOS, acting as a container to store object data. The following code creates a new bucket named `bucket-test`.

```python
import os
import tos

# Obtain AK and SK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
key = "object-test"
data = "Hello world"

try:
    # Create a TosClientV2 object; operations on buckets and objects are all performed through TosClientV2
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Set the bucket's access permissions to private (private read and write)
    client.create_bucket(bucket_name, acl=tos.ACLType.ACL_Private)
except tos.exceptions.TosClientError as e:
    # Operation failed, client exception caught, usually due to invalid request parameters or network issues
    print('fail with client error, message:{}, cause: {}'.format(e.message, e.cause))
except tos.exceptions.TosServerError as e:
    # Operation failed, server exception caught, detailed error information can be obtained from the response
    print('fail with server error, code: {}'.format(e.code))
    # The request ID can be used to pinpoint specific issues; it is highly recommended to log and store it
    print('error with request id: {}'.format(e.request_id))
    print('error with message: {}'.format(e.message))
    print('error with http code: {}'.format(e.status_code))
    print('error with ec: {}'.format(e.ec))
    print('error with request url: {}'.format(e.request_url))
except Exception as e:
    print('fail with unknown error: {}'.format(e))
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information on creating buckets, see <a href="https://docs.byteplus.com/docs/tos/Create-a-bucket-python-sdk">Create a bucket</a>.</div>


<span id=".5LiK5Lyg5a-56LGh"></span>
## Upload an object

After successfully creating a new bucket, you can upload objects to it. The following code uploads a string to the TOS bucket `bucket-test`.

```python
import os
import tos

# Obtain AK and SK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"

try:
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Add Object via string
    client.put_object(bucket_name, object_key, content='Hello World')
except tos.exceptions.TosClientError as e:
    # Operation failed, client exception caught, usually due to invalid request parameters or network issues
    print('fail with client error, message:{}, cause: {}'.format(e.message, e.cause))
except tos.exceptions.TosServerError as e:
    # Operation failed, server exception caught, detailed error information can be obtained from the response
    print('fail with server error, code: {}'.format(e.code))
    # The request ID can be used to pinpoint specific issues; it is highly recommended to log and store it
    print('error with request id: {}'.format(e.request_id))
    print('error with message: {}'.format(e.message))
    print('error with http code: {}'.format(e.status_code))
    print('error with ec: {}'.format(e.ec))
    print('error with request url: {}'.format(e.request_url))
except Exception as e:
    print('fail with unknown error: {}'.format(e))
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more example links about uploading objects, see <a href="https://docs.byteplus.com/docs/tos/Normal-upload-python-sdk">Uploading Objects</a>.</div>


<span id=".5LiL6L295a-56LGh"></span>
## Downloading objects

The following code downloads the specified TOS object into memory.

```python
import os
import tos

# Obtain AK and SK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"

try:
    # Create a TosClientV2 object; operations on buckets and objects are all performed through TosClientV2
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Download the object into memory
    object_stream = client.get_object(bucket_name, object_key)
    # object_stream is an iterator for reading data iteratively
    # for content in object_stream:
    #     print(content)
    # You can also call the read() method to retrieve the complete data in memory at once
    print(object_stream.read())
except tos.exceptions.TosClientError as e:
    # Operation failed, client exception caught, usually due to invalid request parameters or network issues
    print('fail with client error, message:{}, cause: {}'.format(e.message, e.cause))
except tos.exceptions.TosServerError as e:
    # Operation failed, server exception caught, detailed error information can be obtained from the response
    print('fail with server error, code: {}'.format(e.code))
    # The request ID can be used to pinpoint specific issues; it is highly recommended to log and store it
    print('error with request id: {}'.format(e.request_id))
    print('error with message: {}'.format(e.message))
    print('error with http code: {}'.format(e.status_code))
    print('error with ec: {}'.format(e.ec))
    print('error with request url: {}'.format(e.request_url))
except Exception as e:
    print('fail with unknown error: {}'.format(e))
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more example links about downloading objects, see <a href="https://docs.byteplus.com/docs/tos/Normal-download-python-sdk">Downloading Objects</a>.</div>


<span id=".5YiX5Li-5a-56LGh"></span>
## Listing objects

The following code lists objects in the specified bucket `bucket-test`, listing up to 2,000 objects.

```python
import os
import tos

# Obtain AK and SK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"

try:
    # Create a TosClientV2 object; operations on buckets and objects are all performed through TosClientV2
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # By default, up to 1,000 objects are listed per request
    list_out_1 = client.list_objects(bucket_name)
    for ob in list_out_1.contents:
        print(ob.key)

    # If not all objects have been listed, you can continue listing by setting the optional parameter 'marker'
    if list_out_1.is_truncated:
        list_out_2 = client.list_objects(bucket_name, marker=list_out_1.next_marker)
        for ob in list_out_2.contents:
            print(ob.key)
except tos.exceptions.TosClientError as e:
    # Operation failed, client exception caught, usually due to invalid request parameters or network issues
    print('fail with client error, message:{}, cause: {}'.format(e.message, e.cause))
except tos.exceptions.TosServerError as e:
    # Operation failed, server exception caught, detailed error information can be obtained from the response
    print('fail with server error, code: {}'.format(e.code))
    # The request ID can be used to pinpoint specific issues; it is highly recommended to log and store it
    print('error with request id: {}'.format(e.request_id))
    print('error with message: {}'.format(e.message))
    print('error with http code: {}'.format(e.status_code))
    print('error with ec: {}'.format(e.ec))
    print('error with request url: {}'.format(e.request_url))
except Exception as e:
    print('fail with unknown error: {}'.format(e))
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more example links about listing objects, see <a href="https://docs.byteplus.com/docs/tos/List-objects-python-sdk">Listing Objects</a>.</div>


<span id=".5Yig6Zmk5a-56LGh"></span>
## Deleting objects

The following code deletes the object `object-test` from the specified bucket `bucket-test`.

```python
import os
import tos

# Obtain AK and SK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"

try:
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Delete an object from the bucket
    client.delete_object(bucket_name, object_key)
except tos.exceptions.TosClientError as e:
    # Operation failed, client exception caught, usually due to invalid request parameters or network issues
    print('fail with client error, message:{}, cause: {}'.format(e.message, e.cause))
except tos.exceptions.TosServerError as e:
    # Operation failed, server exception caught, detailed error information can be obtained from the response
    print('fail with server error, code: {}'.format(e.code))
    # The request ID can be used to pinpoint specific issues; it is highly recommended to log and store it
    print('error with request id: {}'.format(e.request_id))
    print('error with message: {}'.format(e.message))
    print('error with http code: {}'.format(e.status_code))
    print('error with ec: {}'.format(e.ec))
    print('error with request url: {}'.format(e.request_url))
except Exception as e:
    print('fail with unknown error: {}'.format(e))
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more example links about deleting objects, see <a href="https://docs.byteplus.com/docs/tos/Delete-objects-python-sdk">Deleting Objects</a>.</div>


<span id=".5YWz6ZetLXRvc2NsaWVudA=="></span>
## Close TosClient

The TOS Python SDK enables persistent connections by default. When you create multiple TosClient instances to access TOS, use the following code to close unused TosClient instances and release connection resources.

```python
import os
import tos

# Obtain AK and SK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"

try:
    # Create a TosClientV2 object; operations on buckets and objects are all performed through TosClientV2
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # After performing the relevant operations, close the TosClient when it is no longer needed
    client.close()
except tos.exceptions.TosClientError as e:
    # Operation failed, client exception caught, usually due to invalid request parameters or network issues
    print('fail with client error, message:{}, cause: {}'.format(e.message, e.cause))
except tos.exceptions.TosServerError as e:
    # Operation failed, server exception caught, detailed error information can be obtained from the response
    print('fail with server error, code: {}'.format(e.code))
    # The request ID can be used to pinpoint specific issues; it is highly recommended to log and store it
    print('error with request id: {}'.format(e.request_id))
    print('error with message: {}'.format(e.message))
    print('error with http code: {}'.format(e.status_code))
    print('error with ec: {}'.format(e.ec))
    print('error with request url: {}'.format(e.request_url))
except Exception as e:
    print('fail with unknown error: {}'.format(e))
```
