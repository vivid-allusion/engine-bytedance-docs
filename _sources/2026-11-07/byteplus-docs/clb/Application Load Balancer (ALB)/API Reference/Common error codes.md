---
title: "Common error codes"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Error-codes"
---

This topic introduces common error codes for Application Load Balancer (ALB). For common error codes on the BytePlus platform, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|HTTP Code |Error codes |Error message |Error description |
|---|---|---|---|
| <br><br>400 | <br><br>InvalidParameter | <br><br>Data unmarshal failed |Failed to parse the request. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request does not contain required parameters. Please ensure the request includes all required parameters, such as: %s. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The specified %s parameter format is invalid. |
