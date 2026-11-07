---
title: "Data security (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Data-security-python-sdk"
---

TOS Python SDK supports data security by verifying checksums on the server during upload and on the client after upload.

<span id=".5LiK5Lyg5pe25pyN5Yqh56uv5qCh6aqM"></span>
## server verification during upload

During upload, server verification allows setting a `content-md5` checksum in the request parameters. If the server\-calculated MD5 does not match the one provided, the server returns a 4xx error and the upload fails.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The put_object, append_object, and upload_part interfaces all support setting an MD5 checksum in the request parameters.</div>


<span id=".5LiK5Lyg5ZCO5a6i5oi356uv5qCh6aqM"></span>
## client verification after upload

Client verification after upload can be enabled by setting the `enable_crc` parameter when initializing the client. This verification relies on the server's Crc64 feature. After the request completes, the server returns the Crc64 value of the uploaded data. The client compares this with the locally calculated Crc64 and throws a TosClientError exception if they do not match.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The put_object, append_object, and upload_part interfaces all support Crc64 verification.</div>
