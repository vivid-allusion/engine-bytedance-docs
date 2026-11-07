---
title: "Manage mirroring rules (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-image-return-to-source-python-sdk"
---

Mirror\-based back\-to\-origin (mirroring) is mainly used for scenarios where data is seamlessly migrated to TOS. For example, the web service runs on a user\-built origin server. To migrate the static web page to TOS, the user can configure a mirroring rule to retrieve data not yet migrated to TOS.

<span id=".6K6-572u6ZWc5YOP5Zue5rqQ6KeE5YiZ"></span>
## Set mirroring rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To set mirroring rules for a bucket, you must be the bucket owner.</div>


* <div data-tips="true" data-tips-type="warning">A bucket only supports the creation of one back\-to\-origin rule.</div>


* <div data-tips="true" data-tips-type="warning">Mirroring supports requesting an object of up to 5 GiB. To request an object larger than 5 GiB, use the Get Range feature.</div>


* <div data-tips="true" data-tips-type="warning">Redirect\-based back\-to\-origin (redirection) supports requesting an object of up to 300 GiB.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code sets the mirroring rule for the bucket `bucket-test`.

```python
import os
import tos
from tos import RedirectType
from tos.models2 import Rule, Condition, Redirect, PublicSource, SourceEndpoint, MirrorHeader
# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"

try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)

    # Specified headers carried by the image back to the source.
    mirror_header = MirrorHeader(pass_all=True, pass_headers=['pass_header1', 'pass_header2'],
                                 remove=['remove_header1', 'remove_header2'])
    # Set the origin retrieval conditions.
    condition = Condition(http_code=404)
    # The action performed after setting.
    redirect = Redirect(redirect_type=RedirectType.Mirror,
                        # When fetch_source_on_redirect=True, it indicates whether to fetch information from the configured origin server after redirection.
                        fetch_source_on_redirect=True,
                        # Configure the publicly accessible source endpoint
                        public_source=PublicSource(SourceEndpoint(primary=['http://test.com/obj/tostest/'])),
                        # When pass_query=True, carry the request parameters when executing redirect or mirror origin rules.
                        pass_query=True,
                        # When follow_redirect=True, the result obtained from mirror origin will continue to redirect to the specified Location to obtain data if it is 3xx.
                        follow_redirect=True,
                        # Configure the headers to carry during origin retrieval.
                        mirror_header=mirror_header)

    rule = Rule(id='1', condition=condition, redirect=redirect)
    client.put_bucket_mirror_back(bucket_name, [rule])
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


<span id=".6I635Y-W6ZWc5YOP5Zue5rqQ6KeE5YiZ"></span>
## Get mirroring rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To get the mirroring rule for a bucket, you must be the bucket owner.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to get the mirroring rule for `bucket-test`.

```python
import os
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"

try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)

    rules = client.get_bucket_mirror_back(bucket_name)
    for rule in rules.rules:
        print('id', rule.id)
        print('condition_http_code', rule.condition.http_code)
        print('redirect_redirect_type', rule.redirect.redirect_type.value)
        print('redirect_follow_redirect', rule.redirect.follow_redirect)
        print('redirect_fetch_source_on_redirect', rule.redirect.fetch_source_on_redirect)
        print('source_endpoint', rule.redirect.public_source.source_endpoint.primary)
        print('redirect_pass_query', rule.redirect.pass_query)
        print('pass_all', rule.redirect.mirror_header.pass_all)
        if rule.redirect.mirror_header.pass_headers is not None:
            for header in rule.redirect.mirror_header.pass_headers:
                print('pass_header', header)
        if rule.redirect.mirror_header.remove is not None:
            for header in rule.redirect.mirror_header.remove:
                print('remove_header', header)
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


<span id=".5Yig6Zmk5qG255qE6ZWc5YOP5Zue5rqQ6KeE5YiZ"></span>
## Remove mirroring rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To remove a bucket's mirroring rule, you must be the bucket owner.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code removes the mirroring rule for ` bucket-test`.

```python
import os
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"

try:
    # Create a TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Delete the mirror source rule for a bucket
    client.delete_bucket_mirror_back(bucket_name)
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

For more information on mirror\-based back\-to\-origin, see [Setting back-to-origin rules](https://docs.byteplus.com/docs/tos/docs-setting-back-to-origin-rules).
