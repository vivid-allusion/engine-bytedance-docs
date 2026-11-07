---
title: "Configure and Integrate Conversational Search"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Configure_and_Integrate_Conversational_Search"
---

After successfully configuring and activating item data in your application, you can test the conversational search on the **Experience center** page. By integrating the ***chat_search*** and ***search*** APIs, you can iachieve interactions similar to the experience page on your client or web platform. 

<video src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/dd09d1f2ebe84123b7259ed65d5fd8a3" controls></video>


Conversational search provides two types of interaction \- 


* **Search within conversation:**  Focused on content search and recommendation within conversations. This is ideal for shopping guides and recommendation assistants on e\-commerce or video media platforms, providing users with content discovery and information services.



<columns>
<columnsItem zoneid="bWVBgAtaIC">

<div style="text-align: center">
</div>


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/a77476842e5a450aa982c942c615d203) </span>



</columnsItem>
<columnsItem zoneid="eixOVVEXIE">

<div style="text-align: center">
</div>


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/1fee18d27c6b4254924104ff0cf336b5) </span>



</columnsItem>
</columns>



* **Search while Asking:**  Displays all content found based on user needs alongside the conversation. This is suitable for scenarios like image asset libraries or general e\-commerce, where you need to provide precise recommendations and Q&A while offering a paginated search list.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/a0c0faff1f8343a0968da2bc59b05a0d" width="649px" /></div>


This article describes how to configure and use the ***chat_search*** interface to integrate both "Conversation" and "Search While Asking" interactions.

<span id="72055737"></span>
# Configure Conversational Search Experience

On the **Experience** **center ** page, you will find a configuration panel on the left side containing few categories of settings:


* **Search settings:**  Controls the search strategy when calling search within conversation; it shall be done under Search experience configuration. 

* **Role and style:**  Controls the conversation output, offering settings for persona and response style, as well as controls for prohibited words.


You can adjust these configuration items on the experience page to fine\-tune the search and Q&A performance of the conversation.

<span id="dedac751"></span>
## Adjust search matching strategy

High\-quality conversation depends on search tools finding precise content that matches user intent. Within the configuration, you can adjust the matching strategy for different datasets to ensure the assistant responds accurately.

<span id="74949312"></span>
### Adjust text matching strategy

The search function includes built\-in matching based on keywords and text semantics. You can fine\-tune the weights of semantic matching and keyword matching based on your search scenario.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/d901bd98c34940089009fb4c97bf628a" width="422px" /></div>


**Increase semantic matching weight:**  Semantic matching captures abstract and implicit intentions in natural language queries and performs well in conversation search scenarios.

**Increase keyword matching weight:**  In e\-commerce and news scenarios, appropriately increasing the weight of keyword matching helps improve matching for exclusive entities and terms (such as product names, personal names, place names, companies, organizations, scientific terms, etc.).

<span id="7832ce72"></span>
### Enable semantic re\-ranking

When integrating conversation scenarios, it is recommended to enable semantic re\-ranking. Select the top N recalled items and calculate the semantic relevance between their text descriptions and the user's query. This better captures the conceptual and hidden intent in the user's question and highlights the most relevant items for the reply phase.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/541483829b824f128b3b7fa9b79f7fc7" width="392px" /></div>


&nbsp;

> Note: Semantic re\-ranking increases the time required for search results and reply processing. The more items and the longer their character count, the greater the re\-ranking delay. It is recommended to keep reordering within 20 items in dialogue scenarios.


<span id="132c840b"></span>
## Adjust dialogue persona and style

The dialogue search scenario provides a default assistant character setting and defines the assistant’s baseline language style for replies:

```Plain Text
## Agent Identity: 
As a trustworthy search assistant, you maintain a rigorous and objective stance, dedicated to providing insightful content recommendations and detailed information. No matter how complex the query, you assist users with efficiency and a friendly attitude.

## Response Style:
** Clarity First ** Write clear, effective, and engaging content.
** Straightforward Language ** Use direct language; avoid jargon, long-winded explanations, or filler words.
** Tone ** Maintain a warm, vivid, empathetic, and unbiased tone.
** Structured Replies ** Use bold text, lists, and paragraphs to highlight key points. Long responses must have a clear hierarchy and summarize complex content.
```


If your scenario requires specific assistant character names, personas, or language tone and style in replies, you can directly modify the prompts.

**Character settings:** 

Define the character’s name

Define the character’s persona (role functions, core personality traits, etc.)

... ...

**Response style:** 

Reply language style and tone, such as word preferences, sentence structure requirements, and catchphrases

Level of detail or conciseness in the writing reply

... ...

You can change these settings in the **Experience center** interface at any time to see immediate results. Once optimized, click the **Sync changes to API** button in the top right to push these settings to the live `search` and `chat_search` APIs.

<span id="b4f8f862"></span>
# Integrate Conversational Search

After completing and applying the configuration, integrate the conversational search experience by accessing the chat_search interface.

<span id="31a86ac3"></span>
## Call *ChatSearch* API

When calling the interface, use Volcano's AK authentication mechanism to generate authentication information. We recommend integrating the Volcengine Authentication SDK. Integration details can be found at: [authentication mechanism](https://www.volcengine.com/docs/85296/1544950)

Refer to the following method to call the ChatSearch API:

```Plain Text
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/application/{application_id}/chat_search' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: <Signature String>' \
  -d '{
  "session_id": "<Session ID>",
  "input_message": {
    "content": [
      {
        "type": <Content type: text or image_url>,
        "text": <Query text (when type is text)>,
        "image_url": {
          "url": <Image file URL (when type is image_url)>
        }
      }
    ]
  },
  "user": {
    "_user_id": <User ID>
  },
  "enable_suggestions": <Whether to enable suggested queries; defaults to false>,
  "search_param": {
    "page_size": <Search page size>,
    "dataset_ids": <Range of dataset IDs to search>,
    "filters": <Filters for conversational search; key is dataset_id, value is the dataset filter>
  }
}'
```


**Parameter explanation:** 

`*application_id*` *: * The ID of the application you created

`*session_id*` * String: * The conversation session is maintained by your service. Upload a new *session_id* for each new conversation and ensure the session_id remains consistent for every request within the same conversation

`*input_type*` * (String): * Accepts either "text" or "image"


*  *(when type is "text")* `*query_text*` * (String): * The user's query text input

*  *(when type is "image")* `*image_file*` * (String \- Base64): * Upload the query image in base64 format to perform image\-based search within the conversation and generate a response


> When the user's input contains both image and text, such as "{{image_file}} are there similar products?", upload a list with two elements in the content parameter, passing the text content and the image Base64 file respectively


`*search_page_size*` * (Int): * Optional, determines the pagination logic when calling the search tool

`*search_filter*` *: * Predefined filters for dataset search during conversations. In video media scenarios, set filter to only search where parent_content_id is empty to return only parent\-level content. See the filter syntax in: [Search API - Filter](https://www.volcengine.com/docs/85296/1544974#%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84)

`*user_id*` *(String)* : upload the user ID corresponding to this call; optional

`*enable_suggestions*`  *(Bool)* : provide users with suggested questions after each reply; enabled by default

&nbsp;

**Refer to the following call example:** 

```HTTP
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/application/{application_id}/chat_search' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: <Signature String>' \
  -d '{
  "session_id": "session_id",
  "input_message": {
    "content": [
      {
        "type": "text",
        "text": "Recommend some lipsticks with moisturizing and anti-aging benefits"
      }
    ]
  },
  "user": {
    "_user_id": "U109287BsioaJOns05"
  },
  "enable_suggestions": true
}'
```


&nbsp;

For detailed parameter information of the interface, please refer to: [ChatSearch](https://docs.byteplus.com/docs/viking-aisearch/ChatSearch)

<span id="75361c9d"></span>
## Integrate API Response

<span id="b84cbcd7"></span>
### **Streaming Response Overview**

The ChatSearch API returns data using streaming output. After calling the API, the output process is as follows:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/cb9d8392a94c47dfb96d2dcf36734be1" width="2389px" /></div>


&nbsp;

After the request is initiated, the conversational search agent undergoes a series of reasoning, judgment, and tool invocation processes, finally executing the LLM (Large Language Model) reply. Before the final reply is generated, all preceding steps will return events and intermediate process outputs. These allow you to monitor the output flow or display intermediate processing interactions on your user interface.

<span id="eb7caaad"></span>
### Interaction Examples

Using the interaction design from the Experience center page as an example, the following explains how to integrate the model's output into your own terminal interface:

<span id="4f749ac4"></span>
#### Example of invoking search tools

<div style="text-align: center">
</div>


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/edcd75453c604d6db0e1a17f00e87289) </span>

<span id="f3d2f9a9"></span>
#### Example of invoking video deep search tools

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/66b1eb9859224fc58461436db222141e" width="3678px" /></div>


<span id="ea08e0ea"></span>
### Output of each step

The following provides a detailed explanation of the output content for each step.

<span id="b2042647"></span>
#### Analyze conversation content


|**Returned fields** |**Description** |
|---|---|
|**request_id** |`*String*`<br><br>A unique identifier for this request, allowing quick location of a request’s execution based on the request_id. |
|**result** |`*Result structure*`<br><br>Contains all output during a streaming session; the result content varies across different agent steps |
| **`-`**  ** step_info**<br><br> |`*StepInfo structure*`<br><br>The process agent is in and the output generated during the process |
| **`--`**  **  step** |`String`<br><br>The step name; returns "analyze requirement" during the analysis phase |


**Return example:** 

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


&nbsp;

<span id="d290a972"></span>
#### Tool Invocation

**Invoke the search tool**

In the image and text dataset, the search tool can be invoked for multi\-source data retrieval. For video search scenarios, when users search for media assets or recommended media content, the model triggers the search tool to perform media asset searches.


|**Returned field** |**Description** |
|---|---|
|**request_id** |`*String*`<br><br>The unique identifier for this request, allowing quick location of an execution based on request_id. |
|**result** |`*Result structure*`<br><br>Contains all output content from a streaming session; the content of result varies across different agent steps. |
| **`-`**  ** step_info**<br><br> |`*StepInfo structure*`<br><br>The process stage of the agent and the output content within the process |
| **`--`**  **  step**<br><br> |`*String*`<br><br>Step name, return "tool call" at this stage |
| **`--`**  **  step_payload** |`*Param structure*`<br><br>Return search parameters when calling the search tool, including:<br><br><br>* tool_name：search<br><br>* search_request list containing search parameters for multiple datasets. Each group of search parameters includes:<br><br>   * dataset_id: target dataset for the search<br><br>   * query: model analysis and rewritten query statement<br><br>   * page_size: the number of items returned per page by the search tool |


**sample response:** 

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
                                "query":{"text":"firework over mountain"},
                                "page_size":10,
                                "page_number":1,
                                "dataset_id":"106261599"
                             }
                        ]
                },
            "tool_name":"search"
            }
        }
    }
}
```


&nbsp;

**Invoke video deep search**

In video search, if the analysis phase determines the need for detailed Q&A and explanation within the video's content, it triggers the video deep search tool. The tool invocation phase outputs as follows:


|**Returned fields** |**Description** |
|---|---|
|**request_id** |`*String*`<br><br>the unique identifier for this request, which allows quick location of the request execution by request_id |
|**result** |`*result structure*`<br><br>contains all output content from a streaming output; the content of result varies across different agent steps |
| **`-`**  ** step_info**<br><br> |`*StepInfo structure*`<br><br>The process where the agent is located and the output content within the process |
| **`--`**  **  step**<br><br> |`*String*`<br><br>Step name, returns "tool call" at this stage |
| **`--`**  **  step_payload** |`*Param structure*`<br><br>Parameters used when calling a search tool, including:<br><br><br>* tool_name：video search and analysis<br><br>* search_request list containing query parameters for multiple video datasets. each set of search parameters includes:<br><br>   * dataset_id: the target dataset for the search<br><br>   * query: the model\-analyzed and rewritten query statement |


**Sample response:** 

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
                                "query":{"text":"what are the well-known scripts from drama San Ti?"},
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


&nbsp;

<span id="668e4e8d"></span>
#### Retrieve search results

When the Search Tool or Video Deep Search Tool is invoked, preliminary search results will be returned.


* Search Tool: These results are provided to the LLM for reasoning, judgment, and the final generation of a response.

* Video Deep Search Tool: This tool retrieves a batch of media content, which the model then uses for further filtering and video\-specific knowledge queries.


Search tool returns the following content in response:


|**Returned fields** |**Description** |
|---|---|
|**request_id**<br><br> ** **  |`*String*`<br><br>a unique identifier for this request, which can quickly locate the execution of a request using the request_id. |
|**result** |`*Result structure*`<br><br>Includes all output content from a single streaming output; the result content varies across different agent steps |
| **`-`**  ** step_info**<br><br> |`*StepInfo structure*`<br><br>The process the agent is in and the output content within the process |
| **`--`**  **  step**<br><br> |`*String*`<br><br>Step name, returns "get results" at this stage |


**Sample response:** 

```JSON
{
    "request_id":"d9bb3f4a025bfced6e75762510d76af0",
    "result":{
        "step_info":{
            "step":"get results"
         }
     }
}
```


Subsequently, the payload is used to return a list of search results as intermediate output. The content within this search list is processed by the model for reasoning and intent matching, eventually leading to the output of final results that satisfy the user's requirements during the final response stage.


|**Returned field** |**Description** |
|---|---|
|**request_id** |`*String*`<br><br>The unique identifier for this request, allowing the request execution to be quickly located using request_id. |
|**result** |`*Result structure*`<br><br>Includes all output content from one streaming output; the content of result varies across different agent steps. |
| **`-`**  ** payload** ||
| **`--`**  ** search** |`*Search structure*`<br><br>Contains information about the search call and the search results |
| **`---`**  ** {{dataset_id}}**  |`*String*`<br><br>dataset ID of the search results |
| **`---`**  ** search_results** |`*SearchResults structure*`<br><br>Contains all results found within this dataset |
| **`---`**  ** total_items** |`*Int*`<br><br>Limit on the number of search results returned as configured in the console |
| **`---`**  ** page_size** |`*Int*`<br><br>Number of results returned per page |
| **`---`**  ** page_number** |`*Int*`<br><br>The page number of the search results to return |
| **`---`**  ** dataset_id** |`*String*`<br><br>ID of the dataset to which the search results belong |


**Sample response:** 

```JSON
{
    "request_id":"d9bb3f4a025bfced6e75762510d76af0",
    "result":{
        "payload":{
            "search":{    
                [{ 
                    "106265704": { 
                        "search_results": [ 
                            { 
                                "_id": "WSHOE001", 
                                "display_fields": { 
                                    "item_id": "WSHOE001", 
                                    "pub_time": 1741835835 
                                }, 
                                "score": 0.18181818181818182 
                            } 
                        ], 
                        "total_items": 200, 
                        "query": { 
                            "text": "Recommend me a pair of female office footwear" 
                        }, 
                        "page_size": 1, 
                        "page_number": 1, 
                        "dataset_id": "106265704" 
                    } 
                }]
            }
        }
    }
}
```


&nbsp;

**Content returned by the video deep search tool**

The video deep search tool returns the following content


|**Returned fields** |**Description** |
|---|---|
|**request_id** |`*String*`<br><br>A unique identifier for this request, which allows quick location of the execution of a request based on request_id. |
|**result** |`*Result structure*`<br><br>Contains all output content of a streaming output. The content of result varies in different agent steps. |
| **`-`**  ** step_info**<br><br> |`*StepInfo structure*`<br><br>The agent's current process and the output content within the process |
| **`--`**  **  step**<br><br> |`*String*`<br><br>Step name, return "get results" at this stage |
| **`--`**  ** step_payload** ||
| **`---`**  ** results** |`*Results structure*`<br><br>Return all media content possibly related to the user's query from the preliminary search, including all media content fields |


**Sample response:** 

```JSON
## Displaying the step_info Structure Only ##

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
                    "my_title": "San Ti Episode 26"
                },
                {
                    "content_id": "video_900027",
                    "content_type": "video",
                    "parent_content_id": "collection_342534",
                    "sequence_index": 27,
                    "video_url": [
                        "http://xxxx.mp4"
                    ],
                    "my_title": "San Ti Episode 27"
                }
            ]
        }
    }
}
```


&nbsp;

<span id="7d10abb9"></span>
#### Result analysis and judgment

After retrieving the search results, the model analyzes them to determine the relevance between the items and the user's query and begins preparing the final response.

This step is processed by the LLM (Large Language Model) and typically takes a few seconds. We recommend implementing a "loading" state or a similar interaction on your UI to ensure a smooth and fluid user experience.


|**Returned fields** |**Description** |
|---|---|
|**request_id** |`*String*`<br><br>The unique identifier for this request, allowing quick location of a request execution using request_id. |
|**result** |`*Result structure*`<br><br>Includes all output content from one streaming output; the result content varies across different agent steps. |
| **`-`**  ** step_info**<br><br> |`*StepInfo structure*`<br><br>The process the agent is in and the output content within the process |
| **`--`**  **  step**<br><br> |`*String*`<br><br>The step name; at this stage, returns "analyze results" |


**Return example:** 

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


&nbsp;

<span id="c3f4d3b9"></span>
#### (video deep Q&A output) relevant video content for deep Q&A

Within the Video Deep Q&A workflow, the model analyzes the search results and locks onto the video or video series most relevant to the user's question. This specific content is then used for final analysis and the generation of the response.


|**Returned fields** |**Description** |
|---|---|
|**request_id**<br><br> ** **  |`*String*`<br><br>the unique identifier for this request, which allows quick tracking of the request execution by request_id. |
|**result** |`*Result structure*`<br><br>contains all output content of a streaming output; the content of result varies across different agent steps |
| **`-`**  ** payload** ||
| **`--`**  **  video_deep_answer** ||
| **`---`**  **  related_video** |Return all media asset fields related to this query's video content |


**Sample response:** 

```JSON
{
    "request_id": "9d24e069f768fca9da3f0c1e176689fb",
    "result": {
        "payload": {
            "video_deep_answer": {
                "106706135": {
                    "related_video": {
                        "content_id": "collection_episode_001",                     
                        "content_type": "collection",
                        "actor_list": [
                            {"actor": "Zhang Luyi", "role": "Wang Miao"},
                            {"actor": "Yu Hewei", "role": "Shi Qiang"},
                            {"actor": "Chen Jin", "role": "Ye Wenjie (Elderly)"}
                        ],
                        "category": "TV Series",                       
                        "director": "Yang Lei",
                        "duration": 129654,
                        "first_air_date": "2023",
                        "genres": ["Mystery", "Sci-Fi"],
                        "region": ["Mainland China"],
                        "summary": "In 2005, a series of abnormal disturbances occurred in Earth's fundamental science, causing panic and instability within the scientific community. Bizarre suicides of scientists, a near-miraculous countdown, the secretive 'Frontiers of Science' organization, and the mysterious 'Three-Body' game all emerged. Nanoscientist Wang Miao is brought to the Joint Operations Center by police officer Shi Qiang to infiltrate 'Frontiers of Science' and assist the investigation. Amidst the fog, Wang Miao encounters the ETO organization and discovers its commander-in-chief is Ye Wenjie, the mother of the late scientist Yang Dong. As ETO and the Operations Center engage in a strategic back-and-forth, Wang Miao and Shi Qiang gradually realize the world within the 'Three-Body' game is real. The source of everything is a desperate struggle for survival between two civilizations. Through the collective efforts of the Operations Center and scientists, Wang Miao, Shi Qiang, and others regain hope and lead the preparation for a life-and-death struggle against the impending Trisolaran invasion.",
                        "title": "San Ti"
                    }
                }
            }
        }
    }
}
```


&nbsp;

<span id="2159d64d"></span>
#### Obtain answers

Output begins when step is detected as "reply".

That is:

```JSON
{
    "request_id":"d9bb3f4a025bfced6e75762510d76af0",
    "result":{
        "step_info":{
            "step":"reply"
         }
     }
}
```


The response phase outputs the following content. The details are explained separately for the Search Tool and the Video Deep Search & Q&A Tool:

<span id="6aafe5da"></span>
##### Reply content from Search Tool

**1\- Use ** **`content`** ** text in streaming output ** 


|**Returned fields** |**Introduction** |
|---|---|
|**request_id** |`*String*`<br><br>The unique identifier for this request, allowing quick location of the execution based on the request_id. |
|**result**<br><br> |`*Result structure*`<br><br>Contains all output content from a streaming output; the content of result varies across different agent steps |
| **`-`**  ** content**<br><br> |`*String*`<br><br>Streamed returned string |
| **`-`**  ** citation** |`Array [Citation structure]`<br><br>A list of item data for paragraph citations when outputting referenced items or document content. Each element in the list is an object containing the item type, dataset ID, and data ID. This field is omitted when no citations are in the output. At the paragraph's end, if the paragraph introduces or cites certain media assets, a list is returned. The citation object returns the following structure: |
| **`-`**  ** **  **`-`**  ** type** |`String`<br><br>Enumerated data types for references, currently only "item": item data in the item dataset |
| **`-`**  ** **  **`-`**  ** dataset_id** |`String`<br><br>ID of the dataset to which the referenced content belongs |
| **`-`**  ** **  **`-`**  ** _id** |`String`<br><br>Unique ID of the referenced item or document, corresponding to the item ID passed in the graphic item dataset or the value of `content_id` in the video dataset |


**Sample response:** 

```JSON
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":"Here"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":" are"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":" some"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":" lipsticks"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":" perfect"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":" for"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":" the"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":" club"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":":"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":"\n"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":"-"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":" Glam"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":"orous"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":" Ch"}}
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"content":"icks"}}
... ...
{"request_id":"f7d26edd3d1da65b49fccde4244629f3","result":{"citation":{"type":"item","dataset_id":"289112891","_id":"P19029XJSKK_0928812"}}}
```


&nbsp;

**2\- Use payload to return all referenced items in the answer**


|**Returned fields** |**Description** |
|---|---|
|**request_id** |`*String*`<br><br>The unique identifier for this request, allowing quick location of the execution based on request_id. |
|**result** |`*Result structure*`<br><br>Includes all output content of a streaming output; the content of result varies across different agent steps. |
| **`-`**  ** payload** ||
| **`--`**  ** related_items** |`*Array<Objet>* `<br><br>Returns all fields of items referenced in this answer, along with the datasets these items belong to. |
| **`---`**  ** _id** |`*String*`<br><br>Unique identifier of the item |
| **`---`**  ** display_fields** |`*Object*`<br><br>Return item fields as is |
| **`---`**  ** dataset_id** |`*String*`<br><br>ID of the dataset the item belongs to |
| **`---`**  ** score** |`*Float*`<br><br>Item sorting score |


**Sample response:** 

```JSON
{
    "request_id": "ba88a50a58928940c56f2399fd176045",
    "result": {
        "payload": {
            "related_items": [{
                "_id": "199593",
                "display_fields": {
                    "description_info": {
                        "articleId": "I0090",
                        "bullets": [
                            "• Regular fit",
                            "• Lace closure",
                            "• Nubuck leather upper",
                            "• COLD.RDY technology",
                            "• PrimaLoft® insulation",
                            "• EVA midsole",
                            "• Traxion outsole",
                            "• Midsole drop: 10 mm (heel: 30 mm / forefoot: 20 mm)"
                        ],
                        "contents": "Winter beauty is found both outside the window and deep in the wilderness. When the weather turns cold, let these adidas hiking shoes accompany you as you explore uncharted landscapes. Featuring COLD.RDY technology and PrimaLoft® insulation, they provide a comfortable feel even in damp environments. With a Traxion outsole and nubuck leather upper, these shoes blend practical design with stylish flair for a classic hiking look.\n",
                        "online_date": "2023-08-31 15:48:44",
                        "pdpImageUrls": ["https://some_domain.image.XXXXX.jpeg"],
                        "product_id": "199593",
                        "product_name": "UNITY LEA LOW Outdoor Hiking and Mountaineering Shoes"
                    }
                },
                "score": 0.9201300550324706,
                "recall_info": [{
                    "recall_reason": "text",
                    "recall_score": 0.5273027420043945
                }],
                "rerank_info": {
                    "is_reranked": true,
                    "rerank_score": 0.9201300550324706
                },
                "dataset_id": "106264990"
            }]
        }
    }
}
```


&nbsp;

**3\- Use payload to return suggested questions**


|**Returned field** |**Description** |
|---|---|
|**request_id** |`*String*`<br><br>The unique identifier for this request, which allows quick locating of the execution of a request based on the request_id. |
|**result** |`*Result structure*`<br><br>Contains all output content of a streaming output. The content of result varies across different agent steps. |
| **`-`**  ** payload** ||
| **`--`**  ** suggestions** |`*Array<String>* `<br><br>Return 2\-5 recommended questions for users to continue asking |


**Sample response:** 

```JSON
{
    "request_id": "ba88a50a58928940c56f2399fd176045",
    "result": {
        "payload": {
            "suggestions": [
                "What does the COLD.RDY technology in hiking shoes do?",
                "What is the price of the SEEULATER classic sneakers?",
                "Are there any other brands of hiking shoes you recommend?"
            ]
        }
    }
}
```


&nbsp;

<span id="80dfd3ac"></span>
##### Reply content from video deep search tool

**1\- Use ** **`content`** ** text in streaming output ** 


|**Returned fields** |**Introduction** |
|---|---|
|**request_id** |`*String*`<br><br>The unique identifier for this request, which allows quick location of the execution based on request_id. |
|**result**<br><br> |`*Result structure*`<br><br>Includes all output content of a streaming output; the result content varies across different agent steps |
| **`-`**  ** content**<br><br> |`*String*`<br><br>Streaming returned string |


**Sample response:** 

```JSON
{"request_id":"e86f1ec7-1331-4f96-a412-8407944fc251","result":{"step_info":{"step":"reply"}}}
{"request_id":"e86f1ec7-1331-4f96-a412-8407944fc251","result":{"content":"Although"}}
{"request_id":"e86f1ec7-1331-4f96-a412-8407944fc251","result":{"content":" the"}}
{"request_id":"e86f1ec7-1331-4f96-a412-8407944fc251","result":{"content":" series"}}
{"request_id":"e86f1ec7-1331-4f96-a412-8407944fc251","result":{"content":" does"}}
{"request_id":"e86f1ec7-1331-4f96-a412-8407944fc251","result":{"content":" not"}}
{"request_id":"e86f1ec7-1331-4f96-a412-8407944fc251","result":{"content":" explicitly"}}
{"request_id":"e86f1ec7-1331-4f96-a412-8407944fc251","result":{"content":" state"}}
{"request_id":"e86f1ec7-1331-4f96-a412-8407944fc251","result":{"content":" it,"}}
{"request_id":"e86f1ec7-1331-4f96-a412-8407944fc251","result":{"content":" we"}}
{"request_id":"e86f1ec7-1331-4f96-a412-8407944fc251","result":{"content":" can"}}
{"request_id":"e86f1ec7-1331-4f96-a412-8407944fc251","result":{"content":" infer"}}
... ...
```


&nbsp;

**2\- Use payload to return video highlights related to the user’s question**


|**Returned field** |**Introduction** |
|---|---|
|**request_id** |`*String*`<br><br>Unique identifier for this request, used to quickly locate the execution of a request by request_id. |
|**result** |`*Result structure*`<br><br>Includes all output content from a single streaming output; the result content varies across different agent steps |
| **`-`**  ** payload** ||
| **`--`**  **  video_deep_answer** ||
| **`---`**  **  highlights** |`*Array of Highlight structures*`<br><br>Returns multiple highlight clips and summaries related to user questions within videos |
| **`----`** **content_id** |`String`<br><br>Video content ID to which the highlight belongs |
| **`----`** **video_title** |`String`<br><br>The video title for the highlight, returning the value of the "title" attribute marked in the uploaded video asset |
| **`----`** **generated_title** |`String`<br><br>The video title generated during the video understanding phase |
| **`----`** **snippets** |`*Array of snippet structures*`<br><br>Highlight clips within the video |


Fields included in highlights (snippets):


|**Field** |**introduction** |
|---|---|
|**start_timestamp** |`*Int*`<br><br>start timestamp of the segment (seconds) |
|**end_timestamp**<br><br> ** **  |`*Int*`<br><br>end timestamp of the segment (seconds) |
|**summary** |`*String*`<br><br>summary of the segment |
|**cover**<br><br> |`*String*`<br><br>URL of a non\-keyframe screenshot from the clip, usable for cover display |


**Sample response:** 

```JSON
{
    "payload": {
        "video_deep_answer": {
            "106706135": {
                "highlights": [
                    {
                        "content_id": "video_episode_002",
                        "generated_title": "The Countdown Mystery Under the Collapse of Physics and the Battle of Science Boundaries",
                        "video_title": "",
                        "snippets": [
                            {
                                "start_timestamp": 262,
                                "end_timestamp": 322,
                                "summary": "Physics does not exist",
                                "cover": "XXX"
                            }
                        ]
                    },
                    {
                        "content_id": "video_episode_020",
                        "generated_title": "Mathematical Dilemmas in a Chaotic Universe and the Rebirth of Civilization",
                        "video_title": "",
                        "snippets": [
                            {
                                "start_timestamp": 1412,
                                "end_timestamp": 1465,
                                "summary": "Civilization's Monument and Tombstone",
                                "cover": "XXXX"
                            },
                            {
                                "start_timestamp": 1948,
                                "end_timestamp": 2001,
                                "summary": "Physics has never existed",
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


&nbsp;

**3\- Use payload to return suggested questions**


|**returned field** |**description** |
|---|---|
|**request_id** |`*String*`<br><br>Unique identifier for this request, allowing quick tracking of the request execution using the request_id. |
|**result** |*Result structure*<br><br>Includes all output content from a single streaming session; the result content varies across different agent steps |
| **`-`**  ** payload** ||
| **`--`**  ** suggestions** |`*Array<String>* `<br><br>Returns 2\-5 recommended follow\-up questions for users |


**Return example:** 

```JSON
{
    "request_id": "ba88a50a58928940c56f2399fd176045",
    "result": {
        "payload": {
            "suggestions": [
                "Who said 'Physics does not exist'?",
                "What else was in Yang Dong's suicide note?",
                "Which episode features the line 'The bugs have never been defeated'?"
            ]
        }
    }
}
```


&nbsp;

<span id="55a8ad9d"></span>
# Implement search\-while\-asking in conversational search

The search\-while\-asking experience refers to an interaction model where the complete list of search results triggered by each query is displayed outside of the conversation window during the conversational search process.

In this setup, the dialogue assistant serves to facilitate the search and provide direct answers. Users can progressively refine or expand their search requirements based on the guidance provided in the model's responses. The interactive display of all search results allows users to fully explore the detailed content of every search, significantly improving the efficiency of discovering products or content.

&nbsp;

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/b57290145c504e349d6b7e8426b95a28" width="560px" /></div>


<span id="d714382c"></span>
## Integration Solution

The combined search and query interaction is achieved by integrating the Search and ChatSearch APIs.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/0871762e3f7a459298cdbb9aac50e477" width="4233px" /></div>


The following example illustrates the integration method for combined search and query.

<video src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/e327355c848f4ae4ae3bf6f8949cba23" controls></video>


<span id="82cab34d"></span>
### Step 1: The user enters a query in the conversation

Call the chat_search API to start the conversational search.

```JSON
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/application/{application_id}/chat_search' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: <Signature_String>' \
  -d '{
  "session_id": "session_id",
  "input_message": {
    "content": [
      {
        "type": "text",
        "text": "Recommend highly moisturizing lipsticks"
      }
    ]
  },
  "user": {
    "_user_id": "U109287BsioaJOns05"
  },
  "search_param": {
    "page_size": 20
  },
  "enable_suggestions": true
}'
```


You can specify the **pagination size** for the search results list using the `search_param` parameter when calling the interface. These pagination settings do not affect the quality of the model's generated content; they are used for the subsequent retrieval of the search results list.

<span id="13203c18"></span>
### Step 2: Monitor the streaming output to obtain search call information

The user's query is processed through the model's intent recognition and combined with the extracted historical user query intent from the context, resulting in a rewritten new query. The rewritten query is used for the search when executing the search tool call. You need to monitor the search call information in the streaming output for subsequent post\-search operations such as pagination, sorting, and filtering of the search list.

**When step_info.step is "tool call," obtain the search parameters from step_info.step_payload**

The search parameters are in step_payload.param.search_request:

```JSON
{
    "request_id":"d9bb3f4a025bfced6e75762510d76af0",
    "result":{
        "step_info":{
            "step":"tool call",
            "step_payload":{
                "param":{
                    "tool_name":"search"
                    "search_requests":
                        [
                            {
                                "query":{"text":"highly moisturizing lip balm，highly moisturizing lipstick"},
                                "page_size":20,
                                "page_number":1,
                                "dataset_id":"106261599"
                             }
                        ]
                },
            }
        }
    }
}
```


search_request is a list; when your app is linked to multiple datasets, the model dynamically selects the appropriate dataset for the search. When multiple datasets are selected for a fan\-out search, search_request contains multiple elements, each including:


* `dataset_id`: the dataset ID of the search source

* `query`: the search query

* `page_size`: defaults to 10

* `page_number`: returns the first page by default


<span id="06a8daa4"></span>
### Step 3: Return the first page of search results

You can monitor step_info.step when it is "get results" to obtain the first page of search results from the following output payload.

The search results are returned in payload.search as a list of return results for each dataset searched:

```JSON
{
    "request_id":"8501cb6ab3ff76519cfbd39636168ee1",
    "result":
        {"payload":{
            "search":
                {"106263958":{
                    "search_results":
                    [
                        {
                            "_id":"B08CYY3VFH",
                            "display_fields":{
                                "average_rating":3.799999952316284,
                                "categories":["Beauty \u0026 Personal Care","Makeup","Lips","Lipstick"],
                                "description":[],
                                "details":"{\"Brand\": \"KISSIO\", \"Color\": \"504#\", \"Item Form\": \"Oil\", \"Finish Type\": \"Matte\", \"Age Range (Description)\": \"Adult\", \"Package Dimensions\": \"3.62 x 1.06 x 0.87 inches; 1.52 Ounces\", \"Manufacturer\": \"KISSIO\"}",
                                "features":["Comfortable on lips, Highly pigmented lipgloss comes in both vibrant and soft shades with easy-to-apply matte finishes for beautifully lips.","Perfect Kiss Always, No stickiness, no smudging, no leftover stain marks,The lipgloss makes your lips perfect for a kiss anytime, anywhere,Perfect Gift for Valentine's Day.","Waterproof Long-Lasting, Warm and soft matte texture provides a sexy all-day effect,With its Waterproof Quick Dry design, lips stay Hydrated with less smudging.","Aluminum tube unique design Package,Strong protection lipstick，Magnetic Pakage design for a better user experience.","KISSIO lipstick ,NO fragrance , NO alcohol , NO hormone, NO mineral oil .Contains Vitamin E, Olive oil and natural botanic ingredient.Bring you beauty and nourish your lips."],
                                "images":[{"image_url":"https://m.media-amazon.com/images/I/41eeD6xSByL._SS40_.jpg"}],
                                "item_id":"B08CYY3VFH",
                                "main_category":"All Beauty",
                                "title":"KISSIO Matte Lipstick,Practical colors,Enjoy the new silky，Aluminum tube Lips,Magnetic lipstick,Flicker matte,6 Colors to choose (504#)"
                            },
                            "score":0.014219443323920937,
                            "recall_info":[
                                {
                                    "recall_reason":"text",
                                    "recall_score":0.45546954870224
                                },
                                {
                                    "recall_reason":"vlm",
                                    "recall_score":0.653238832950592
                                }]
                        },
                        ... ...
                    ],
                    "total_items":200,
                    "query":{"text":"highly moisturizing lip balm，highly moisturizing lipstick"},
                    "page_size":20,
                    "page_number":1,
                    "dataset_id":"106263958"
                }
            }
        }
    }
}
```


You can also use the search parameters returned in step_payload.param.search_request to call the search interface and control the length of the search list.

<span id="0e14bb9e"></span>
### Step 4: User triggers post\-search actions

Once the search list is displayed, you will need to use the retrieved search parameters to invoke the `search` interface whenever a user performs operations like pagination, filtering, or sorting on the front end. Taking pagination as an example, it happens when the user clicks "Next Page" on the front\-end interface. 

```JSON
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/application/{application_id}/search' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: <Signature_String>' \
  -d '{
  "query":{
    "text":"highly moisturizing lip balm, highly moisturizing lipstick"
  },
  "dataset_id": "106263958",
  "page_number": 2,
  "page_size": 20
}'
```


When a user triggers post\-search operations such as filtering or sorting, these can be executed by passing the `filter` or `sort_by` parameters. For more details, please refer to  [search interface](https://www.volcengine.com/docs/85296/1544974)
