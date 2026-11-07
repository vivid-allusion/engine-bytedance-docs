---
title: "Manage website configuration (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-website-configuration-python-sdk"
---

TOS supports hosting static websites. You can store all the content of a static website in a TOS bucket. After configuring static website rules, you can access the website through the bucket domain name.

<span id=".6K6-572u572R56uZ6YWN572u6KeE5YiZ"></span>
## Set up website configuration rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Only one static website hosting rule can be created in a bucket.</div>


* <div data-tips="true" data-tips-type="warning">After setting up a static website, a custom domain name must be bound to take effect.</div>


* <div data-tips="true" data-tips-type="warning">For security compliance reasons, starting from October 18, 2022, if you use the default domain name of the bucket to access the webpage type file (mimetype is text/html, the extension includes HTM, HTML, JSP, PLG, HTX, STM), the Response Header will automatically add <code>Content-Disposition: attachment</code>, that is, when accessing the webpage type file from the browser, the website will not be previewed directly, but the content of the website will be downloaded locally.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to redirect all requests to another site.

```python
import os
import tos

from tos.models2 import RedirectAllRequestsTo

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"

try:
    # Create TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Scenario 1: Redirect all requests to another site
    redirect_all_requests_to = RedirectAllRequestsTo('www.example.com', 'http')
    client.put_bucket_website(bucket_name, redirect_all_requests_to)
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


The following code is used to set specific redirection rules to redirect specific requests.

```python
import os
import tos

from tos import ProtocolType
from tos.models2 import IndexDocument, ErrorDocument, RoutingRule, RoutingRuleCondition, \
    RoutingRuleRedirect, RoutingRules

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
try:
    # Create TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Scenario 2: Set specific redirect rules to redirect specific requests
    # Set IndexDocument
    index_document = IndexDocument(
        # When the object name is empty or ends with "/", access the index.html in that directory.
        suffix='index.html'
    )
    # ErrorDocument Configuration
    # Specify the error file to return when accessing unauthorized files or non-existent files
    error_document = ErrorDocument('error.html')

    # RoutingRules Configuration, prefix matching, retrieve redirect results
    rule = RoutingRule(
        condition=RoutingRuleCondition(key_prefix_equals='prefix'),
        redirect=RoutingRuleRedirect(protocol=ProtocolType.Protocol_Http, host_name='www.redirect.com')
    )
    routing_rules = RoutingRules([rule])
    client.put_bucket_website(bucket_name, index_document=index_document, error_document=error_document,
                              routing_rules=routing_rules)
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


<span id=".6I635Y-W572R56uZ6YWN572u6KeE5YiZ"></span>
## Get website configuration rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To get the bucket's site configuration rules, by default you must be the bucket owner.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to obtain the site configuration rules for `bucket-test`.

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
    out = client.get_bucket_website(bucket_name)
    if out.redirect_all_requests_to:
        # Print RedirectAllRequestsTo related information.
        print('redirect all host name', out.redirect_all_requests_to.host_name)
        print('redirect all protocol', out.redirect_all_requests_to.protocol)
    if out.index_document:
        print('index document suffix', out.index_document.suffix)
        print('index document forbidden sub dir', out.index_document.forbidden_sub_dir)
    if out.error_document:
        print('error document key', out.error_document.key)
    if out.routing_rules:
        for rule in out.routing_rules:
            if rule.condition:
                print('condition by prefix', rule.condition.key_prefix_equals)
                print('condition by http error code', rule.condition.http_error_code_returned_equals)
            if rule.redirect:
                print('redirect host name', rule.redirect.host_name)
                print('redirect host name', rule.redirect.protocol)
                print('redirect code', rule.redirect.http_redirect_code)
                print('redirect replace key with', rule.redirect.replace_key_with)
                print('redirect replace key prefix with', rule.redirect.replace_key_prefix_with)
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


<span id=".5Yig6Zmk572R56uZ6YWN572u6KeE5YiZ"></span>
## Delete website configuration rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To remove a bucket's site configuration rule, you must be the bucket owner by default.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code removes the site configuration rule for `bucket-test`.

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
    client.delete_bucket_website(bucket_name)
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
