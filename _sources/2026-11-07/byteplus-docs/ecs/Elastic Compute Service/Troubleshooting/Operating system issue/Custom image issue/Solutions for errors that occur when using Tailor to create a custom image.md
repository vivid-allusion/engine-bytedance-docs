---
title: "Solutions for errors that occur when using Tailor to create a custom image"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Solutions_for_errors_when_using_Tailor_to_create_a_Custom_Image"
---

<span id=".5L2_55SoVGFpbG9y5Yib5bu66Ieq5a6a5LmJ6ZWc5YOP5pe277yM5Ye6546w4oCcWW91IG5lZWQgc3BlY2lmeSBZb3VyIEFLJlNLIG9mIHZvbGMhIeKAnemUmeivr-WmguS9leino-WGs--8nw=="></span>
### How to resolve the "You need specify Your AK&SK of volc!!" error when I use Tailor to create a custom image?

Before you use Tailor, you need to execute the following commands to import the Access Key ID (AK for short) and Secret Access Key (SK for short) of the account that owns the base image. For more information, see the User guide.

```Plain Text
export VOLC_AK=xxx 
export VOLC_SK=xxx
```


<span id=".5L2_55SoVGFpbG9y5Yib5bu66Ieq5a6a5LmJ6ZWc5YOP5pe277yM5Ye6546w4oCcVGhlIHNwZWNpZmllZCBzeXN0ZW0gdm9sdW1lIHNpemUgZXhjZWVkcyB0aGUgbGltaXQu4oCd6ZSZ6K-v5aaC5L2V6Kej5Yaz77yf"></span>
### How to resolve the "The specified system volume size exceeds the limit." error when I use Tailor to create a custom image?

The value you specified for the `disksize` (image size) parameter does not comply with the BytePlus instance specification standards. Modify the parameter value.

<span id=".5L2_55SoVGFpbG9y5Yib5bu66Ieq5a6a5LmJ6ZWc5YOP5pe277yM5Ye6546w4oCcVGhlIHNwZWNpZmllZCBpbWFnZSBhbmQgaW5zdGFuY2UgdHlwZSBkbyBub3QgbWF0Y2gu4oCd6ZSZ6K-v5aaC5L2V6Kej5Yaz77yf"></span>
### How to resolve the "The specified image and instance type do not match." error when I use Tailor to create a custom image?

The `spec` (temporary instance specification) you specified does not support the use of the `base` base image. Modify the instance specification or the base image.

<span id=".5L2_55SoVGFpbG9y5Yib5bu66Ieq5a6a5LmJ6ZWc5YOP5pe277yM5Ye6546w4oCcQ3JlYXRlIHh4eCBmYWlsZWQgd2l0aCBlcnI6IFF1b3RhRXhjZWVkZWQuWHh4OiBYWFggbnVtYmVyIGV4Y2VlZGVkIHF1b3RhLiBzdGF0dXMgY29kZTogNDAwLCByZXF1ZXN0IGlkOlhYWFhYWFhYWFhYWFhY4oCd6ZSZ6K-v5aaC5L2V6Kej5Yaz77yf"></span>
### How to resolve the "Create xxx failed with err: QuotaExceeded.Xxx: XXX number exceeded quota. status code: 400, request id:XXXXXXXXXXXXXX" error when I use Tailor to create a custom image?

Creation of the corresponding resources failed due to some resources being insufficient.
