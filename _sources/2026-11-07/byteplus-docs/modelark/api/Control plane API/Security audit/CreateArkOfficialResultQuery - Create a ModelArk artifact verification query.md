---
title: "CreateArkOfficialResultQuery - Create a ModelArk artifact verification query"
product: "ModelArk"
product_code: "modelark"
source: "https://docs.byteplus.com/en/docs/modelark/create-ark-official-result-query-api"
---

`POST https://ark.ap-southeast-1.byteplusapi.com/?Action=CreateArkOfficialResultQuery&Version=2024-01-01`

Submits content for official ModelArk output verification and returns a query ID for subsequent result polling.

## Authentication

This API supports the following authentication method(s). For details, see [Base URL and authentication](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/base-url-and-authentication).

* Access Key authentication. Go to the [Access Key management](https://console.byteplus.com/iam/keymanage) page. Obtain an Access Key. This API supports only Access Key authentication.

---

## Request parameters

### Body parameters

**Type** `string` `Required`  |  Verification type

The verification type. Set this field to `content_url` to verify an image or video output file by URL.

**ContentURL** `string`  |  Content URL to verify

The URL of the content to verify. When `Type` is `content_url`, provide the URL of an image or video output file.

Image limits:

* File size: no more than 20 MB.

* File formats: `png`, `jpg` (`jpeg`), `heic`, and `webp`.

Video limits:

* File size: no more than 100 MB.

* File formats: `mp4`, `mov`, and `avi`.

## Response parameters

**QueryID** `string`  |  Query ID

The unique ID of this verification query, used in subsequent API calls to retrieve the verification result.
