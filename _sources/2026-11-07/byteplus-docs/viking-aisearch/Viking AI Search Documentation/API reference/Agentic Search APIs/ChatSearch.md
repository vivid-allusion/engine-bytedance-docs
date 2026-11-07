---
title: "ChatSearch"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/ChatSearch"
---

***Viking AI Search*** * is an enterprise\-grade AI search product powered by generative AI. It combines the multimodal semantic representation and understanding of large models with ByteDance's best practices in information retrieval to provide an out\-of\-the\-box AI search platform service. This service helps customers easily build and integrate end\-to\-end multimodal search and recommendation capabilities for text and images.* 


---



Based on chat content, this feature dynamically handles intents such as small talk, refusal to answer, and search. It provides appropriate user responses while also calling the search function to return retrieved item data.

When using the Chat Search feature, you need to maintain a unique session identifier. You can upload the session_id with each call:


* Upload a new session_id: starts a new session by default.

* Upload an existing session_id: the system automatically retrieves the session history and continues to process the user query based on the historical context.


<span id="4524ac0e"></span>
# Notes


* **Usage Limits:** 

   * Due to the HTTP body size limit, the maximum request body size is 10 MB.

* **Response Format**

   * The chat API returns responses in a streaming format. Clients must parse the streamed response when making API calls.


<span id="c85dbbc7"></span>
# Request URL


* Request method: POST

* Request URL:



|**Service** |**Region** |**URL** |
|---|---|---|
|BytePlus |Asia\-Pacific (Johor) |`https://aisearch.ap-southeast-1.bytepluses.com/api/v1/application/{application_id}/chat_search` |
|Volcano Engine |North China (Beijing) |`https://aisearch.cn-beijing.volces.com/api/v1/application/{application_id}/chat_search` |
|Volcano Engine |Asia\-Pacific (Johor) |`https://aisearch.cn-beijing.volces.com/api/v1/application/{application_id}/chat_search` |


`{application_id}`: The unique identifier for your application, which is assigned after creation and can be found in the console.

<span id="054142fe"></span>
# Authentication Method

Authenticate with an API Key or Access Key. For more information, see [API Authentication](https://www.volcengine.com/docs/85296/1544950).

<span id="06cac2ca"></span>
# Send a Chat Request

<span id="14b90719"></span>
## Start a conversation directly


<columns>
<columnsItem zoneid="syet6joeYW">

&nbsp;

**session_id  ** `String` `Required`

A unique identifier for a session, used to link the user's chat history for the current conversation. A new session_id is required when starting a new conversation.

**input_message ** `Object` `Required`

The user's input for the current conversation in the session:


* **content ** `List [Object]` `Required`

   The user's input as images or text. It can contain multiple content elements with the following parameters:

* **type ** `String` `Required`

   The type of a content element. The following enum values can be passed:

   * "text": The element is text information.

   * "image_url": The element is an image.

* **text ** `String` `Required when the content element is text`

   When the content element is text, pass the user input as a string.

* **image_url ** `Object` `Required when the content element is an image.`

   The input image content.

   * **url ** `String` `Required.`

      The image file, uploaded as a base64\-encoded string (supports bitmap formats).


**user ** `Object`

The user information for the current conversation. Currently supports user ID and nickname. Uploading user information is recommended. User interactions are saved to the user profile as personalized memories, and preferences reflected in the conversation are used for personalized recommendations.


*  **_user_id ** `String`

   The unique identifier for the user.

* **nickname ** `String`

   User nickname, used to generate a welcome message when a conversation starts.


**enable_suggestions ** `Boolean`

Determines whether to suggest follow\-up questions after generating a response.

`true`: enable suggested questions.

`false`: disable suggested questions. The default is `false`.

**reply_mode** `String`

The selected reply mode, which controls the underlying model used for the current conversation to balance between reply effectiveness and response speed. The following enumerated values can be passed:

`balanced`: Balanced mode. Uses a model with better performance, featuring higher retrieval accuracy and reply generation quality, with a relatively slower response speed.

`fast`: Fast mode. Uses a faster model with lower response latency, but its retrieval accuracy and generation effectiveness are inferior to those of Balanced mode.

If this parameter is not passed, the default value is "balanced".

**opening_remarks ** `Boolean`

Determines whether to trigger a welcome message when a conversation starts.

`true: `enable. When enabled, this follows the "Conversation Start Settings" in the console. If startup recommendations are configured, a welcome message with recommended content is displayed. If no recommendations are configured, your defined welcome message is displayed.

`false: `disable. Defaults to `false`

For usage details, see: [Greet users when starting a conversation](https://docs.byteplus.com/docs/viking-aisearch/ChatSearch#68777956)

**search_param  ** `Object`

Specify search parameters, such as the dataset scope and filter conditions, for searching datasets in the current conversation.


* **page_size ** `Integer`

   The number of items to return in the conversation when a search is triggered. Defaults to 30 if not provided.

* **dataset_ids ** `List[String]`

   When an app is configured to search multiple datasets, you can specify the scope for the conversation by passing a list of searchable `Dataset IDs`. For example, ["0999281902", "099281972"]. If not specified, all datasets associated with the app are searched by default.

* **filters ** `Map < dataset id, filter object>`

   Specifies the filter conditions for searching a dataset in a conversation. These conditions are passed as a map where the key is the dataset ID string, and the value is the filter expression object. For example:


```JSON
"filters":{
    "0999281902":{
        "op":"must",
        "field":"parent_content_id",
        "conds":[""]
    }
}
```


For more examples, see: [AI Search: Filter](https://docs.byteplus.com/docs/viking-aisearch/AI_search_filter)


* **output_fields ** `Object`

   Specifies which fields from the item dataset to return in the API response. This includes fields shown in search tool results and the `related_items` list returned after a conversation ends.

   The input is a Map object.

   * key: Data source ID (String)

   * value: A list of fields to return from this data source (Array<String\>)

   For datasets not specified in `output_fields`, all fields are returned by default. If this parameter is omitted, all fields from all datasets are returned by default. If a dataset contains nested objects, only top\-level field names are supported.

   Non\-existent fields or fields nested within an Object are ignored.

   Example:


```JSON
"output_fields":{
    "10299201": ["product_code", "product_name", "description"],       
    "10299202": ["content_id", "title", "keywords", "summary"]
}
```


**context ** `Object`

The user context for the request, which supports uploading the user's geographic location.


* **location ** `Object`

   The user's geographic location, including latitude and longitude. If you configure location\-based ranking in Search and Recommendations, the policy takes effect when search or recommendation tools are used in a conversation.

   * **latitude ** `String`

      Latitude. Supports data in string format, such as "12.291". The string value must be a number in the range [\-90, 90].

   * **longitude** String

      Longitude. Supports uploading data in string format, such as "30.218". The string content must be a number in the range of [\-180, 180].




</columnsItem>
<columnsItem zoneid="izOObPH5IS">

**Session start:** 

```Bash
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/application/${application_id}/chat_search' \
  -H 'Content-Type: application/json' \
  -H 'Authorization:Bearer <API_KEY>' \
  -d '{
    "session_id": "25ee998a-5462-9385-9f18-035f1da7a6e5",
    "user": {
        "_user_id": "ldy_199432"
    },
    "opening_remarks":true
}'
```


**User provides conversation content.** 

```Bash
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/application/${application_id}/chat_search' \ 
  -H 'Content-Type: application/json' \ 
  -H 'Authorization: Bearer <API Key>' \ 
  -d '{
    "session_id": "25ee998a-5462-9385-9f18-035f1da7a6e5",  
    "input_message": { 
        "content":[{"type":"text", "text":"Any Chinese sci-fi drama recommendation?"}] 
    }, 
    "user": { 
        "_user_id": "ldy_199432", 
        "nickname":"user A"
    },
    "enable_suggestions": true,
    "reply_mode": "balanced",
    "search_param": {
        "page_size": 30,
        "dataset_ids": ["111111104"],
        "filters": {   
            "106265704": {
                "op": "must",
                "field": "parent_conent_id",
                "conds": [""]
            }
        } 
        "output_fields":{
            "10299201": ["product_code", "product_name", "description"],       
            "10299202": ["content_id", "title", "keywords", "summary"]        
        }
    }
    "context":{
        "location":{
            "longitude":"-12.299",
            "latitude":"-10.019"
        }
    }
}'
```




</columnsItem>
</columns>


<span id="68777956"></span>
## Greet users when starting a conversation

You can use the **opening_remarks** parameter to control whether to send a welcome message when starting a conversation. When this parameter is enabled, two types of interactions can be achieved based on the console configuration:


* **Recommend items at startup:**  Configure recommended items at startup and link them to an active recommendation scenario in the conversational search settings.

* **Send a welcome message at startup:**  A welcome message is automatically sent if recommended items are not configured for startup in the conversational search settings.


When `opening_remarks` is set to `true`, ensure that `session_id` is a new value, and do not pass `input_message` and `search_param`.

<span id="3af766aa"></span>
## Upload an image in a conversation

**Query image upload format instructions:** 

Pass the image file in base64 format to query.image_url. For details on the format and restrictions, see the instructions:

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Description</div>


<div data-tips="true" data-tips-type="default"><strong>The uploaded image must meet the following conditions:</strong></div>


<div data-tips="true" data-tips-type="default"><strong>Supported formats:</strong> jpeg, png, webp, bmp, tiff, ico, dib, icns, sgi, jpeg2000. Images in tiff, sgi, icns, and jpeg2000 formats must be aligned with their metadata. For example, the file metadata in object storage must be set correctly; otherwise, parsing will fail.</div>


<div data-tips="true" data-tips-type="default"><strong>Aspect ratio (width/height):</strong> In the range of [1/100, 100].</div>


<div data-tips="true" data-tips-type="default"><strong>Side length:</strong> [10, 6000] px, i.e., the shorter side must be longer than 10 px and the longer side must be shorter than 6000 px.</div>


Ensure the Base64 encoding follows the standard format, including both the **Data URI scheme** and the **Base64 encoded body**:

```Plain Text
data:[<MIME type>];base64,<Base64 encoded string>
```



|**Components** |**Format requirements** |**Description** |**Example** |
|---|---|---|---|
|**Data header prefix** |Fixed as `data:` |Indicates the string is in Data URI format and cannot be omitted or modified. |\- |
|**MIME type** |Must strictly match the actual format of the image. |Used by the server to identify the image type. Do not enter an incorrect value, such as using the PNG MIME type for a JPG image. |JPG/JPEG：`image/jpeg`；PNG：`image/png`；WebP：`image/webp` |
|**Delimiter** |Fixed as `;base64,` |Connects the MIME type to the Base64\-encoded body. The semicolon, "base64", and comma cannot be omitted or replaced. |\- |
|**Base64\-encoded body** |A Base64\-encoded string compliant with RFC 4648. |Encoded directly from the binary data of an image file. **It must not contain spaces, line breaks, or special characters,**  and must be a continuous ASCII string. | |


<span id="72b22d2e"></span>
## Using Filters

Filter conditions provided in the conversation are passed to the search tool. This means users can only filter for dataset items that meet these conditions.

Unlike search, when a conversation references multiple datasets, you must apply filters to each one. The filter parameter is a JSON map where the key is the dataset ID (String) and the value specifies the filtering conditions for the data in that dataset.

For filter condition syntax, see: [AI Search: Filter](https://docs.byteplus.com/docs/viking-aisearch/AI_search_filter)

<span id="49b84403"></span>
# Streaming Responses

<span id="7f574e62"></span>
## Streaming Response Workflow

The Chat_search API uses streaming output. After the API is called, the output process is as follows:

&nbsp;

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/1e9a1c32f0c44984bbdd05613e0c391c) </span>

&nbsp;

After the API is called, the conversational search agent performs a series of reasoning, decision\-making, and tool\-calling processes before outputting the final response from the large model. Before generating a response, all steps return events and intermediate outputs, allowing you to monitor the output flow or display intermediate processing interactions on your interface.

<span id="9c35bcb8"></span>
## Receive conversation opening content

If a new session_id is passed in the API and `opening _remarks` is set to `true`, a welcome message will be triggered along with a batch of personalized recommendations at startup (if configured in the console).

<span id="ce49e29c"></span>
### Returning only the welcome message

When returning only the welcome message, its content is streamed.


<columns>
<columnsItem zoneid="YnDwZZnfTk">

**Output parameters:** 

**request_id ** `String`

The unique ID for this request.

**result ** `Object`

Top\-level structure of the streamed response


* **content ** `String`

   Content of the welcome message in the streamed output



&nbsp;

&nbsp;




</columnsItem>
<columnsItem zoneid="Gg1IKPiGDS">

**Response example:** 

```JSON
{
  "request_id": "11fcaddc-addc-4a22-ae18-c6c39f4bbe8a",
  "result": {"content": "#"}
}
{
  "request_id": "11fcaddc-addc-4a22-ae18-c6c39f4bbe8a",
  "result": {"content": " 🎬"}
}
{
  "request_id": "11fcaddc-addc-4a22-ae18-c6c39f4bbe8a",
  "result": {"content": " Hi"}
}
{
  "request_id": "11fcaddc-addc-4a22-ae18-c6c39f4bbe8a",
  "result": {"content": "，"}
}
{
  "request_id": "11fcaddc-addc-4a22-ae18-c6c39f4bbe8a",
  "result": {"content": "Good"}
}
{
  "request_id": "11fcaddc-addc-4a22-ae18-c6c39f4bbe8a",
  "result": {"content": "Afternoon"}
}
... ...
{
  "request_id": "11fcaddc-addc-4a22-ae18-c6c39f4bbe8a",
  "result": {
    "stop_reason": "stop"
  }
}
```


</columnsItem>
</columns>


After the welcome message is returned, recommended questions are returned immediately:


<columns>
<columnsItem zoneid="Huo2UvZYDN">

**Output parameters**

**request_id ** `String`

The unique ID for this request

**result ** `Object`

Top\-level structure of the streamed response


* **payload ** `Object`

   The content of a one\-time batch output.

   * **suggestions ** `List[String]`

      A list of suggested questions for the welcome stage, returned according to the maximum number of results configured in the console.




</columnsItem>
<columnsItem zoneid="OD3AIJqXqN">

&nbsp;

```JSON
{
  "request_id": "fc627693-cc53-4903-8de6-9a49a51f4e05",
  "result": {
    "payload": {
      "suggestions": [
        "What are the popular color options for monitoring headphones?",
        "What color options are available for gaming headsets?",
        "Are Apple's monitoring headphones reliable?",
        "How long is the typical warranty period for headphones?",
        "What scenarios are headphones with 5-hour battery life suitable for?",
        "Any recommendations for mirrorless cameras with image stabilization?",
        "What is the standard warranty policy for mirrorless cameras?",
        "Which mirrorless cameras are suitable for video beginners?"
      ]
    }
  }
}
```




</columnsItem>
</columns>


&nbsp;

<span id="db7e178b"></span>
### Return a welcome message and a recommendation list

**Step 1: Call the personalized recommendation tool at startup**

At the start of a conversation, the system uses the user ID to call the recommendation tool and retrieve a personalized recommendation list.


<columns>
<columnsItem zoneid="THIudRWv9k">

**Output parameters:** 

**request_id ** `String`

A unique identifier for the request.

**result ** `Object`

The top\-level structure of the streamed response.


* **step_info ** `Object`

   Output Step Description Structure

   * **step ** `Object`

      The name of the step, returned when calling a tool:

      `tool call`: Call the recommendation tool

      `get_results`: Get the recommendation list

      * **tool_name ** `String`

         Returns the tool name when the step is 'tool call'. Outputs 'rec' when launching recommended items.

   * **step_payload ** `Object`

      Additional information output with the step, such as tool call information.

      * **param** Object

         The parameters for the recommendation scene. By default, the `scene_id` of the homepage recommendation scene configured in the console is used.

         {"scene_id":"<scene_id selected in the console\>"}

   * **payload**  `Object`

      Content returned by the recommendation tool.

      * **rec ** `Object`

         The response object from the recommendation tool.

      * **rec_results ** `List[Object]`

         A list of recommended items. The content includes:

         _id: The ID of the recommended item.

         display_fields: all fields of the item




</columnsItem>
<columnsItem zoneid="OLjWbL0K6f">

**Output example:** 


* Call the recommendation tool


```JSON
{
    "request_id": "6db275e0-8b6d-421d-beb9-b8d7453498b6",
      "result": {
           "step_info": {
               "step": "tool call",
               "step_payload": {
                   "param": {"scene_id": "scene-C4fI0e8b"},
                    "tool_name": "rec"
                 }
            }
        }
}
```



* Return the recommendation tool call result


```JSON
{
    "request_id": "6db275e0-8b6d-421d-beb9-b8d7453498b6",
    "result": {
        "step_info": {
            "step": "get results"
        }
    }
}

{
    "request_id": "6db275e0-8b6d-421d-beb9-b8d7453498b6",
    "result": {
        "payload": {
            "rec": {    
                "rec_results": [    
                {
                    "_id": "019992810",
                    "display_fields": {
                          "_hash_item_id": 4635372581706750000,
                          "formatted_description_info": {}
                          "articleId": "GK9607",
                          "contents": []
                }]
      }
}
```




</columnsItem>
</columns>


**Step 2: Stream the welcome message and recommendation reasons**

After the recommendation list is returned, the model combines the recommended content, user profile, uploaded nickname, and time to generate personalized welcome messages and recommendation reasons.


<columns>
<columnsItem zoneid="pRD453aLLw">

**Output parameters:** 

**request_id ** `String`

The unique identifier for this request

**result ** `Object`

The top\-level structure of the streamed response


* **content ** `String`

   Welcome message content for streaming output




</columnsItem>
<columnsItem zoneid="VDwXkSdobH">

```JSON
{
  "request_id": "11fcaddc-addc-4a22-ae18-c6c39f4bbe8a",
  "result": {"content": "#"}
}
{
  "request_id": "11fcaddc-addc-4a22-ae18-c6c39f4bbe8a",
  "result": {"content": " 🎬"}
}
{
  "request_id": "11fcaddc-addc-4a22-ae18-c6c39f4bbe8a",
  "result": {"content": " Hi"}
}
{
  "request_id": "11fcaddc-addc-4a22-ae18-c6c39f4bbe8a",
  "result": {"content": "，"}
}
{
  "request_id": "11fcaddc-addc-4a22-ae18-c6c39f4bbe8a",
  "result": {"content": "Good"}
}
{
  "request_id": "11fcaddc-addc-4a22-ae18-c6c39f4bbe8a",
  "result": {"content": "Afternoon"}
}
... ...
{
  "request_id": "11fcaddc-addc-4a22-ae18-c6c39f4bbe8a",
  "result": {
    "stop_reason": "stop"
  }
}
```


</columnsItem>
</columns>


**Step 3: Output featured items related to the welcome messages and recommendation reasons**

After the output is complete, it returns the list of featured recommended items referenced in the welcome messages and recommendation reasons, along with suggested questions.


<columns>
<columnsItem zoneid="UfbR72G1KE">

**Output parameters:** 

**request_id ** `String`

Unique identifier for the request.

**result ** `Object`

The top\-level structure of the streamed response.


* **payload ** `Object`

   The content structure for batch output.

   * **related_rec_items ** `List[Object]`

      If you have configured recommended items for startup in the console and linked them to an active recommendation scenario, the API returns a list of featured content after the welcome message. This list contains multiple recommended items.

      *  **_id ** `String`

         Item ID

      * **display_fields ** `Object`

         Returns all field information for the item

   * **suggestions ** `List [String]`

      Outputs recommended questions based on the recommendation list, returned as a list of strings




</columnsItem>
<columnsItem zoneid="wI0DavODhf">

**Outputs the featured recommendation list**

```JSON
{
    "request_id": "6db275e0-8b6d-421d-beb9-b8d7453498b6",
    "result": {
        "payload": {  
            "related_rec_items": [    
                {
                    "_id": "019992810",
                    "display_fields": {
                          "_hash_item_id": 4635372581706750000,
                          "formatted_description_info": {}
                          "articleId": "GK9607",
                          "contents": []
                 }
              ]
      }
}
```


**Outputs suggested questions**

```JSON
{
  "request_id": "6db275e0-8b6d-421d-beb9-b8d7453498b6",
  "result": {
    "payload": {
      "suggestions": [
        "What are the design highlights of the GAZELLE classic athletic sneakers?",
        "Are there any other recommendations for retro-style footwear?",
        "What are some other comfortable and breathable athleisure shoes?"
      ]
    }
  }
}
```




</columnsItem>
</columns>


<span id="08fd0683"></span>
## Receive the conversation response

After a user enters a message, the `chat_search` API processes the input, calls the search function, summarizes the findings, and streams the response.

<span id="ef9acbf5"></span>
### Process the user query

This stage returns a step label to indicate that the user's query has been received and is being processed.


<columns>
<columnsItem zoneid="KcVaQZf1DR">

**Output parameters:** 

**request_id ** `String`

The unique ID for this request

**result ** `Object`

The top\-level structure of the streaming response


**step_info ** `Object`

      Information about the step

            **step ** `String`

            The step name. Returns "analyze requirement" in the analysis phase.




</columnsItem>
<columnsItem zoneid="tkCzzLohRI">

**Output example:** 

```JSON
{
    "request_id":"d9bb3f4a025bfced6e75762510d76af0",
    "result":{
        "step_info":{
            "step":"analyze requirement"
         }
     }
}
```




</columnsItem>
</columns>


<span id="50687662"></span>
### Tool call

This step returns a step label and uses the payload to output the process data for the tool call, which includes two tools:


* **Search dataset:**  Call the Search tool to search the dataset associated with the application.

* **Deep Video Search:**  uses video search and video understanding tools to deeply analyze and retrieve video content.



<columns>
<columnsItem zoneid="bx4eWEoVVO">

**Output parameters**

**request_id ** `String`

The unique identifier for the request.

**result ** `Object`

The top\-level structure of the streamed response.


* **step_info ** `Object`

   Step\-related information.

   * **step ** `String`

      The name of the step. Returns "tool call" during the analysis phase.

   * **step_payload ** `Object`

      Returns the search parameters for calling the search tool, including:

      * **tool_name ** `String`

         Returns "search" when searching datasets.

         Returns "video search and analysis" for deep video searches.

      * **params ** `List[Object]`

         A list of parameters for the tool call.

         * **search_request ** `Map`

            A list of `search_request ` for the search tool call, which contains search parameters for multiple datasets. Each set of search parameters includes parameters like dataset_id, query, and filter. For details, see [Search - Search](https://www.volcengine.com/docs/85296/1544974?lang=zh).




</columnsItem>
<columnsItem zoneid="wxyPJAnfgd">

**Example output:** 

Calling the dataset search tool:

```JSON
{
    "request_id":"d9bb3f4a025bfced6e75762510d76af0",
    "result":{
        "step_info":{
            "step":"tool call",
            "step_payload":{
                "param":{
                    "search_requests":
                        [
                            {
                                "query":{"text":"film camera"},
                                "page_size":30,
                                "page_number":1,
                                "dataset_id":"111111111"
                             }
                        ]
                },
            "tool_name":"search"
            }
        }
    }
}
```


Calling the deep video search tool:

```JSON
{
    "request_id":"d9bb3f4a025bfced6e75762510d76af0",
    "result":{
        "step_info":{
            "step":"tool call",
            "step_payload":{
                "param":{
                    "search_requests":
                        [
                            {
                                "query":{"text":"What are some of the classic lines from The Stranger Things"},
                                "dataset_id":"106261599"
                             }
                        ]
                },
                "tool_name":"video search and analysis"
            }
        }
    }
}
```


</columnsItem>
</columns>


<span id="dff69a38"></span>
### Returns search results when using the dataset search tool.

Returns search results when the dataset search tool is triggered during a tool call.


<columns>
<columnsItem zoneid="sYOGm9MlUl">

**Output Parameters**

**request_id ** `String`

The unique identifier for this request

**result ** `Object`

The top\-level structure of the streamed response


* **step_info ** `Object`

   Information related to the step

   * **step ** `String`

      The step name, which is "get_results" during the analysis phase

* **payload ** `Object`

   Returns step information followed by the search result structure.

   * **search ** `Map<Object>`

      Contains the search call information and results. The key for each element is the dataset ID (String).

      * **search_result ** `Object`

         Search results from multiple datasets, identical to the response from the Search API call. See [Search - Search](https://www.volcengine.com/docs/85296/1544974?lang=zh).




</columnsItem>
<columnsItem zoneid="bDR79xv3JE">

**Response Example**

```JSON
{
  "request_id": "91c4a4e9-fd29-47a4-963e-c7ab30169c4e",
  "result": {
    "step_info": {
      "step": "get results"
    }
  }
}

{
  "request_id": "dc96d0d7-0610-4b0d-886-be56525392fa",
  "result": {
    "payload": {
      "search": {
        "149341004": {
          "search_results": [
            {
              "_id": "916179554",
              "display_fields": {
                "actor_list": [
                  "Peppa Pig",
                  "George Pig",
                  "Mummy Pig",
                  "Daddy Pig"
                ],
                "category": "movie",
                "content_id": "id—1",
                "content_type": "collection",
                "first_air_date": "2024",
                "genres": [
                  "Animation",
                  "Adventure",
                  "Comedy"
                ],
                "summary": "In 'Peppa Pig: Interstellar Adventure,' Peppa and her friends embark on an unknown journey through the stars. Facing various cosmic challenges and dangers, they must unite and use their collective wisdom and courage to complete their mission and return safely to Earth. The film continues the series' signature humor and positive themes, making it perfect for family viewing.",
                "title": "Peppa Pig: Interstellar Adventure"
              },
              "score": 0.7499999984446123,
              "recall_info": [
                {
                  "recall_reason": "text",
                  "recall_score": 0.4821949005126953,
                  "recall_rank": 1
                },
                {
                  "recall_reason": "es_recall"
                },
                {
                  "recall_reason": "vlm"
                }
              ]
            }
          ],
          "total_items": 100,
          "query": {
            "text": "animated cartoons for children featuring a pig as the main character"
          },
          "page_size": 30,
          "page_number": 1,
          "user": {
            "_user_id": "xiaoyan.1081"
          },
          "dataset_id": "149341004",
          "filter": {
            "conds": [
              ""
            ],
            "field": "parent_content_id",
            "op": "must"
          }
        }
      }
    }
  }
}
```


</columnsItem>
</columns>


<span id="d1bbbd51"></span>
### Returns video content relevant to the user's query when using the deep video search tool.

Returns video content relevant to the user's query (intermediate result) when deep video search is triggered during the tool call phase.


<columns>
<columnsItem zoneid="SL70zUW7VG">

**Output Parameters**

**request_id ** `String`

A unique identifier for the request.

**result ** `Object`

Top\-level structure for streaming responses


* **step_info ** `Object`

   Step information

   * **step ** `String`

      The step name. Returns "get results" in this stage.

   * **step_payload ** `Object`

      Returns the search parameters used to call the search tool, including:

      * **results ** `Map<Object>`

         The relevant video content results are returned as a map, where the key is the video dataset ID and the value is the video's metadata.




</columnsItem>
<columnsItem zoneid="ZG4FK35bLv">

**Output example**

```JSON
{
  "step": "get results",
  "step_payload": {
    "type": "video",
    "results": {
      "106265704": [
        {
          "content_id": "video_900026",
          "content_type": "video",
          "parent_content_id": "collection_342534",
          "sequence_index": 26,
          "video_url": [
            "http://xxxx.mp4"
          ],
          "my_title": "Stranger Things Episode 26"
        },
        {
          "content_id": "video_900027",
          "content_type": "video",
          "parent_content_id": "collection_342534",
          "sequence_index": 27,
          "video_url": [
            "http://xxxx.mp4"
          ],
          "my_title": "Stranger Things Episode 27"
        }
      ]
    }
  }
}
```


</columnsItem>
</columns>


<span id="3fe8f776"></span>
### Analyze Search Results

After using the dataset search and deep video search tools to retrieve content relevant to the user's query, the model analyzes the results and prepares an answer. This stage displays "analyze result" step information and includes a brief waiting period.


<columns>
<columnsItem zoneid="uW8eyh1onE">

**Output Parameters**

**request_id ** `String`

The unique identifier for this request

**result ** `Object`

The top\-level structure of the streamed response


* **step_info ** `Object`

   Step information

   * **step ** `String`

      The step name. Returns "analyze results" in this stage.




</columnsItem>
<columnsItem zoneid="kABzp8SaO3">

**Output Example**

```JSON
{
    "request_id":"d9bb3f4a025bfced6e75762510d76af0",
    "result":{
        "step_info":{
            "step":"analyze results"
         }
     }
}
```




</columnsItem>
</columns>


<span id="ee78e5dc"></span>
### Get Streaming Response

The model begins to generate a streaming response, streaming the summarized content after analysis.


<columns>
<columnsItem zoneid="JMsfBe70Rk">

**Output parameters**

**request_id ** `String`

The unique identifier for this request.

**result ** `Object`

The top\-level structure of the streamed response.


* **step_info ** `Object`

   Step information.

   * **step ** `String`

      The step name. Returns "reply" at this stage.

* **content ** `String`

   String returned via streaming

* **citation ** `Array [Citation structure]`

   When citing items or documents, this field returns a list of data for tracing paragraph citations, where each element is an object containing the content type, dataset ID, and data ID. This field is omitted if the output contains no citations. A list is returned at the end of a paragraph if it introduces or cites any media asset information. The citation object has the following structure:

   * **type ** `String`

      The enumeration of the cited data type. Currently, the only available value is "item", which represents data from an item dataset.

   * **dataset_id ** `String`

      The ID of the dataset to which the cited content belongs.

   *  **_id ** `String`

      The unique ID of the cited item or document, corresponding to the item ID in the image\-text item dataset and `content_id` in the video dataset.

   * **display_fields ** `Object`

      Detailed information about the cited data. The following content is returned when citing document data:

      * **doc_id ** `String`: document ID

      * **doc_name ** `String`: document name, used to identify the specific name of the cited document

      * **doc_type ** `String`: document extension

      * **text ** `String`: the original text of the cited document chunk




</columnsItem>
<columnsItem zoneid="wAntxm3kBq">

**Output Example**

```JSON
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":"为"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":"你"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":"推荐"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":"以下"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":"适合"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":"夜店"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":"的"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":"口红"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":"："}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":"\\"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":"n"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":"-"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":" Glam"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":"orous"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":" Ch"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":"icks"}}
... ...
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"citation":{"type":"item","dataset_id":"289112891","_id":"P19029XJSKK_0928812"}}}
```




</columnsItem>
</columns>


<span id="95d9e7b2"></span>
### **Batch outputs the list of items cited in the response when using the search tool.** 

Outputs a list of items cited in the response, sourced from multiple datasets, after the streaming response is complete.


<columns>
<columnsItem zoneid="jd8GeHJUgj">

**Output Parameters**

**request_id ** `String`

The unique ID for this request.

**result ** `Object`

The top\-level structure of the streaming response.


* **payload ** `Object`

   Outputs a structured list of item data.

   * **related_items ** `List[Object]`

      Returns all fields for all items referenced in this answer, along with the datasets they belong to.

      *  **_id ** `String`

         The unique ID of the item.

      * **display_fields ** `Object`

         Returns all fields of the item.

      * **dataset_id ** `String`

         The source dataset of the item.




</columnsItem>
<columnsItem zoneid="wXpY1qblw0">

**Output Example**

```JSON
{
    "request_id":"ba88a50a58928940c56f2399fd176045",
    "result":{
        "payload":{
            "related_items":[{
                "_id":"199593",
                "display_fields":{
                    "description_info":{"articleId":"I0090",
                    "bullets":["•   常规版型","•   系带设计","•   正绒面革鞋面","•   COLD.RDY科技","•   PrimaLoft®隔层","•   乙烯/乙酸乙烯酯（EVA）中底","•   Traxion外底","•   掌跟落差：10毫米（鞋跟：30毫米 / 前掌：20毫米）"],
                    "contents":"冬季美景，在窗外，更在野外。天气转冷时，让这款adidas徒步运动鞋相伴，助你自在探索未曾到访的风景。含COLD.RDY科技与PrimaLoft®隔层，即使偶遇潮湿环境，亦有舒适脚感伴你前行。采用Traxion外底和正绒面革鞋面，既有实用设计又含时尚气质，旨在打造经典徒步造型。\n",
                    "online_date":"2023-08-31 15:48:44",
                    "pdpImageUrls"：["https://some_domain.image.XXXXX.jpeg"],
                    "product_id":"199593",
                    "product_name":"UNITY LEA LOW 户外运动登山徒步鞋"},
                "score":0.9201300550324706,
                "recall_info":[{
                    "recall_reason":"text",
                    "recall_score":0.5273027420043945}],
                "rerank_info":{"is_reranked":true,"rerank_score":0.9201300550324706},
                "dataset_id":"106264990"}]
        }
    }
}
```




</columnsItem>
</columns>


<span id="c2ac4b12"></span>
### Returns a list of video clips related to the answer and their timestamp information when the video deep search tool is called.

Video deep search returns a list of video clips related to the user's question. Each clip includes a video ID, start timestamp, and end timestamp, allowing users to quickly locate relevant content.


<columns>
<columnsItem zoneid="tCSQJ5a643">

**Output Parameters**

**request_id ** `String`

The unique ID for the request.

**result ** `Object`

The top\-level structure of the streamed response.


* **payload ** `Object`

   Outputs structured segment data.

   * **video_deep_answer ** `List[Object]`

      Returns all fields for every item cited in the answer, along with the datasets they belong to.

      * **highlights ** `List[Object]`

         Returns highlight segments and summaries from multiple videos relevant to the user's query.

         * **content_id ** `String`

            Returns highlight segments and summaries from multiple videos relevant to the user's query.

         * **video_title ** `String`

            The title of the video containing the highlight. This returns the value of the "title" attribute from the uploaded video asset.

         * **generated_title ** String

            Video title generated during the video understanding stage.

         * **snippets ** `List[Object]`

            Highlight clips from the video, including the following information:

            * **start_timestamp ** `Int`

               The start timestamp of the clip (in seconds).

            * **end_timestamp ** `Int`

               The end timestamp of the clip (in seconds).

            * **summary ** `String`

               A short summary of the clip.

            * **cover ** `String`

               The URL of the screenshot for the clip's first non\-black frame, which can be used as a cover.




</columnsItem>
<columnsItem zoneid="HCL9BG0Ht6">

**Output example**

```JSON
{
  "payload": {
    "video_deep_answer": {
      "106706135": {
        "highlights": [
          {
            "content_id": "video_episode_002",
            "generated_title": "Psychic Resonance: The Vanishing Mystery and the Hawkins Lab Conspiracy",
            "video_title": "",
            "snippets": [
              {
                "start_timestamp": 262,
                "end_timestamp": 322,
                "summary": "Logic begins to fail as the supernatural emerges",
                "cover": "XXX"
              }
            ]
          },
          {
            "content_id": "video_episode_020",
            "generated_title": "Mathematical Anomalies within the Upside Down and Dimensional Rebirth",
            "video_title": "",
            "snippets": [
              {
                "start_timestamp": 1412,
                "end_timestamp": 1465,
                "summary": "A monument to lost dimensions",
                "cover": "XXXX"
              },
              {
                "start_timestamp": 1948,
                "end_timestamp": 2001,
                "summary": "The laws of physics no longer apply here",
                "cover": "XXXXX"
              }
            ]
          }
        ]
      }
    }
  }
}
```




</columnsItem>
</columns>


<span id="d95c1e45"></span>
### Returns suggested questions

If 'enable_suggestion' is enabled in the parameters, it returns a list of suggested questions related to the current search, helping users further explore or optimize their query.


<columns>
<columnsItem zoneid="v64zAwxU9Y">

**Output parameters**

**request_id ** `String`

The unique identifier for this request.

**result ** `Object`

The top\-level structure of the streamed response.


* **payload ** `Object`

   The payload containing the suggested questions.

   * **suggestions ** `List[String]`

      Returns three suggested follow\-up questions.




</columnsItem>
<columnsItem zoneid="tFGdsVaLuB">

**Output Example**

```JSON
{   
    "request_id": "ba88a50a58928940c56f2399fd176045",
    "result": {
        "payload": {
            "suggestions": [
                "Who said the phrase 'Physics has never existed'?",
                "What were the other details in Barb's missing person file?",
                "Which episode features the quote 'Friends don't lie'?"
            ]
        }
    }
}
```




</columnsItem>
</columns>


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To experience more of Viking AI's search capabilities, visit: <a href="https://www.volcengine.com/product/AI-Search-Rec">Viking AI Search Engine, the integrated search, recommendation, and Q&A intelligent engine for enterprises</a></div>
