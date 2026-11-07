---
title: "Obtain the Base URL"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Obtain_the_Base_URL"
---

To invoke online operators, you must first determine the Base URL for operator invocation based on the region where your current LAS service is deployed. This is required to configure the path parameter value for operator invocation. This document provides the Base URL information for each region.

# Invoke operators via the public URL

|Region |Region ID |Base URL |Operator invocation path example |
|---|---|---|---|
|Asia Pacific (Johor) |ap\-southeast\-1 |https://operator.las.ap\-southeast\-1.bytepluses.com |https://operator.las.ap\-southeast\-1.bytepluses.com/api/v1/process |

# Invoke operators via the internal network on the LAS development machine

When using the LAS development machine to invoke LAS operators, you can directly use the preset Base URL environment variable to invoke operators. Using the internal network environment is more stable when submitting operator processing tasks in batches than using the public URL.

|Details |Detailed explanation |
|---|---|
|Preset Base URL environment variable |`$LAS_BASE_URL`<br><br><br>* The LAS development machine has preset a Base URL environment variable for the operator API. When invoking operators on the development machine, you can reference it directly in the operator API invocation code.<br><br>* This environment variable automatically selects the appropriate internal network Base URL based on your region and queue resource type, making it more convenient and stable to submit operator tasks on the development machine. |
|Operator invocation path example |`$LAS_BASE_URL/api/v1/chat/completions` |
|Examples |The following uses an operator task as an example to demonstrate how to use the environment variable to invoke operators when using the development machine.<br><br>```JSON```<br>```curl --location "$LAS_BASE_URL/api/v1/chat/completions" \```<br>```--header "Content-Type: application/json" \```<br>```--header "Authorization: Bearer $LAS_API_KEY" \```<br>```--data '{```<br>```    "messages": [```<br>```        {```<br>```            "role": "user",```<br>```            "content": [```<br>```                {```<br>```                    "type": "image_url",```<br>```                    "image_url": {```<br>```                        "url": "https://example-bucket.tos-ap-southeast-1.bytepluses.com/images/view.jpeg"```<br>```                    }```<br>```                },```<br>```                {```<br>```                    "type": "text",```<br>```                    "text": "What is in this image?"```<br>```                }```<br>```            ]```<br>```        }```<br>```    ],```<br>```    "model": "doubao-seed-1-8-251228"```<br>```}'```<br> |
