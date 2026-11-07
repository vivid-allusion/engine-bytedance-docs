---
title: "Create model response"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Create_a_model_response"
---

This document describes the input and output parameters for the Responses API when creating a model request, allowing you to refer to the meaning of each field when using the interface.

<span id="5101e22c"></span>
# Request description


* **Base URL**: Using North China 2 (Beijing) as an example, the Base URL is: https://operator.las.ap\-southeast\-1.bytepluses.com. When actually using the API, you need to use the Base URL for your current service region. For details, see [Usage methods](https://docs.byteplus.com/docs/Byteplus_LAS/Usage_methods).

* **Path**：/api/v1/responses

* **Method**: POST

* **Content\-type**: application/json


<span id="67d94f59"></span>
# Request parameters

The request body parameters are described as follows.

```mixin-react
const properties = ({
  "columns": [
{ "title": "Parameter", "dataIndex": "column_0", "key": "column_0", "width": 300 },
{ "title": "Type", "dataIndex": "column_1", "key": "column_1", "width": 180 },
{ "title": "Required", "dataIndex": "column_2", "key": "column_2", "width": 120 },
{ "title": "Default value", "dataIndex": "column_3", "key": "column_3", "width": 150 },
{ "title": "Description", "dataIndex": "column_4", "key": "column_4", "width": 450 }
  ],
  "data": [
    {
      "key": 1,
      "column_0": "model",
      "column_1": "string",
"column_2": "Yes",
      "column_3": "",
"column_4": <div> The ID (Model ID) of the model you need to call. </div>
    },
    {
      "key": 2,
      "column_0": "input",
      "column_1": "string / array",
"column_2": "Yes",
      "column_3": "",
"column_4": <div> The content to input; the information that the model needs to process. Supported types:<ul><li> Text input (string): Equivalent to the text information entered by the user role. </li><li> List of input elements (array): Contains input information elements of different types. </li></ul></div>,
      "children": [
        {
          "key": 21,
          "column_0": "content",
          "column_1": "string / array",
"column_2": "Yes",
          "column_3": "",
"column_4": "Text, image, or video input used to generate a reply. Can also include the content of previous assistant replies.",
          "children": [
            {
              "key": 211,
              "column_0": "type",
              "column_1": "string",
"column_2": "Yes",
              "column_3": "",
"column_4": <div> The type of input item. Optional values:<ul><li> input_text: Text</li><li> input_image: Image</li><li> input_video: Video</li><li> input_file: File type; currently only PDF files are supported. </li></ul></div>
            },
            {
              "key": 212,
              "column_0": "text",
              "column_1": "string",
"column_2": "Yes",
              "column_3": "",
"column_4": "Text input for the model (when type is input_text)."
            },
            {
              "key": 213,
              "column_0": "image_url",
              "column_1": "string",
"column_2": "No",
              "column_3": "",
"column_4": "The image URL to send to the model (when type is input_image). Can be a complete URL or a base64 image encoded as a data URL."
            },
            {
              "key": 214,
              "column_0": "detail",
              "column_1": "string",
"column_2": "No",
              "column_3": "",
"column_4": <div> Value range: low, high, xhigh. <br/> For details on image understanding granularity, default values for different models, and corresponding pixel ranges, see<a href="https://www.volcengine.com/docs/82379/1362931#bf4d9224" target="_blank"> Control image understanding granularity</a>. </div>
            },
            {
              "key": 215,
              "column_0": "image_pixel_limit",
              "column_1": "object",
"column_2": "No",
              "column_3": "null",
"column_4": <div> The pixel range of the image input to the model. If the image is not within this range, it will be proportionally scaled to fit. <br/> The image pixel range must be within [196, 36,000,000]; otherwise, an error will be returned. <br/><ul><li> Priority: Higher than the detail field. </li><li> Default rule: If image_pixel_limit is not set, the value configured in detail is used. </li></ul></div>,
              "children": [
                {
                  "key": 2151,
                  "column_0": "max_pixels",
                  "column_1": "integer",
"column_2": "No",
                  "column_3": "",
"column_4": <div> Maximum pixel limit for the input image. <ul><li>seedFor models before -1.8, the value range is: (min_pixels, 4014080]</li><li>seedFor -1.8 and -2.0 models, the value range is: (min_pixels, 9031680]seed </li></ul></div>
                },
                {
                  "key": 2152,
                  "column_0": "min_pixels",
                  "column_1": "integer",
"column_2": "No",
                  "column_3": "",
"column_4": <div> Minimum pixel limit for the input image. <ul><li>seedFor models before -1.8, the value range is: [3136, max_pixels)</li><li>seedFor -1.8 and -2.0 models, the value range is: [1764, max_pixels)seed </li></ul></div>
                }
              ]
            },
            {
              "key": 216,
              "column_0": "video_url",
              "column_1": "string",
"column_2": "No",
              "column_3": "",
"column_4": "The video URL to send to the model (when type is input_video). Can be a complete URL or a base64 video encoded as a data URL."
            },
            {
              "key": 219,
              "column_0": "fps",
              "column_1": "float",
"column_2": "No",
              "column_3": "",
"column_4": "Extracts a specified number of images from the video per second. Value range: [0.2, 5]."
            },
            {
              "key": 221,
              "column_0": "file_url",
              "column_1": "string",
"column_2": "No",
              "column_3": "",
"column_4": "Accessible URL of the file (when type is input_file). Currently, only PDF files are supported, and the file size must not exceed 50 MB."
            },
            {
              "key": 218,
              "column_0": "file_data",
              "column_1": "string",
"column_2": "No",
              "column_3": "",
"column_4": "Base64 encoding of the file content. The size of a single file must not exceed 50 MB."
            },
            {
              "key": 220,
              "column_0": "filename",
              "column_1": "string",
"column_2": "No",
              "column_3": "",
"column_4": "File name. This parameter is required when using file_data."
            }
          ]
        },
        {
          "key": 22,
          "column_0": "role",
          "column_1": "string",
"column_2": "Yes",
          "column_3": "",
"column_4": "Role of the input message. Can be user, system, assistant, or developer."
        },
        {
          "key": 23,
          "column_0": "type",
          "column_1": "string",
"column_2": "No",
          "column_3": "message",
"column_4": <div> Type of message input. This should be message. It can also be function_call, function_call_output, reasoning, and so on. </div>
        },
        {
          "key": 24,
          "column_0": "partial",
          "column_1": "boolean",
"column_2": "No",
          "column_3": "",
"column_4": <div> Model continuation mode. To enable continuation mode, set the role of the last message in the input list to assistant and set partial to true. For details, see the <a href="https://www.volcengine.com/docs/82379/1958520#.57ut5YaZ5qih5byP" target="_blank"> documentation</a>. </div>
        },
        {
          "key": 25,
          "column_0": "status",
          "column_1": "string",
"column_2": "No",
          "column_3": "",
"column_4": "Project status. Optional values: in_progress, completed, or incomplete."
        },
        {
          "key": 26,
          "column_0": "arguments",
          "column_1": "string",
"column_2": "Yes",
          "column_3": "",
"column_4": "JSON string of parameters to be passed to the function (when type is function_call)."
        },
        {
          "key": 27,
          "column_0": "call_id",
          "column_1": "string",
"column_2": "Yes",
          "column_3": "",
"column_4": "Unique ID for the function tool call generated by the model (when type is function_call or function_call_output)."
        },
        {
          "key": 28,
          "column_0": "name",
          "column_1": "string",
"column_2": "Yes",
          "column_3": "",
"column_4": "Name of the function to be executed (when type is function_call)."
        },
        {
          "key": 29,
          "column_0": "output",
          "column_1": "string",
"column_2": "Yes",
          "column_3": "",
"column_4": "Result output by the tool after invocation (when type is function_call_output)."
        },
        {
          "key": 210,
          "column_0": "id",
          "column_1": "string",
"column_2": "No",
          "column_3": "",
"column_4": "Unique identifier for chain-of-thought information (when type is reasoning)."
        },
        {
          "key": 211,
          "column_0": "summary",
          "column_1": "array",
"column_2": "No",
          "column_3": "",
"column_4": "Chain-of-thought content (when type is reasoning). Includes text and type (summary_text)."
        }
      ]
    },
    {
      "key": 3,
      "column_0": "instructions",
      "column_1": "string",
"column_2": "No",
      "column_3": "null",
"column_4": <div> Insert a system message or developer as the first instruction in the model context. When used together with previous_response_id, the instruction in the previous response will not be inherited by the next response. This allows you to conveniently replace the system (or developer) message in the new response. <br/> Cannot be used together with caching capability. </div>
    },
    {
      "key": 4,
      "column_0": "previous_response_id",
      "column_1": "string",
"column_2": "No",
      "column_3": "null",
"column_4": <div> Unique identifier of the previous model response. This identifier enables multi-turn conversation. For details on how it works, see the <a href="https://www.volcengine.com/docs/82379/2123288?lang=zh#41d0a095" target="_blank"> multi-turn conversation scenario</a>. </div>
    },
    {
      "key": 5,
      "column_0": "expire_at",
      "column_1": "integer",
"column_2": "No",
      "column_3": "",
"column_4": <div> Set the expiration time for storage. The UTC Unix timestamp must be provided. By default, data is retained for 3 days, up to a maximum of 7 days. </div>
    },
    {
      "key": 6,
      "column_0": "max_output_tokens",
      "column_1": "integer",
"column_2": "No",
      "column_3": "null",
"column_4": "Maximum number of tokens for model output, including model responses and chain-of-thought content."
    },
    {
      "key": 7,
      "column_0": "thinking",
      "column_1": "object",
"column_2": "No",
      "column_3": "",
"column_4": "Controls whether the model enables deep thinking mode.",
      "children": [
        {
          "key": 71,
          "column_0": "type",
          "column_1": "string",
    "column_2": "Yes",
          "column_3": "",
    "column_4": <div> Value range:<ul><li> enabled: enable thinking mode</li><li> disabled: disable thinking mode</li><li> auto: automatic thinking mode</li></ul></div>
        }
      ]
    },
    {
      "key": 8,
      "column_0": "reasoning",
      "column_1": "object",
"column_2": "No",
      "column_3": <div>&#123;"effort": "medium"&#125;</div>,
"column_4": "Limits the workload of deep thinking.",
      "children": [
        {
          "key": 81,
          "column_0": "effort",
          "column_1": "string",
"column_2": "No",
          "column_3": "medium",
"column_4": <div> Value range: minimal, low, medium, high. For models that support this field and its relationship with the thinking.type field, see the <a href="https://www.volcengine.com/docs/82379/1956279?lang=zh#dc4c1547" target="_blank"> documentation</a>. </div>
        }
      ]
    },
    {
      "key": 9,
      "column_0": "caching",
      "column_1": "object",
"column_2": "No",
      "column_3": <div>&#123;"type": "disabled"&#125;</div>,
"column_4": <div> Whether to enable caching. </div>,
      "children": [
        {
          "key": 91,
          "column_0": "type",
          "column_1": "string",
"column_2": "Yes",
          "column_3": "disabled",
"column_4": <div> Value range:<ul><li> enabled: Enable caching</li><li> disabled: Disable caching</li></ul> </div>
        },
        {
          "key": 92,
          "column_0": "prefix",
          "column_1": "boolean",
"column_2": "No",
          "column_3": "false",
"column_4": "true: Only create a public prefix cache; the model does not return a response. false: Do not create a public prefix cache."
        }
      ]
    },
    {
      "key": 10,
      "column_0": "store",
      "column_1": "boolean",
"column_2": "No",
      "column_3": "true",
"column_4": <div> Whether to store the generated model responses for subsequent retrieval via API. </div>
    },
    {
      "key": 11,
      "column_0": "stream",
      "column_1": "boolean",
"column_2": "No",
      "column_3": "false",
"column_4": <div> Whether the response content is returned as a stream. </div>
    },
    {
      "key": 12,
      "column_0": "temperature",
      "column_1": "float",
"column_2": "No",
      "column_3": "1",
"column_4": "Sampling temperature, valid range: [0, 2]."
    },
    {
      "key": 13,
      "column_0": "top_p",
      "column_1": "float",
"column_2": "No",
      "column_3": "0.7",
"column_4": "Nucleus sampling probability threshold, valid range: [0, 1]."
    },
    {
      "key": 14,
      "column_0": "text",
      "column_1": "object",
"column_2": "No",
      "column_3": "",
"column_4": <div> Definition of the model's text output format. It can be in natural language or structured JSON data. For details, see<a href="https://www.volcengine.com/docs/82379/1568221" target="_blank"> Structured output</a>. </div>,
      "children": [
        {
          "key": 141,
          "column_0": "format",
          "column_1": "object",
"column_2": "No",
          "column_3": "&#123;\"type\": \"text\"&#125;",
"column_4": "Specify the format of the model's text output.",
          "children": [
            {
              "key": 1411,
              "column_0": "type",
              "column_1": "string",
"column_2": "Yes",
              "column_3": "text",
"column_4": <div> Type of reply format:<ul><li> text: Natural language</li><li> json_object: JSON object. For examples of structured output, see<a href="https://www.volcengine.com/docs/82379/1585128#.57uT5p6E5YyW6L6T5Ye6" target="_blank"> documentation</a>. </li><li> json_schema: JSON object following Schema. For examples of structured output, see<a href="https://www.volcengine.com/docs/82379/1585128#.anNvbi1zY2hlbWHovpPlh7rmoLzlvI8=" target="_blank"> documentation</a>. </li></ul></div>
            },
            {
              "key": 1412,
              "column_0": "name",
              "column_1": "string",
"column_2": "No",
              "column_3": "",
"column_4": "Name of the custom JSON structure (required when type is json_schema)."
            },
            {
              "key": 1413,
              "column_0": "schema",
              "column_1": "object",
"column_2": "No",
              "column_3": "",
"column_4": "Definition of the JSON format (required when type is json_schema)."
            },
            {
              "key": 1414,
              "column_0": "strict",
              "column_1": "boolean",
"column_2": "No",
              "column_3": "false",
"column_4": "Whether to enable strict schema compliance (available when type is json_schema)."
            },
            {
               "key": 1415,
               "column_0": "description",
               "column_1": "string",
"column_2": "No",
               "column_3": "",
"column_4": "Description of the purpose of the reply."
            }
          ]
        }
      ]
    },
    {
      "key": 15,
      "column_0": "tools",
      "column_1": "array",
"column_2": "No",
      "column_3": "",
"column_4": "List of tools that the model can use.",
      "children": [
        {
          "key": 151,
          "column_0": "type",
          "column_1": "string",
"column_2": "Yes",
          "column_3": "",
"column_4": <div> Tool types:<ul><li> function: custom tools</li><li> mcp: MCP tools</li></ul> </div>
        },
        {
          "key": 152,
          "column_0": "name",
          "column_1": "string",
"column_2": "Yes",
          "column_3": "",
"column_4": "Function name (when type is function)."
        },
        {
          "key": 153,
          "column_0": "description",
          "column_1": "string",
"column_2": "No",
          "column_3": "",
"column_4": "Function description."
        },
        {
          "key": 154,
          "column_0": "parameters",
          "column_1": "object",
"column_2": "Yes",
          "column_3": "",
"column_4": <div> Function request parameters, described using the <a href="https://json-schema.org/understanding-json-schema" target="_blank"> JSON Schema</a> documentation format (when type is function). </div>
        },
        {
          "key": 155,
          "column_0": "strict",
          "column_1": "boolean",
"column_2": "Yes",
          "column_3": "true",
"column_4": "Strict parameter validation (when type is function)."
        },
        {
          "key": 156,
          "column_0": "server_label",
          "column_1": "string",
"column_2": "Yes",
          "column_3": "",
"column_4": "MCP server label (when type is mcp)."
        },
        {
          "key": 157,
          "column_0": "server_url",
          "column_1": "string",
"column_2": "Yes",
          "column_3": "",
"column_4": "MCP server access URL (when type is mcp)."
        },
        {
          "key": 158,
          "column_0": "headers",
          "column_1": "object",
"column_2": "No",
          "column_3": "",
"column_4": "Optional HTTP request headers to be sent to the MCP server. Used for authentication or other purposes. Includes Authorization information (not stored), custom key-value pairs."
        },
        {
          "key": 159,
          "column_0": "require_approval",
          "column_1": "object/string",
"column_2": "No",
"column_3": "always:{ tool a, tool b} ",
"column_4": <div> Specify which MCP server tools require approval. Value range includes:<ul><li> always: Tools require user approval before invocation. You can set the list of tools requiring confirmation by specifying tool names in an array. If no specific tool names are specified, all tools will require user confirmation before invocation. </li><li> never: Tools can be invoked directly without user approval. You can specify the names of specific tools using an array to set the list of tools that require confirmation. If no tool names are specified, it means that all tools do not require confirmation (which may pose a security risk). </li></ul></div>
        },
        {
          "key": 1510,
          "column_0": "allowed_tools",
          "column_1": "array/object",
"column_2": "No",
          "column_3": "",
"column_4": "Tool loading scope. By default, all tools on the current MCP Server are included."
        }
      ]
    },
    {
      "key": 16,
      "column_0": "tool_choice",
      "column_1": "string / object",
"column_2": "No",
      "column_3": "auto",
"column_4": <div> Controls whether the model's response includes the tool to be invoked. </div>,
      "children": [
        {
          "key": 161,
          "column_0": "type",
          "column_1": "string",
"column_2": "Yes",
          "column_3": "",
"column_4": "Type of invocation (function or built-in tool name)."
        },
        {
          "key": 162,
          "column_0": "name",
          "column_1": "string",
"column_2": "No",
          "column_3": "",
"column_4": "Name of the tool to be invoked."
        }
      ]
    },
    {
      "key": 17,
      "column_0": "max_tool_calls",
      "column_1": "integer",
"column_2": "No",
      "column_3": "",
"column_4": "Maximum number of tool call rounds. Value range: [1, 10]."
    },
    {
      "key": 18,
      "column_0": "context_management",
      "column_1": "object",
"column_2": "No",
      "column_3": "",
"column_4": "Context management strategy.",
      "children": [
        {
          "key": 181,
          "column_0": "edits",
          "column_1": "array",
"column_2": "No",
          "column_3": "",
"column_4": "List of supported context editing strategies.",
          "children": [
            {
              "key": 1811,
              "column_0": "type",
              "column_1": "string",
"column_2": "Yes",
              "column_3": "",
"column_4": <div> Strategy types:<ul><li> clear_thinking: Clear thinking blocks</li><li> clear_tool_uses: Clear tool call content</li></ul></ div>
            },
            {
              "key": 1812,
              "column_0": "keep",
              "column_1": "object / string",
"column_2": "No",
              "column_3": "",
"column_4": "Retention strategy. Can be set to all or specify the number of rounds to retain."
            },
            {
              "key": 1813,
              "column_0": "trigger",
              "column_1": "object",
"column_2": "No",
              "column_3": "",
"column_4": "Threshold for triggering the clearing strategy."
            },
            {
              "key": 1814,
              "column_0": "exclude_tools",
              "column_1": "array",
"column_2": "No",
              "column_3": "",
"column_4": "List of tool names that will not be cleared."
            },
            {
              "key": 1815,
              "column_0": "clear_tool_input",
              "column_1": "boolean",
"column_2": "No",
              "column_3": "false",
"column_4": "Whether to clear tool call parameters."
            }
          ]
        }
      ]
    }
  ]
}); 
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```


<span id="5fa6a3c8"></span>
# Response parameters

<span id="6fa7ea15"></span>
## Non\-streaming call return

For details, see [The response object](https://docs.byteplus.com/docs/Byteplus_LAS/The_response_object).

<span id="1546c4e0"></span>
## Streaming call return

For details, see [Streaming response](https://docs.byteplus.com/docs/Byteplus_LAS/Streaming_response).

<span id="2e196316"></span>
# Example

<span id="4c40f031"></span>
## Single\-turn conversation


* request

   ```Bash
   curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/responses" \
   --header "Authorization: Bearer $LAS_API_KEY" \
   --header "Content-Type: application/json" \
   --data '{
       "model": "seed-1-6-250615",
       "input": "你好呀。"
   }'
   ```
   

* response

   ```Bash
   {
     "id": "resp_0217****",
     "created_at": 1756280722.0,
     "error": null,
     "incomplete_details": null,
     "instructions": null,
     "model": "seed-1-6-250615",
     "object": "response",
     "output": [
       {
         "id": "rs_0217****404a",
         "summary": [
           {
             "text": "\n用户说“你好呀。”，这是一个很友好的问候，我需要用同样友好的方式回应。首先，应该回应用户的问候，然后可以表达一下愿意帮助的态度，让对话能够继续下去。用户可能接下来会有其他问题或者想聊聊天，所以回应要自然、亲切。\n\n首先，直接回“你好呀！”来呼应对方的问候，保持一致的语气。然后加上一句“很高兴见到你～ 有什么我可以帮你的吗？”这样既表达了友好，又主动提供帮助，让用户知道我在这里可以协助他们。这样的回应比较温暖，也符合日常交流的习惯，不会显得太生硬。\n\n需要注意的是，用户可能只是想打个招呼，所以回应不要太复杂，保持简洁和亲切就好。避免使用太正式的语言，保持口语化，让用户感觉舒适。总结一下，回应应该包含问候、表达高兴见到对方，以及提供帮助的意愿。",
             "type": "summary_text"
           }
         ],
         "type": "reasoning",
         "status": "completed"
       },
       {
         "id": "msg_0217****a93c",
         "content": [
           {
             "text": "你好呀！很高兴见到你～ 有什么我可以帮你的吗？ 😊",
             "type": "output_text",
             "annotations": null
           }
         ],
         "role": "assistant",
         "status": "completed",
         "type": "message"
       }
     ],
     "parallel_tool_calls": null,
     "temperature": null,
     "tool_choice": null,
     "tools": null,
     "top_p": null,
     "max_output_tokens": 32768,
     "previous_response_id": null,
     "thinking": null,
     "service_tier": "default",
     "status": "completed",
     "text": null,
     "usage": {
       "input_tokens": 88,
       "input_tokens_details": {
         "cached_tokens": 0
       },
       "output_tokens": 230,
       "output_tokens_details": {
         "reasoning_tokens": 211
       },
       "total_tokens": 318
     },
     "caching": {
       "type": "disabled"
     },
     "store": true,
     "expire_at": 1756539922
   }
   ```
   


<span id="12823c91"></span>
## Function calling


* request

   ```Bash
   curl --location 'https://operator.las.ap-southeast-1.bytepluses.com/api/v1/responses' \
   --header "Authorization: Bearer $LAS_API_KEY" \
   --header 'Content-Type: application/json' \
   --data '{
       "model": "seed-1-6-250615",
       "input": "查询北京今天的天气",
       "tools":[
           {
               "type": "function",
               "name": "获取天气信息",
               "description": "根据给出的位置获取天气信息",
               "parameters": {
                   "type": "object",
                   "properties": {
                       "location": {
                           "type": "string",
                           "description": "城市名称，例如：北京"
                       }
                   },
                   "required": [
                       "location"
                   ]
               }
           }
       ]
   }'
   ```
   

* response

   ```Bash
   {
     "id": "resp_0217****b63e",
     "created_at": 1756477803.0,
     "error": null,
     "incomplete_details": null,
     "instructions": null,
     "model": "seed-1-6-250615",
     "object": "response",
     "output": [
       {
         "id": "rs_0217****6b15",
         "summary": [
           {
             "text": "让我思考一下，我现在需要回答用户的问题：“北京的天气怎么样？”根据系统提示，我需要调用工具来获取天气信息。首先，我要确认用户的问题是否需要调用工具。用户询问的是当前北京的天气，这属于实时信息，无法通过常识直接回答，所以必须使用提供的工具。\n\n接下来，查看可用的工具列表，只有一个工具叫做“获取天气信息”，它的参数需要一个“location”，类型是字符串，必填项。用户的问题中明确提到了“北京”，所以location参数应该是“北京”。\n\n然后，我需要按照格式要求生成工具调用。系统提示说调用工具需要用包裹，里面是一个JSON数组。这里只需要调用一个工具，所以是单工具调用。参数部分应该是{\"location\": \"北京\"}。\n\n检查是否有其他需要注意的地方，比如参数是否正确，格式是否符合要求。确认无误后，生成调用语句。不需要并行调用，因为只有一个工具可用，且只需要一次调用就能获取所需信息。因此，最终的调用应该是：\n\n",
             "type": "summary_text"
           }
         ],
         "type": "reasoning",
         "status": "completed"
       },
       {
         "arguments": "{\"location\":\"北京\"}",
         "call_id": "call_****a6al",
         "name": "获取天气信息",
         "type": "function_call",
         "id": "fc_0217****c976b",
         "status": "completed"
       }
     ],
     "parallel_tool_calls": null,
     "temperature": null,
     "tool_choice": null,
     "tools": [
       {
         "name": "获取天气信息",
         "parameters": {
           "type": "object",
           "properties": {
             "location": {
               "type": "string",
               "description": "城市名称，例如：北京"
             }
           },
           "required": ["location"]
         },
         "type": "function",
         "description": "根据给出的位置获取天气信息"
       }
     ],
     "top_p": null,
     "max_output_tokens": 32768,
     "previous_response_id": null,
     "thinking": null,
     "service_tier": "default",
     "status": "completed",
     "text": null,
     "usage": {
       "input_tokens": 454,
       "input_tokens_details": {
         "cached_tokens": 0
       },
       "output_tokens": 306,
       "output_tokens_details": {
         "reasoning_tokens": 279
       },
       "total_tokens": 760
     },
     "caching": {
       "type": "disabled"
     },
     "store": true,
     "expire_at": 1756737003
   }
   ```
