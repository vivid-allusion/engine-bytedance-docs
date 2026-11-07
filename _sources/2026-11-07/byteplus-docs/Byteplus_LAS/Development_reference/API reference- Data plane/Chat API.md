---
title: "Chat API"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Chat_API"
---

<span id="46c942b1"></span>
# Request description

Send a list of messages containing modalities such as text, images, videos, and more. The model will generate the next message in the conversation.


* **Base URL**: For example, in the North China 2 (Beijing) region, the Base URL is: https://operator.las.ap\-southeast\-1.bytepluses.com. When actually using the service, you need to use the Base URL for your current service region. For details, see [Usage methods](https://docs.byteplus.com/docs/Byteplus_LAS/Usage_methods).

* **Path**：/api/v1/chat/completions

* **Method**: POST

* **Content\-type**: application/json


<span id="79c134b4"></span>
# Request parameters

```mixin-react
const properties = ({
  "columns": [
    {
"title": "Parameter name",
      "dataIndex": "column_0",
      "key": "column_0",
      "width": 300
    },
    {
"title": "Data type",
      "dataIndex": "column_1",
      "key": "column_1",
      "width": 150
    },
    {
"title": "Required",
      "dataIndex": "column_2",
      "key": "column_2",
      "width": 80
    },
    {
"title": "Parameter description",
      "dataIndex": "column_3",
      "key": "column_3"
    }
  ],
  "data": [
    {
      "key": 1,
      "column_0": "model",
      "column_1": "string",
"column_2": "Yes",
"column_3": "The model ID to call. After enabling the model service, query to obtain it. For multiple applications and fine-grained management scenarios, it is recommended to use Endpoint ID for invocation."
    },
    {
      "key": 2,
      "column_0": "messages",
      "column_1": "object[]",
"column_2": "Yes",
"column_3": "List of messages. Different models support different types of messages, such as text, images, videos, and more.",
      "children": [
        {
          "key": 21,
          "column_0": "role",
          "column_1": "string",
"column_2": "Yes",
"column_3": "The role sending the message. Optional values: system (system message), user (user message), assistant (model message), tool (tool message)."
        },
        {
          "key": 22,
          "column_0": "content",
          "column_1": "string / object[]",
"column_2": "Yes",
"column_3": "Message content. For plain text messages, pass a string. For multimodal messages, pass an array of objects (including text, image, video, and more modalities).",
          "children": [
            {
              "key": 221,
              "column_0": "type",
              "column_1": "string",
"column_2": "Yes",
"column_3": "When passing an array of objects for message content, use this field to define the modality type. Optional values: text (text), image_url (image), video_url (video), and more."
            },
            {
              "key": 222,
              "column_0": "text",
              "column_1": "string",
"column_2": "Yes",
"column_3": "Content of the text modality (required only when content is a multimodal object array and the type is text)."
            },
            {
              "key": 223,
              "column_0": "image_url",
              "column_1": "object",
"column_2": "Yes",
"column_3": "Content of the image modality (required only when content.type is image_url).",
              "children": [
                {
                  "key": 2231,
                  "column_0": "url",
                  "column_1": "string",
"column_2": "Yes",
"column_3": "Image resource identifier. Supports image links or Base64 encoding."
                },
                {
                  "key": 2232,
                  "column_0": "detail",
                  "column_1": "string",
"column_2": "No",
"column_3": "Image understanding granularity. Optional values: high (high detail), low (low detail);seed-1.8 models default to low, 1.8 and above default to high."
                },
                {
                  "key": 2233,
                  "column_0": "image_pixel_limit",
                  "column_1": "object",
"column_2": "No",
"column_3": "Image pixel range limit. This takes precedence over the detail field. If not set, the default pixel range corresponding to detail is used.",
                  "children": [
                    {
                      "key": 22331,
                      "column_0": "max_pixels",
                      "column_1": "integer",
"column_2": "No",
"column_3": "Maximum image pixel limit. seed-1.8 models value range (min_pixels, 4014080], 1.8 and above models value range (min_pixels, 9031680)"
                    },
                    {
                      "key": 22332,
                      "column_0": "min_pixels",
                      "column_1": "integer",
"column_2": "No",
"column_3": "Minimum image pixel limit. seed-1.8 models value range [3136, max_pixels), 1.8 and above models value range [1764, max_pixels)"
                    }
                  ]
                }
              ]
            },
            {
              "key": 224,
              "column_0": "video_url",
              "column_1": "object",
"column_2": "Yes",
"column_3": "Content of the video modality (required only when content.type is video_url). Audio content in the video is not supported for understanding.",
              "children": [
                {
                  "key": 2241,
                  "column_0": "url",
                  "column_1": "string",
"column_2": "Yes",
"column_3": "Video resource identifier. Supports video links or Base64 encoding."
                },
                {
                  "key": 2242,
                  "column_0": "fps",
                  "column_1": "float / null",
"column_2": "No",
"column_3": "Frame sampling frequency, value range [0.2, 5], default value 1; higher values make the model more sensitive to changes in the image, lower values reduce token consumption and increase speed"
                }
              ]
            }
          ]
        },
        {
          "key": 23,
          "column_0": "tool_calls",
          "column_1": "object[]",
"column_2": "No",
"column_3": "Model tool call section (only required when messages.role is assistant and tool invocation is needed)",
          "children": [
            {
              "key": 231,
              "column_0": "id",
              "column_1": "string",
"column_2": "Yes",
"column_3": "Tool call ID (generated by the model)"
            },
            {
              "key": 232,
              "column_0": "type",
              "column_1": "string",
"column_2": "Yes",
"column_3": "Message type, currently only function is supported"
            },
            {
              "key": 233,
              "column_0": "function",
              "column_1": "object",
"column_2": "Yes",
"column_3": "Function information for tool call",
              "children": [
                {
                  "key": 2331,
                  "column_0": "name",
                  "column_1": "string",
"column_2": "Yes",
"column_3": "Name of the function to be called"
                },
                {
                  "key": 2332,
                  "column_0": "arguments",
                  "column_1": "string",
"column_2": "Yes",
"column_3": "Function input parameters, in JSON format (parameter validity must be verified)"
                }
              ]
            }
          ]
        },
        {
          "key": 24,
          "column_0": "tool_call_id",
          "column_1": "string",
"column_2": "Yes",
"column_3": "Tool call ID (only required when messages.role is tool)"
        },
        {
          "key": 25,
          "column_0": "reasoning_content",
          "column_1": "string",
"column_2": "No",
"column_3": "Model reasoning chain content (only supported by seed-1-8-251228, deepseek-v3-2-251201 models)"
        }
      ]
    },
    {
      "key": 3,
      "column_0": "thinking",
      "column_1": "object",
"column_2": "No",
"column_3": "Controls the model's deep thinking mode, default value {\"type\":\"enabled\"}",
      "children": [
        {
          "key": 31,
          "column_0": "type",
          "column_1": "string",
"column_2": "Yes",
"column_3": "Thinking mode, optional values: enabled (forced reasoning), disabled (direct answer), auto (automatic judgment)"
        }
      ]
    },
    {
      "key": 4,
      "column_0": "stream",
      "column_1": "boolean / null",
"column_2": "No",
"column_3": "Whether the response is returned in streaming mode, default value is false; when true, returns in blocks according to the SSE protocol, ending with data: [DONE]"
    },
    {
      "key": 5,
      "column_0": "stream_options",
      "column_1": "object / null",
"column_2": "No",
"column_3": "Streaming response options (can only be set when stream is true)",
      "children": [
        {
          "key": 51,
          "column_0": "include_usage",
          "column_1": "boolean / null",
"column_2": "No",
"column_3": "Whether to return the total token usage before the end of streaming output, default value is false"
        },
        {
          "key": 52,
          "column_0": "chunk_include_usage",
          "column_1": "boolean / null",
"column_2": "No",
"column_3": "Whether each streaming chunk returns cumulative token usage, default value is false"
        }
      ]
    },
    {
      "key": 6,
      "column_0": "max_tokens",
      "column_1": "integer / null",
"column_2": "No",
"column_3": "Maximum length of model response (in tokens), default value is 4096; does not include reasoning chain content, subject to model context length limit"
    },
    {
      "key": 7,
      "column_0": "max_completion_tokens",
      "column_1": "integer / null",
"column_2": "No",
"column_3": "Maximum length of model output (including response and reasoning chain, in tokens), value range [0, 65536]; mutually exclusive with max_tokens, max_tokens becomes invalid when configured"
    },
    {
      "key": 8,
      "column_0": "service_tier",
      "column_1": "string / null",
"column_2": "No",
"column_3": "TPM protection package usage control, default value is auto; auto prioritizes quota usage, default does not use"
    },
    {
      "key": 9,
      "column_0": "stop",
      "column_1": "string / string[] / null",
"column_2": "No",
"column_3": "Trigger condition for model to stop generating, supports up to 4 strings; not supported by deep reasoning models"
    },
    {
      "key": 10,
      "column_0": "reasoning_effort",
      "column_1": "string / null",
"column_2": "No",
"column_3": "Reasoning workload limit, default value is medium; optional values: minimal (reasoning disabled), low (lightweight reasoning), medium (balanced), high (in-depth analysis)"
    },
    {
      "key": 11,
      "column_0": "response_format",
      "column_1": "object",
"column_2": "No",
"column_3": "Model response format, default value {\"type\": \"text\"} (beta stage)",
      "children": [
        {
          "key": 111,
          "column_0": "type",
          "column_1": "string",
"column_2": "Yes",
"column_3": "Response format type, optional values: text (text), json_object (JSON object), json_schema (follows specified JSON Schema)"
        },
        {
          "key": 112,
          "column_0": "json_schema",
          "column_1": "object",
"column_2": "Yes",
"column_3": "JSON Schema definition (only required when response_format.type is json_schema)",
          "children": [
            {
              "key": 1121,
              "column_0": "name",
              "column_1": "string",
"column_2": "Yes",
"column_3": "Custom JSON structure name"
            },
            {
              "key": 1122,
              "column_0": "description",
              "column_1": "string / null",
"column_2": "No",
"column_3": "Description of reply purpose, used for model format adaptation judgment"
            },
            {
              "key": 1123,
              "column_0": "schema",
              "column_1": "object",
"column_2": "Yes",
"column_3": "JSON Schema definition for reply format"
            },
            {
              "key": 1124,
              "column_0": "strict",
              "column_1": "boolean / null",
"column_2": "No",
"column_3": "Whether to strictly follow the Schema, default value is false"
            }
          ]
        }
      ]
    },
    {
      "key": 12,
      "column_0": "frequency_penalty",
      "column_1": "float / null",
"column_2": "No",
"column_3": "Frequency penalty coefficient, value range [-2.0, 2.0], default value is 0; positive values reduce the probability of repeated tokens"
    },
    {
      "key": 13,
      "column_0": "presence_penalty",
      "column_1": "float / null",
"column_2": "No",
"column_3": "A penalty coefficient is present, value range [-2.0, 2.0], default value 0; positive values increase the probability of new topic tokens"
    },
    {
      "key": 14,
      "column_0": "temperature",
      "column_1": "float / null",
"column_2": "No",
"column_3": "Sampling temperature, value range [0, 2], default value 1; higher values result in more randomness, lower values result in more determinism (it is recommended to adjust only one of temperature or top_p)"
    },
    {
      "key": 15,
      "column_0": "top_p",
      "column_1": "float / null",
"column_2": "No",
"column_3": "Nucleus sampling probability threshold, value range [0, 1], default value 0.7; controls the probability quality range of candidate tokens (it is recommended to adjust only one of temperature or top_p)"
    },
    {
      "key": 16,
      "column_0": "logprobs",
      "column_1": "boolean / null",
"column_2": "No",
"column_3": "Whether to return the log probability of output tokens, default value is false; not supported by deep reasoning models"
    },
    {
      "key": 17,
      "column_0": "top_logprobs",
      "column_1": "integer / null",
"column_2": "No",
"column_3": "Maximum number of possible tokens returned at each token position, value range [0, 20], default value 0; only effective when logprobs is true, not supported by deep reasoning models"
    },
    {
      "key": 18,
      "column_0": "tools",
      "column_1": "object[] / null",
"column_2": "No",
"column_3": "List of tools to be called (must be configured when the model returns tool calls)",
      "children": [
        {
          "key": 181,
          "column_0": "type",
          "column_1": "string",
"column_2": "Yes",
"column_3": "Tool type, should be function here"
        },
        {
          "key": 182,
          "column_0": "function",
          "column_1": "object",
"column_2": "Yes",
"column_3": "Tool function information",
          "children": [
            {
              "key": 1821,
              "column_0": "name",
              "column_1": "string",
"column_2": "Yes",
"column_3": "Tool function name"
            },
            {
              "key": 1822,
              "column_0": "description",
              "column_1": "string",
"column_2": "No",
"column_3": "Tool function description, used for the model to determine whether to call"
            },
            {
              "key": 1823,
              "column_0": "parameters",
              "column_1": "object",
"column_2": "No",
"column_3": "Function request parameters, described in JSON Schema format"
            }
          ]
        }
      ]
    },
    {
      "key": 19,
      "column_0": "parallel_tool_calls",
      "column_1": "boolean",
"column_2": "No",
"column_3": "Whether multiple tool calls are allowed to be returned, default value is true; when false, at most one will be returned (only seed-1-6-*** models are effective)"
    },
    {
      "key": 20,
      "column_0": "tool_choice",
      "column_1": "string / object",
"column_2": "No",
"column_3": "Tool call control (only seed-1-6-*** and later models are supported); for string type, options are none (no tool), required (must call), auto (automatic decision); for object type, specify the specific tool",
      "children": [
        {
          "key": 201,
          "column_0": "type",
          "column_1": "string",
"column_2": "Yes",
"column_3": "Call type, should be function here (only required when tool_choice is an object)"
        },
        {
          "key": 202,
          "column_0": "function",
          "column_1": "object",
"column_2": "Yes",
"column_3": "Specify tool information (only required when tool_choice is an object)",
          "children": [
            {
              "key": 2021,
              "column_0": "name",
              "column_1": "string",
"column_2": "Yes",
"column_3": "Name of the tool to be called"
            }
          ]
        }
      ]
    }
  ]
}); 
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```


<span id="7cdb1366"></span>
# Response parameters

<span id="fbd1234d"></span>
## Non\-streaming response

```mixin-react
const properties = ({
  "columns": [
    {
"title": "Parameter name",
      "dataIndex": "column_0",
      "key": "column_0",
      "width": 300
    },
    {
"title": "Data type",
      "dataIndex": "column_1",
      "key": "column_1",
      "width": 150
    },
    {
"title": "Parameter description",
      "dataIndex": "column_2",
      "key": "column_2"
    }
  ],
  "data": [
    {
      "key": 1,
      "column_0": "id",
      "column_1": "string",
"column_2": "Unique identifier for this request"
    },
    {
      "key": 2,
      "column_0": "model",
      "column_1": "string",
"column_2": "Name and version of the model actually used for this request"
    },
    {
      "key": 3,
      "column_0": "service_tier",
      "column_1": "string",
"column_2": "TPM protection package usage status, optional values: scale (quota used), default (not used)"
    },
    {
      "key": 4,
      "column_0": "created",
      "column_1": "integer",
"column_2": "Unix timestamp (seconds) of request creation time"
    },
    {
      "key": 5,
      "column_0": "object",
      "column_1": "string",
"column_2": "Returned object type, fixed as chat.completion"
    },
    {
      "key": 6,
      "column_0": "choices",
      "column_1": "object[]",
"column_2": "List of model output contents",
      "children": [
        {
          "key": 61,
          "column_0": "index",
          "column_1": "integer",
"column_2": "Index of the current element in the choices list"
        },
        {
          "key": 62,
          "column_0": "finish_reason",
          "column_1": "string",
"column_2": "Reason for model generation stop, optional values: stop (natural end / hit stop field), length (reached length limit), content_filter (content moderation interception), tool_calls (tool invocation)"
        },
        {
          "key": 63,
          "column_0": "message",
          "column_1": "object",
"column_2": "Complete message output by the model",
          "children": [
            {
              "key": 631,
              "column_0": "role",
              "column_1": "string",
"column_2": "Output role, fixed as assistant"
            },
            {
              "key": 632,
              "column_0": "content",
              "column_1": "string",
"column_2": "Content of the message generated by the model"
            },
            {
              "key": 633,
              "column_0": "reasoning_content",
              "column_1": "string / null",
"column_2": "Model chain-of-thought content (only supported by deep reasoning models)"
            },
            {
              "key": 634,
              "column_0": "tool_calls",
              "column_1": "object[] / null",
"column_2": "Tool call information generated by the model",
              "children": [
                {
                  "key": 6341,
                  "column_0": "id",
                  "column_1": "string",
"column_2": "Tool call ID"
                },
                {
                  "key": 6342,
                  "column_0": "type",
                  "column_1": "string",
"column_2": "Tool type, currently only function is supported"
                },
                {
                  "key": 6343,
                  "column_0": "function",
                  "column_1": "object",
"column_2": "Function information for the tool call",
                  "children": [
                    {
                      "key": 63431,
                      "column_0": "name",
                      "column_1": "string",
"column_2": "Name of the called function"
                    },
                    {
                      "key": 63432,
                      "column_0": "arguments",
                      "column_1": "string",
"column_2": "Function arguments (JSON format; validity must be verified)"
                    }
                  ]
                }
              ]
            }
          ]
        },
        {
          "key": 64,
          "column_0": "logprobs",
          "column_1": "object / null",
"column_2": "Log probability information for output tokens (returned only when logprobs is true)",
          "children": [
            {
              "key": 641,
              "column_0": "content",
              "column_1": "object[] / null",
"column_2": "Log probability details for each content element's token",
              "children": [
                {
                  "key": 6411,
                  "column_0": "token",
                  "column_1": "string",
"column_2": "Current token content"
                },
                {
                  "key": 6412,
                  "column_0": "bytes",
                  "column_1": "integer[] / null",
"column_2": "UTF-8 encoding of the current token"
                },
                {
                  "key": 6413,
                  "column_0": "logprob",
                  "column_1": "float",
"column_2": "Log probability of the current token"
                },
                {
                  "key": 6414,
                  "column_0": "top_logprobs",
                  "column_1": "object[]",
"column_2": "List of the most probable tokens and their log probabilities at the current position",
                  "children": [
                    {
                      "key": 64141,
                      "column_0": "token",
                      "column_1": "string",
"column_2": "Candidate token content"
                    },
                    {
                      "key": 64142,
                      "column_0": "bytes",
                      "column_1": "integer[] / null",
"column_2": "UTF-8 encoding of the candidate token"
                    },
                    {
                      "key": 64143,
                      "column_0": "logprob",
                      "column_1": "float",
"column_2": "Log probability of the candidate token"
                    }
                  ]
                }
              ]
            }
          ]
        },
        {
          "key": 65,
          "column_0": "moderation_hit_type",
          "column_1": "string / null",
"column_2": "Sensitive information risk classification label. Optional values: severe_violation (severe violation), violence (violent behavior); returned only for vision understanding models and when the content guardrail is set to Basic."
        }
      ]
    },
    {
      "key": 7,
      "column_0": "usage",
      "column_1": "object / null",
"column_2": "Token usage statistics",
      "children": [
        {
          "key": 71,
          "column_0": "total_tokens",
          "column_1": "integer",
"column_2": "Total token consumption (input + output)"
        },
        {
          "key": 72,
          "column_0": "prompt_tokens",
          "column_1": "integer",
"column_2": "Number of tokens in the input content"
        },
        {
          "key": 73,
          "column_0": "prompt_tokens_details",
          "column_1": "object",
"column_2": "Details of input token count",
          "children": [
            {
              "key": 731,
              "column_0": "cached_tokens",
              "column_1": "integer",
"column_2": "Token usage for cached input, fixed at 0"
            }
          ]
        },
        {
          "key": 74,
          "column_0": "completion_tokens",
          "column_1": "integer",
"column_2": "Number of tokens in the output content"
        },
        {
          "key": 75,
          "column_0": "completion_tokens_details",
          "column_1": "object",
"column_2": "Details of output token count",
          "children": [
            {
              "key": 751,
              "column_0": "reasoning_tokens",
              "column_1": "integer",
"column_2": "Token consumption for chain-of-thought content (only supported for chain-of-thought models)"
            }
          ]
        }
      ]
    }
  ]
}); 
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```


<span id="e6069dd4"></span>
## Streaming response

```mixin-react
const properties = ({
  "columns": [
    {
"title": "Parameter name",
      "dataIndex": "column_0",
      "key": "column_0",
      "width": 300
    },
    {
"title": "Data type",
      "dataIndex": "column_1",
      "key": "column_1",
      "width": 150
    },
    {
"title": "Parameter description",
      "dataIndex": "column_2",
      "key": "column_2"    }
  ],
  "data": [
    {
      "key": 1,
      "column_0": "id",
      "column_1": "string",
"column_2": "Unique identifier for this request"
    },
    {
      "key": 2,
      "column_0": "model",
      "column_1": "string",
"column_2": "Model name and version actually used for this request"
    },
    {
      "key": 3,
      "column_0": "service_tier",
      "column_1": "string",
"column_2": "TPM package usage status. Optional values: scale (quota used), default (not used)"
    },
    {
      "key": 4,
      "column_0": "created",
      "column_1": "integer",
"column_2": "Unix timestamp (seconds) for request creation time"
    },
    {
      "key": 5,
      "column_0": "object",
      "column_1": "string",
"column_2": "Returned object type, fixed as chat.completion.chunk"
    },
    {
      "key": 6,
      "column_0": "choices",
      "column_1": "object[]",
"column_2": "List of model output content",
      "children": [
        {
          "key": 61,
          "column_0": "index",
          "column_1": "integer",
"column_2": "Index of the current element in the choices list"
        },
        {
          "key": 62,
          "column_0": "finish_reason",
          "column_1": "string",
"column_2": "Reason for model generation stop. Optional values: stop (natural end / hit stop field), length (reached length limit), content_filter (content moderation interception), tool_calls (tool call)"
        },
        {
          "key": 63,
          "column_0": "delta",
          "column_1": "object",
"column_2": "Incremental content output by the model",
          "children": [
            {
              "key": 631,
              "column_0": "role",
              "column_1": "string",
"column_2": "Output role, fixed as assistant"
            },
            {
              "key": 632,
              "column_0": "content",
              "column_1": "string",
"column_2": "Incremental message content generated by the model"
            },
            {
              "key": 633,
              "column_0": "reasoning_content",
              "column_1": "string / null",
"column_2": "Incremental chain-of-thought content from the model (only supported by deep reasoning models)"
            },
            {
              "key": 634,
              "column_0": "tool_calls",
              "column_1": "object[] / null",
"column_2": "Incremental tool call information generated by the model",
              "children": [
                {
                  "key": 6341,
                  "column_0": "id",
                  "column_1": "string",
"column_2": "Tool call ID"
                },
                {
                  "key": 6342,
                  "column_0": "type",
                  "column_1": "string",
"column_2": "Tool type, currently only function is supported"
                },
                {
                  "key": 6343,
                  "column_0": "function",
                  "column_1": "object",
"column_2": "Function information for the tool call",
                  "children": [
                    {
                      "key": 63431,
                      "column_0": "name",
                      "column_1": "string",
"column_2": "Name of the called function"
                    },
                    {
                      "key": 63432,
                      "column_0": "arguments",
                      "column_1": "string",
"column_2": "Function arguments (JSON format; validity must be verified)"
                    }
                  ]
                }
              ]
            }
          ]
        },
        {
          "key": 64,
          "column_0": "logprobs",
          "column_1": "object / null",
"column_2": "Log probability information for output tokens (returned only when logprobs is true)",
          "children": [
            {
              "key": 641,
              "column_0": "content",
              "column_1": "object[] / null",
"column_2": "Log probability details for each content element's token",
              "children": [
                {
                  "key": 6411,
                  "column_0": "token",
                  "column_1": "string",
"column_2": "Current token content"
                },
                {
                  "key": 6412,
                  "column_0": "bytes",
                  "column_1": "integer[] / null",
"column_2": "UTF-8 encoding of the current token"
                },
                {
                  "key": 6413,
                  "column_0": "logprob",
                  "column_1": "float",
"column_2": "Log probability of the current token"
                },
                {
                  "key": 6414,
                  "column_0": "top_logprobs",
                  "column_1": "object[]",
"column_2": "List of the most probable tokens and their log probabilities at the current position",
                  "children": [
                    {
                      "key": 64141,
                      "column_0": "token",
                      "column_1": "string",
"column_2": "Candidate token content"
                    },
                    {
                      "key": 64142,
                      "column_0": "bytes",
                      "column_1": "integer[] / null",
"column_2": "UTF-8 encoding of the candidate token"
                    },
                    {
                      "key": 64143,
                      "column_0": "logprob",
                      "column_1": "float",
"column_2": "Log probability of the candidate token"
                    }
                  ]
                }
              ]
            }
          ]
        },
        {
          "key": 65,
          "column_0": "moderation_hit_type",
          "column_1": "string / null",
"column_2": "Sensitive information risk classification label. Optional values: severe_violation (severe violation), violence (violent behavior). Returned only when the visual understanding model is used and the content guard is set to the Basic plan."
        }
      ]
    },
    {
      "key": 7,
      "column_0": "usage",
      "column_1": "object / null",
"column_2": "Token usage statistics. Returned only when stream_options.include_usage is set to true.",
      "children": [
        {
          "key": 71,
          "column_0": "total_tokens",
          "column_1": "integer",
"column_2": "Total token consumption (input + output)"
        },
        {
          "key": 72,
          "column_0": "prompt_tokens",
          "column_1": "integer",
"column_2": "Number of tokens in the input content"
        },
        {
          "key": 73,
          "column_0": "prompt_tokens_details",
          "column_1": "object",
"column_2": "Details of the number of input tokens",
          "children": [
            {
              "key": 731,
              "column_0": "cached_tokens",
              "column_1": "integer",
"column_2": "Token usage for cached input, fixed at 0"
            }
          ]
        },
        {
          "key": 74,
          "column_0": "completion_tokens",
          "column_1": "integer",
"column_2": "Number of tokens in the output content"
        },
        {
          "key": 75,
          "column_0": "completion_tokens_details",
          "column_1": "object",
"column_2": "Details of the number of output tokens",
          "children": [
            {
              "key": 751,
              "column_0": "reasoning_tokens",
              "column_1": "integer",
"column_2": "Token consumption for chain-of-thought content (returned only for chain-of-thought models)"
            }
          ]
        }
      ]
    }
  ]
}); 
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```


<span id="b87fb0fd"></span>
# Examples

<span id="3079a868"></span>
## Streaming output


* request

   
   <Tabs>
   <Tab zoneid="K5sYX423o1" title="curl">
   <TabTitle>curl</TabTitle>
   
   ```Bash
   curl https://operator.las.ap-southeast-1.bytepluses.com/api/v1/chat/completions \
     -H "Content-Type: application/json" \
     -H "Authorization: Bearer $ARK_API_KEY" \
     -d $'{
       "messages": [
           {
               "content": "You are a helpful assistant.",
               "role": "system"
           },
           {
               "content": "hello",
               "role": "user"
           }
       ],
       "model": "seed-1-5-pro-32k-250115",
       "stream": true
   }'
   ```
   
   
   
   </Tab>
   </Tabs>
   

* response

   
   <Tabs>
   <Tab zoneid="ETdA3rNBwh" title="curl">
   <TabTitle>curl</TabTitle>
   
   ```Bash
   {"choices":[{"delta":{"content":"Hello","role":"assistant"},"index":0}],"created":1742632436,"id":"021742632435712396f12d018b5d576a7a55349c2eba0815061fc","model":"seed-1-5-pro-32k-250115","service_tier":"default","object":"chat.completion.chunk","usage":null}
   
   {"choices":[{"delta":{"content":"!","role":"assistant"},"index":0}],"created":1742632436,"id":"021742632435712396f12d018b5d576a7a55349c2eba0815061fc","model":"seed-1-5-pro-32k-250115","service_tier":"default","object":"chat.completion.chunk","usage":null}
   
   {"choices":[{"delta":{"content":" How","role":"assistant"},"index":0}],"created":1742632436,"id":"021742632435712396f12d018b5d576a7a55349c2eba0815061fc","model":"seed-1-5-pro-32k-250115","service_tier":"default","object":"chat.completion.chunk","usage":null}
   
   {"choices":[{"delta":{"content":" can","role":"assistant"},"index":0}],"created":1742632436,"id":"021742632435712396f12d018b5d576a7a55349c2eba0815061fc","model":"seed-1-5-pro-32k-250115","service_tier":"default","object":"chat.completion.chunk","usage":null}
   
   {"choices":[{"delta":{"content":" I","role":"assistant"},"index":0}],"created":1742632436,"id":"021742632435712396f12d018b5d576a7a55349c2eba0815061fc","model":"seed-1-5-pro-32k-250115","service_tier":"default","object":"chat.completion.chunk","usage":null}
   
   {"choices":[{"delta":{"content":" help","role":"assistant"},"index":0}],"created":1742632436,"id":"021742632435712396f12d018b5d576a7a55349c2eba0815061fc","model":"seed-1-5-pro-32k-250115","service_tier":"default","object":"chat.completion.chunk","usage":null}
   
   {"choices":[{"delta":{"content":" you","role":"assistant"},"index":0}],"created":1742632436,"id":"021742632435712396f12d018b5d576a7a55349c2eba0815061fc","model":"seed-1-5-pro-32k-250115","service_tier":"default","object":"chat.completion.chunk","usage":null}
   
   {"choices":[{"delta":{"content":" today","role":"assistant"},"index":0}],"created":1742632436,"id":"021742632435712396f12d018b5d576a7a55349c2eba0815061fc","model":"seed-1-5-pro-32k-250115","service_tier":"default","object":"chat.completion.chunk","usage":null}
   
   {"choices":[{"delta":{"content":"?","role":"assistant"},"index":0}],"created":1742632436,"id":"021742632435712396f12d018b5d576a7a55349c2eba0815061fc","model":"seed-1-5-pro-32k-250115","service_tier":"default","object":"chat.completion.chunk","usage":null}
   
   {"choices":[{"delta":{"content":"","role":"assistant"},"finish_reason":"stop","index":0}],"created":1742632436,"id":"021742632435712396f12d018b5d576a7a55349c2eba0815061fc","model":"seed-1-5-pro-32k-250115","service_tier":"default","object":"chat.completion.chunk","usage":null}
   
   [DONE]
   ```
   
   
   
   </Tab>
   </Tabs>
   


<span id="a2fbd23c"></span>
## Continuation mode


* request

   
   <Tabs>
   <Tab zoneid="TAuK2u0WUe" title="curl">
   <TabTitle>curl</TabTitle>
   
   ```Bash
   curl https://operator.las.ap-southeast-1.bytepluses.com//api/v1/chat/completions \
     -H "Content-Type: application/json" \
     -H "Authorization: Bearer $ARK_API_KEY" \
     -d $'{
       "messages": [
           {
               "content": "You are a calculator, please calculate: 1 + 1",
               "role": "user"
           },
           {
               "content": "=",
               "role": "assistant"
           }
       ],
       "model": "seed-1-5-pro-32k-250115"
   }'
   ```
   
   
   
   </Tab>
   </Tabs>
   

* response

   
   <Tabs>
   <Tab zoneid="pZDwESSDgV" title="curl">
   <TabTitle>curl</TabTitle>
   
   ```Bash
   {
     "choices": [
       {
         "finish_reason": "stop",
         "index": 0,
         "logprobs": null,
         "message": {
           "content": " 2",
           "role": "assistant"
         }
       }
     ],
     "created": 1742634165,
     "id": "0217426341647344ee2a242cadeb3c7acc981f0bd805884bc65fc",
     "model": "seed-1-5-pro-32k-250115",
     "service_tier": "default",
     "object": "chat.completion",
     "usage": {
       "completion_tokens": 2,
       "prompt_tokens": 21,
       "total_tokens": 23,
       "prompt_tokens_details": {
         "cached_tokens": 0
       },
       "completion_tokens_details": {
         "reasoning_tokens": 0
       }
     }
   }
   ```
   
   
   
   </Tab>
   </Tabs>
   


<span id="3b06831f"></span>
## Image understanding


* request

   
   <Tabs>
   <Tab zoneid="KuKBgHILQ2" title="curl">
   <TabTitle>curl</TabTitle>
   
   ```Bash
   curl https://operator.las.ap-southeast-1.bytepluses.com//api/v1/chat/completions \
     -H "Content-Type: application/json" \
     -H "Authorization: Bearer $ARK_API_KEY" \
     -d $'{
       "model": "seed-1-5-vision-pro-32k-250115",
       "messages": [
           {
               "content": [
                   {
                       "image_url": {
                           "url": "https://ark-project.tos-cn-beijing.volces.com/images/view.jpeg"
                       },
                       "type": "image_url"
                   },
                   {
                       "text": "What is the main theme of the picture?",
                       "type": "text"
                   }
               ],
               "role": "user"
           }
       ]
   }'
   ```
   
   
   
   </Tab>
   </Tabs>
   

* response

   
   <Tabs>
   <Tab zoneid="emRWWkdPIM" title="curl">
   <TabTitle>curl</TabTitle>
   
   ```Bash
   {
     "choices": [
       {
         "finish_reason": "stop",
         "index": 0,
         "logprobs": null,
         "message": {
           "content": "The picture presents a peaceful outdoor scene. A person in an orange kayak, holding a paddle, is paddling on the calm water. The water is like a mirror, reflecting the surrounding scenery. In the distance is a dense forest, and behind the forest stands a towering snow-capped mountain. The sky is light blue, with some clouds floating. The overall atmosphere is quiet and beautiful, showing the purity and grandeur of nature. ",
           "role": "assistant"
         }
       }
     ],
     "created": 1742636149,
     "id": "0217426361458116592a076493be583bc5e33f80ac2dcf1efc31b",
     "model": "seed-1-5-vision-pro-32k-250115",
     "service_tier": "default",
     "object": "chat.completion",
     "usage": {
       "completion_tokens": 85,
       "prompt_tokens": 521,
       "total_tokens": 606,
       "prompt_tokens_details": {
         "cached_tokens": 0
       },
       "completion_tokens_details": {
         "reasoning_tokens": 0
       }
     }
   }
   ```
   
   
   
   </Tab>
   </Tabs>
   


<span id="b8ac5a6d"></span>
## Deep reasoning


* request

   
   <Tabs>
   <Tab zoneid="wNxitlgxog" title="curl">
   <TabTitle>curl</TabTitle>
   
   ```Bash
   curl https://operator.las.ap-southeast-1.bytepluses.com//api/v1/chat/completions \
     -H "Content-Type: application/json" \
     -H "Authorization: Bearer $ARK_API_KEY" \
     -d $'{
       "messages": [
   
           {
               "content": "I want to study the difference between inferential and non-inferential models, how to reflect my professionalism",
               "role": "user"
           }
       ],
       "model": "seed-seed-1-6-251015"
   }'
   ```
   
   
   
   </Tab>
   </Tabs>
   

* response

   
   <Tabs>
   <Tab zoneid="PsJjOSzMUV" title="curl">
   <TabTitle>curl</TabTitle>
   
   ```Bash
   {
     "choices": [
       {
         "finish_reason": "stop",
         "index": 0,
         "logprobs": null,
         "message": {
           "content": "The main difference between a reasoning model and a non-reasoning model lies in the way it handles tasks, the focus of its capabilities, and the application scenarios. The following is the core difference analysis of the two:\ n\ n---\ n\ n ###** 1. Core definition **\ n- *** The reasoning model **\ n has the ** ability of logical reasoning, causal inference or complex decision-making. In practical applications, the two types of models are often used together (such as using a non-reasoning model to extract features and then handing them over to the reasoning model for decision-making) to balance efficiency and accuracy.",
           "reasoning_content": "Well, what the user is asking is what is the difference between an inference model and a non-inference model. I need to understand the specific meaning of these two terms first. Maybe the user has some understanding of machine learning or deep learning, but needs a clearer distinction. First, I should clarify the definition of these two concepts, and then compare them from different angles.\ n\ nFirst, inference models may refer to those models that need to perform logical reasoning and handle complex tasks, ***, while non-inference models focus on pattern recognition and direct mapping to help users form a clear conceptual framework.\ n",
           "role": "assistant"
         }
       }
     ],
     "created": 1742636537,
     "id": "0217426364949596592a076493be583bc5e33f80ac2dcf1eeaf9b",
     "model": "seed-1-6-251015",
     "service_tier": "default",
     "object": "chat.completion",
     "usage": {
       "completion_tokens": 1207,
       "prompt_tokens": 11,
       "total_tokens": 1218,
       "prompt_tokens_details": {
         "cached_tokens": 0
       },
       "completion_tokens_details": {
         "reasoning_tokens": 419
       }
     }
   }
   ```
   
   
   
   </Tab>
   </Tabs>
