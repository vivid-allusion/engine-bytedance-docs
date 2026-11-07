---
title: "Data Security (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Data-security-c-sdk"
---

The TOS C++ SDK supports data validation, including server\-side validation during upload and client\-side validation after upload, thereby ensuring data security during both upload and download operations.

<span id=".5LiK5Lyg5pe25pyN5Yqh56uv5qCh6aqM"></span>
## Server\-Side Validation During Upload

This feature primarily relies on the server's data validation capability. You can specify the content\-md5 checksum value for the data in the request parameters. If the MD5 value calculated by the server does not match the value provided in the request, the server will immediately return a 4xx error, and the upload will fail.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The putObject, appendObject, and uploadPart interfaces all support specifying an MD5 checksum value in the request parameters.</div>


<span id=".5LiK5Lyg5ZCO5a6i5oi356uv5qCh6aqM"></span>
## Client\-side validation after upload

Client\-side verification after uploading can be enabled during client initialization by setting the enableCRC parameter. Relying on the server\-side Crc64 feature, after the API request is completed, the server returns the Crc64 value of the uploaded data. At this point, the locally computed Crc64 is compared with the value returned by the server. If they do not match, an error code and error message are returned.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The putObject, appendObject, and uploadPart interfaces all support Crc64 verification.</div>
