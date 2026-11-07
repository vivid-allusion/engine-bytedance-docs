---
title: "Integrating Conversational Search"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Integrated_Conversational_Search"
---

To build a powerful conversational assistant, you can use the **Conversational Search API.**  This guide provides detailed instructions and code examples for managing the entire conversation lifecycle. It explains core concepts like sessions and user context, and details how to initiate a conversation with or without a welcome message, handle user queries, and parse streaming responses, including citations and suggested follow\-up questions.

<span id="b2219776"></span>
# Core concepts

**Session:**  A **Session** represents the entire continuous interaction between a user and the assistant within a single interface. It encapsulates the **multi\-turn conversation history**, allowing the assistant to maintain context and continuity throughout the dialogue.

**User information:**  This refers to the metadata passed during a session, currently supporting **User ID** and **Nickname**. Providing this information enables the Dialogue Engine to accumulate interaction data, which is crucial for building accurate **user interest profiles** and delivering personalized experiences.

**Step:**  The conversation assistant uses an Agent architecture. Before producing the final answer, it goes through steps such as reasoning, tool invocation, and receiving search results. Each of these is reported as step events during the process to indicate the current execution phase of the agent.

**Payload:**  Represents intermediate results output by the conversation interface that are not final replies. Each step may return different payload information, which you can either ignore or use to enhance the display of the agent's intermediate execution process to users.

<span id="b58c2ad2"></span>
# Starting a new conversation

Session startup supports two modes


1. **Conversational\-Based Opening**

   Assistant first presents the **Smart Welcome Message** or **Personalized Item Recommendations** as defined in your settings.  After the user has engaged with the opening content or entered a query, the conversation proceeds. The opening setting is set in your console. 

   For more details: [Conversational-Based Opening](https://docs.byteplus.com/docs/393/Integrated_Conversational_Search#fcce2d1e)



&nbsp;

2. **Direct Q&A**

   No welcome message or initial item recommendations. Assistant waits for the first user input and begins the Q&A process immediately. 

   For more details: [Direct Q&A](https://docs.byteplus.com/docs/393/Integrated_Conversational_Search#4c96fc7a)


<span id="fcce2d1e"></span>
# Conversational\-Based Opening

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">To configure details of welcome message or item personalization, refer to <a href="https://docs.byteplus.com/docs/viking-aisearch/92256">Configure Conversation Opening</a>.</div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/9b323881dbf94c69962430be1bf7a27c" width="370px" /></div>


&nbsp;

<span id="bd446e16"></span>
## API Request

<span id="2490c453"></span>
### **Example API Call**

```Bash
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/application/{application_id}/chat_search' \
  -H 'Content-Type: application/json' \
  -H 'Authorization:Bearer {API_KEY}' \
  -d '{
    "session_id": "25ee998a-5462-9385-9f18-035f1da7a6e5",
    "user": {
        "_user_id":"<user_id>",
        "nickname":"[User Nickname for Greetings]"
    },
    "context":{
        "location":{
            "longitude":"-12.299",
            "latitude":"-10.019"
        }
    }   
    "opening_remarks":true
}'
```


&nbsp;

<span id="d5d817f5"></span>
### **Input Parameters**


|**Parameter** |**Required?**  |**Datatype** |**Description** |
|---|---|---|---|
|{application_id} |<span data-api-tag="require\|adpRh5bUh">必选</span> |String |Application ID of the app that this Conversational Search Experience belongs to, available in the console. |
|{API_KEY} |<span data-api-tag="require\|abMVT8AvP">必选</span> |String |API key created in the console, see [API Authentication](https://docs.byteplus.com/docs/viking-aisearch/API_Authentication). |
|opening_remarks | |String |whether to activate Conversation Opening, pass`true`. |
|session_id | |String |the unique identifier of the session, used to track and manage user conversation status. You need to maintain the session ID on your server. For each new user's conversation, pass a unique new session_id. The session_id must remain consistent within one conversation. |
|_user_id | |String |(**Recommended**) A unique user ID from your platform. You must ensure this ID matches the user ID in the incoming behavior data. This parameter is required if you have enabled recommendations at the start of the conversation. |
|nickname | |String |(**Recommended**) Used to address the user with their custom nickname during opening greetings. Please refer to [Personalized welcome message](https://docs.byteplus.com/docs/viking-aisearch/92256#4918a786)  for more details. |
|location | |Object |User’s current geographic location can be passed in. |


<span id="6e250762"></span>
## API Response

<span id="7a0b458f"></span>
### Welcome Message

If no Initial Item Recommendation is configured in the console, the API returns only the welcome message, followed by suggested Starter Questions.

<span id="42ce87c8"></span>
#### **Output Parameters**


|**Parameter** |**Datatype** |**Description** |
|---|---|---|
|request_id |String |The unique request identifier for this request |
|result |Object |Top\-level structure returned to the stream |
|* content |String |Welcome message in the streaming output |


<span id="1a40baf0"></span>
#### **Sample Response**

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
  "result": {"content": ","}
}
{
  "request_id": "11fcaddc-addc-4a22-ae18-c6c39f4bbe8a",
  "result": {"content": "afternoon"}
}
{
  "request_id": "11fcaddc-addc-4a22-ae18-c6c39f4bbe8a",
  "result": {"content": "Good"}
}
... ...
{
  "request_id": "11fcaddc-addc-4a22-ae18-c6c39f4bbe8a",
  "result": {
    "stop_reason": "stop"
  }
}
```


&nbsp;

<span id="d1c08c74"></span>
### Starter Questions

After streaming the welcome message, immediately return the recommended starter questions:

<span id="13b91cd0"></span>
#### **Output Parameters**


|**Parameter** |**Datatype** |**Description** |
|---|---|---|
|request_id |String |The unique request identifier for this request |
|result |Object |Top\-level structure returned to the stream |
|* payload |Object |Content output in batch mode. |
|   * suggestions |Array<String\> |The list of “guess what you want to search” questions for the welcome phase, limited by the maximum number configured in the console |


<span id="cfaa3ca1"></span>
#### **Sample Response**

```JSON
{
    "request_id": "fc627693-cc53-4903-8de6-9a49a51f4e05",
    "result": {
        "payload": {
            "suggestions": [
                "What are the trending color options for monitoring headphones?",
                "What colors are available for gaming headsets?",
                "Are Apple monitoring headphones reliable?",
                "How long is the typical warranty period for headphones?",
                "What scenarios are best suited for headphones with a 5-hour battery life?",
                "Can you recommend a mirrorless camera with image stabilization?",
                "What is the standard warranty policy for mirrorless cameras?",
                "Which mirrorless camera is best for a beginner videographer?"
            ]
        }
    }
}
```


&nbsp;

<span id="5b617167"></span>
# Conversational\-Based Opening with Item Recommendation

When item recommendations are configured, the agent first calls the recommendation API using the user ID to obtain a personalized recommendation list, then summarizes, processes, and streams the curated recommended items, welcome message, and starter questions.

<span id="44a51a3b"></span>
## **Step 1: Triggering Recommendation API on startup**

At the start, use the user ID to call the recommendation API and get the personalized recommendation results list.

<span id="6277ce45"></span>
### **Output Parameters**


|**Parameter** |**Datatype** |**Description** |
|---|---|---|
|request_id |String |The unique request identifier for this request |
|result |Object |Top\-level structure returned to the stream |
|* step_info |Object |Output step description structure |
|   * step |Object |Step name, returned when calling a tool:<br><br><br>* tool call: Calling the recommended tool<br><br>* get_results: Fetch the recommendation list. The list of “guess what you want to search” questions for the welcome phase, limited by the maximum number configured in the console |
|   * step_payload |Object |Additional information output with the step, such as tool call details |
|      * param |Object |Parameters for the recommendation scenario.<br><br>Defaults to the homepage recommendation configuration's scene_id configured in the console<br><br>`{"scene_id":"<scene_id selected in console>"}` |
|      * tool_name |String |Returns the tool name when the step is a tool call<br><br>Outputs "rec" when starting to recommend items. |


<span id="3bda6ce8"></span>
### **Sample Response**


<columns>
<columnsItem zoneid="AnBhTsIQT6">

Calling the recommendation tool

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




</columnsItem>
<columnsItem zoneid="YVfoq2oU0A">

Returning recommendation results

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


&nbsp;

<span id="afccd7f3"></span>
## **Step 2: Welcome Message and Recommendation Reasons**

After receiving the recommendation list, the model generates personalized welcome messages and recommendation reasons based on the recommended items, user profile, uploaded user nickname, and time.

<span id="e78e62e1"></span>
### **Output Parameters**


|**Parameter** |**Datatype** |**Description** |
|---|---|---|
|request_id |String |The unique request identifier for this request |
|result |Object |Top\-level structure returned to the stream |
|* content |String |The welcome message content for streaming output |


<span id="fe99d470"></span>
### **Sample Response**

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
  "result": {"content": "Good afternoon!"}
}
}
... ...
{
  "request_id": "11fcaddc-addc-4a22-ae18-c6c39f4bbe8a",
  "result": {
    "stop_reason": "stop"
  }
}
```


<span id="bdd2bb59"></span>
## **Step 3: Output Referenced Recommended Items and Starter Questions**

Returns a sub\-list of recommended items referenced in the welcome messages and recommendation reasons, along with starter questions.

<span id="3dc9ad76"></span>
### **Output Parameters**


|**Parameter** |**Datatype** |**Description** |
|---|---|---|
|request_id |String |The unique request identifier for this request |
|result |Object |Top\-level structure returned to the stream |
|* payload |Object |Batch output content structure |
|   * related_rec_items |List[Object] |If item recommendation is configured in the console and linked to an active recommendation configuration, the API returns a curated item list after the welcome message.  |
|      * _id |String |Item ID |
|      * display_fields |Object |Returns all field information of the item |
|   * suggestions |List [String] |Return starter questions as a list of strings |


<span id="8c066e2f"></span>
### **Sample Response**


<columns>
<columnsItem zoneid="I34vSXPaj5">

Curated recommendation list

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




</columnsItem>
<columnsItem zoneid="RAAAva7DaG">

Starter questions

```JSON
{
    "request_id": "6db275e0-8b6d-421d-beb9-b8d7453498b6",
    "result": {
        "payload": {
            "suggestions": [
                "What are the key design highlights of the GAZELLE classic sneakers?",
                "Do you have any other recommendations for retro-style footwear?",
                "What other comfortable and breathable sports-leisure shoes are available?"
            ]
        }
      }
}
```




</columnsItem>
</columns>


&nbsp;


---



<span id="4c96fc7a"></span>
# Direct Q&A

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Explanation</div>


<div data-tips="true" data-tips-type="default">This request allows skipping Welcome Message and Initial Item Recommendations to directly answer questions. It also applies to each user input after the conversation opening and requires passing the session_id provided at the start.</div>


<span id="4a80c3e8"></span>
## API Request

<span id="ddc6e9f4"></span>
### **Example API Call**

```Bash
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/application/${application_id}/chat_search' \ 
  -H 'Content-Type: application/json' \ 
  -H 'Authorization: Bearer <API Key>' \ 
  -d '{
    "session_id": "25ee998a-5462-9385-9f18-035f1da7a6e5",  
    "input_message": { 
        "content":[{"type":"text", "text":"What are some good Chinese sci-fi movies worth watching?"}] 
    }, 
    "user": { 
        "_user_id": "ldy_199432", 
        "nickname":"Apple"
    },
    enable_suggestions:true
    "search_param": {
        "page_size": 20,
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


<span id="3f22c777"></span>
### **Input Parameters**


|**Parameter** |**Required?**  |**Description** |
|---|---|---|
|input_message |<span data-api-tag="require\|aiTL8Uba2">必选</span> |The content provided by the user. This can include **multimodal data**, such as both image and text information. |
|search_params | |Parameters for the search tools triggered during the conversation, including the number of homepage results to return, restrictions within a specific dataset, and search filters limiting the dataset. |
|enable_suggestion | |Determines whether to generate Follow\-up Questions at the end of the response. Defaults to **false.**  |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">For detailed explanations, refer to <a href="https://docs.byteplus.com/docs/viking-aisearch/ChatSearch">ChatSearch</a>.</div>


&nbsp;

For video conversations, if you want to display or recommend a series of content (such as a full season of a TV show instead of individual episodes). In such a use case, you will need to pass the following filter as part of the API request. 

```JSON
"{video dataset ID}": {
    "op": "must",
    "field": "parent_content_id",
    "conds": [""]
}
```


&nbsp;

<span id="75fc8078"></span>
## API Processing

Once the user’s input is received, the interface streams the Agent’s execution process followed by the final response content. For detailed execution flow and parameter explanation, see: [ChatSearch](https://docs.byteplus.com/docs/viking-aisearch/ChatSearch).

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/5599fc5d577c492cab1bdd3f28ca0ae2) </span>

<div style="text-align: center">
</div>


The streaming of the actual answer begins when the `step` is identified as  **"reply"** . This output includes the response text in Markdown format, as well as specific item fields referenced within the response paragraphs. The return fields are as follows:

<span id="98f4196c"></span>
## API Response 

<span id="51702037"></span>
### **Default Output**

<span id="2980e72d"></span>
#### **Output Parameters**


|**Parameter** |**Type** |**Description** |
|---|---|---|
|request_id |`String` |The unique request identifier for this request |
|result |`Object` |Top\-level structure of the streaming return |
|* step_info |`Object` |Information related to the step |
|   * step |`String` |Step name. "reply" is returned at this stage |
|* content |`String` |Streaming returned string |
|* citation |`Array [Citation structure]` |When a response paragraph references items or documents, this field contains a list of the cited data sources. If there are no citations, this field is omitted. Each object in the list contains the data type, dataset ID, and data ID. |
|   * type |`String` |The data type of the citation. Returns one of the following values:`"item"`item data in the item dataset;`"document"`document data in the document dataset |
|   * dataset_id |`String` |The dataset ID to which the cited content belongs |
|   * _id |`String` |The unique ID of the cited item or document, corresponding to the item ID in the image & text item dataset or the`content_id`in the video dataset |
|   * display_fields |`Object` |Detailed information of the cited data. Currently, the following content is returned when referencing document data: |
|      * doc_id |`String` |Document ID |
|      * doc_name |`String` |Document name used to identify the specific referenced document |
|      * doc_type |`String` |Document extension |
|      * text |`String` |Original text of the referenced document slice |


<span id="73f46a43"></span>
#### **Sample Response**

```JSON
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":"Can"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":"you"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":"recommend"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":"some"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":"lipsticks"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":"perfect"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":"for"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":"clubbing"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":":"}}
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


&nbsp;

<span id="bb4352c1"></span>
### Cited Video Segment [Applications with Video Dataset] 

In applications that utilises video datasets, user questions trigger a deep video search. After the streaming output is complete, a list of video clips related to the user's question is provided. Each clip includes video ID, start timestamp, and end timestamp to help users quickly locate relevant content.

<span id="9c13c308"></span>
#### **Output Parameters**


|**Parameter** |**Type** |**Description** |
|---|---|---|
|request_id |String |The unique request identifier for this request |
|result |Object |Top\-level structure of the streaming return |
|* payload |Object |Use payload to output suggested questions |
|   * video_deep_answer |Array<String\> |Return all fields of all items referenced in this answer, along with the datasets these items belong to |
|      * highlights |Array<Object\> |Return highlights and summaries related to user questions across multiple videos |
|         * content_id |String |Return highlights and summaries related to user questions across multiple videos |
|         * video_title |String |The title of the video to which the highlight belongs, returning the field value of the "title" attribute marked in the uploaded video asset |
|         * generated_title |String |The video title generated during the video understanding phase |
|         * snippets |Array<Object\> |Highlight segments in the video containing the following information: |
|            * start_timestamp |Int |Start timestamp of the segment (seconds) |
|            * end_timestamp |Int |End timestamp of the segment (seconds) |
|            * summary |String |Short summary of the clip |
|            * cover |String |URL of the clip's non\-black first frame, used for cover display |


<span id="e8be8665"></span>
#### **Sample Response**

```JSON
{
    "payload":{
        "video_deep_answer":{
            "106706135":{
                "highlights":[
                    {"content_id":"video_episode_002",
                    "generated_title":"The Countdown Enigma: Collapsing Physics and the Battle for Scientific Frontiers",
                    "video_title":"",
                    "snippets":[{
                        "start_timestamp":262,
                        "end_timestamp":322,
                        "summary":"Physics no longer exists",
                        "cover":"XXX"}]},
                    {"content_id":"video_episode_020",
                    "generated_title":"Mathematical Deadlocks in a Chaotic Universe and the Rebirth of Civilization",
                    "video_title":"",
                    "snippets":[{
                        "start_timestamp":1412,
                        "end_timestamp":1465,
                        "summary":"A Monument and a Tombstone for Civilization",
                        "cover":"XXXX"},
                        {"start_timestamp":1948,
                        "end_timestamp":2001,
                        "summary":"Physics has never existed.",
                        "cover":"XXXXX"}]}]
                    }
                ]
            }
        }
    }
}
```


&nbsp;

<span id="b995ee22"></span>
### Follow\-up questions

If the parameter 'enable_suggestion' is enabled, a list of suggested questions related to the current search will be returned to help users explore further or refine their queries.

<span id="0c69300a"></span>
#### **Output Parameters**


|**Parameter** |**Type** |**Description** |
|---|---|---|
|request_id |String |The unique request identifier for this request |
|result |Object |Top\-level structure of the streaming return |
|* payload |Object |Use payload to output suggested questions |
|   * suggestions |Array<String\> |Return 3 recommended follow\-up questions for users |


<span id="6aa2a8d1"></span>
#### **Sample Response**

```JSON
{   
    "request_id":"ba88a50a58928940c56f2399fd176045",
    "result":{
        "payload":{
            "suggestions":["Who said 'Physics no longer exists'?","What else was in Yang Dong's suicide note?","Which episode is 'The bugs have never been defeated' from?"]
         }
    }
}
```


&nbsp;

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Explanation</div>


<div data-tips="true" data-tips-type="default">For more examples and best practices, refer to <a href="https://docs.byteplus.com/docs/viking-aisearch/Configure_and_Integrate_Conversational_Search">Configure and Integrate Conversational Search</a></div>
