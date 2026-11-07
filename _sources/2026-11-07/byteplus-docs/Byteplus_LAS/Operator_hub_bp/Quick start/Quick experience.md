---
title: "Quick experience"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Quick_experience"
---

Try out data processing operators within a few minutes.

# Quickly invoke LAS operators

## 1. Obtain and configure LAS API Key

1. After logging in to the LAS console, go to the Operator service  **\>**  API key management page, and click Create API key on the page. Create an API Key as prompted on the interface.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bebbc10d609e45e98ea426ecc8860b4b~tplv-goo7wpa0wc-image.image)

2. Configure environment variables. Run the following command in the terminal to set the API Key as an environment variable.

   ```Bash
   export LAS_API_KEY="<YOUR_API_KEY>"
   ```

## 2. Obtain the Base URL

The Base URL depends on the region of the LAS service you are using. It is recommended to use https://operator.las.ap\-southeast\-1.bytepluses.com consistently when experiencing operator capabilities.

## 3. Send an API request

The following demonstrates a quick experience by calling the Multimodal Deep Thinking (Doubao\-Seed\-1.8) operator. Run the following curl command on your development machine to quickly experience the LAS operator's image understanding processing results.

|Input |Output preview |
|---|---|
|Test image details:<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/53380ea6b5a6413da816785a2760f8d4~tplv-goo7wpa0wc-image.image) |This is an outdoor scene filled with a sense of natural tranquility: |

The operator invocation code is as follows.

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/chat/completions" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{
    "messages": [
        {
            "role": "user",
            "content": [
                {
                    "type": "image_url",
                    "image_url": {
                        "url": "https://ark-project.tos-cn-beijing.volces.com/images/view.jpeg"
                    }
                },
                {
                    "type": "text",
                    "text": "What' s in the picture"
                }
            ]
        }
    ],
    "model": "seed-1-8-251228"
}'
```

# Expand your knowledge

* Business migration: Compatible with OpenAI SDK: OpenAI SDK compatibility note

* Operator categories: LAS provides you with two types of data processing operators: offline and online.

   * Online operators: Invoked directly via the operator API.

   * Offline operators: Invoked using the Daft engine. LAS provides the VeDaft engine, which integrates the SDK for offline operator invocation, enabling more efficient scheduling and execution of batch data processing tasks.

* When calling the official online operator OpenAPI via HTTP, there are two invocation modes: synchronous and asynchronous.

   * Synchronous invocation allows you to request directly and obtain the data processing result in the response.

   * Asynchronous invocation requires submitting a job first, then using the returned job ID to query the job and obtain the business result.
