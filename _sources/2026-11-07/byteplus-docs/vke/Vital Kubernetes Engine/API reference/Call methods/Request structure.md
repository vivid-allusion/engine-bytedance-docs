---
title: "Request structure"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Request-structure"
---

When you call APIs of BytePlus, requests are sent to the specified service addresses, which must meet the signature requirements of BytePlus and contain the business information specific to the APIs.

The following content describes the request structure of BytePlus APIs.

<span id=".5pyN5Yqh5Zyw5Z2A"></span>
## Service addresses

The API address varies based on different regions. For details, see [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses).

<span id=".6YCa5L-h5Y2P6K6u"></span>
## Communication protocols

All APIs send requests by using HTTPS, which provides a highly secure communication channel.

<span id=".6K-35rGC5pa55rOV"></span>
## Request methods

APIs only support **POST** requests.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When you use the POST method, <code>Action</code> and <code>Version</code> in the public parameters must be placed in the <code>Query String</code>.</div>


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The API requests of BytePlus consist of two types of parameters:


* Public request parameters: the request parameters that are required for each API. For more details, please refer to the [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters) documentation.

* API request parameters: the request parameters specific to each API. For detailed information, see the corresponding API documentation.


<span id=".5a2X56ym57yW56CB"></span>
## Character encoding

Both the request and response results are encoded using the UTF\-8 character set.
