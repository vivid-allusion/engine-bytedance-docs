---
title: "Response examples"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/Response_examples"
---

**Response status codes**

The HTTP status code 200 indicates a successful API request. A 4xx or 5xx HTTP status code indicates a failed API request. To check whether the response contains abnormal results, check whether the [ResponseMetadata](https://docs.byteplus.com/en/docs/kms/ResponseMetadata) structure in the response contains the [Error](https://docs.byteplus.com/en/docs/kms/Error) field. If this field exists, an error occurs during the API call.

**Response examples**


* Example of a normal response


```Plain Text
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DescribeKeys",
        "Version": "2021-02-18",
        "Service": "kms",
        "Region": "cn-north-1"
        }，
    "Result": {
            ......
    }
}

```



* Example of an unexpected response


```Plain Text
{
    "ResponseMetadata": {
        "RequestId": "2021080519374301022514515201DBC0DD",
        "Action": "UpdateKeyring",
        "Version": "2021-02-18",
        "Service": "kms",
        "Region": "cn-north-1",
        "Error": {
            "Code": "Not Found",
            "Message": "Not found keyring [demo_keyring11111]."
        }
    }
}

```
