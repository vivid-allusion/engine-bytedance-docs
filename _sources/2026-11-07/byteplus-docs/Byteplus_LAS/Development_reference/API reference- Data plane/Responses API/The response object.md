---
title: "The response object"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/The_response_object"
---

After creating a model request or retrieving a model response, the model returns a response object. This document describes the detailed parameters included in the response object.

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
      "dataIndex": "column_4",
      "key": "column_4"
    }
  ],
  "data": [
    {
      "key": 1,
      "column_0": "created_at",
      "column_1": "integer",
"column_4": "The Unix timestamp (in seconds) when this request was created."
    },
    {
      "key": 2,
      "column_0": "error",
      "column_1": "object / null",
"column_4": < div> The error object returned when the model fails to generate a response. < ul>< li> code: The corresponding error code. </ li>< li> message: Error description. </li></ul></div>
    },
    {
      "key": 3,
      "column_0": "id",
      "column_1": "string",
"column_4": "The unique identifier for this request."
    },
    {
      "key": 4,
      "column_0": "incomplete_details",
      "column_1": "object / null",
"column_4": < div> Details about why the response was not completed. < br/> reason: The reason why the response was not completed. </div>
    },
    {
      "key": 5,
      "column_0": "instructions",
      "column_1": "string / null",
"column_4": "Insert a system (or developer) message as the first item in the model context.<br/>When used together with previous_response_id, the instructions from the previous response will not be carried over to the next response."
    },
    {
      "key": 6,
      "column_0": "max_output_tokens",
      "column_1": "integer / null",
"column_4": "The maximum number of tokens for model output, including both the model's answer and chain-of-thought content."
    },
    {
      "key": 7,
      "column_0": "model",
      "column_1": "string",
"column_4": "The actual model name and version used for this request."
    },
    {
      "key": 8,
      "column_0": "object",
      "column_1": "string",
"column_4": "Always set to response."
    },
    {
      "key": 9,
      "column_0": "output",
      "column_1": "array",
"column_4": "The list of output messages from the model, including the answers generated for this request, chain-of-thought content, and tool calls.",
      "children": [
        {
          "key": 901,
          "column_0": "content",
          "column_1": "array",
"column_4": "The content of the output message (model answer).",
          "children": [
{ "key": 9011, "column_0": "text", "column_1": "string", "column_4": "The text content of the model's answer." },
{ "key": 9012, "column_0": "type", "column_1": "string", "column_4": "The type of the model's answer, always output_text." },
{ "key": 9013, "column_0": "role", "column_1": "string", "column_4": "The role of the output message, always assistant." },
{ "key": 9014, "column_0": "status", "column_1": "string", "column_4": "The status of the output message." },
{ "key": 9015, "column_0": "id", "column_1": "string", "column_4": "The unique identifier for this answer." },
{ "key": 9016, "column_0": "type", "column_1": "string", "column_4": "The type of the output message, which should be message." },
{ "key": 9017, "column_0": "partial", "column_1": "boolean", "column_4": "This field is returned when the model is in continuation mode, and should be true." }
          ]
        },
        {
          "key": 902,
          "column_0": "summary",
          "column_1": "array",
"column_4": "Chain-of-thought content.",
          "children": [
{ "key": 9021, "column_0": "text", "column_1": "string", "column_4": "The text part of the chain-of-thought content." },
{ "key": 9022, "column_0": "type", "column_1": "string", "column_4": "The type of the object, which should be summary_text." }
          ]
        },
        {
          "key": 903,
          "column_0": "type",
          "column_1": "string",
"column_4": "The type of this output object (such as reasoning, function_call, mcp_call, web_search_call, image_process)."
        },
        {
          "key": 904,
          "column_0": "status",
          "column_1": "string",
"column_4": "The status of the returned message."
        },
        {
          "key": 905,
          "column_0": "id",
          "column_1": "string",
"column_4": "The unique identifier for this output."
        },
        {
          "key": 906,
          "column_0": "arguments",
          "column_1": "string",
"column_4": "Parameters to be passed to the function, formatted as a JSON string (Function Call)."
        },
        {
          "key": 907,
          "column_0": "call_id",
          "column_1": "string",
"column_4": "The unique ID for this tool call information."
        },
        {
          "key": 908,
          "column_0": "name",
          "column_1": "string",
"column_4": "The name of the function to run."
        },
        {
          "key": 909,
          "column_0": "server_label",
          "column_1": "string",
"column_4": "MCP Server label."
        },
        {
          "key": 910,
          "column_0": "tools",
          "column_1": "object",
"column_4": "Return information from MCP/network search/image processing tools.",
          "children": [
{ "key": 9101, "column_0": "id", "column_1": "string", "column_4": "The unique identifier for this output." },
{ "key": 9102, "column_0": "type", "column_1": "string", "column_4": "Tool type (such as mcp_call, web_search_call, image_process)." },
{ "key": 9103, "column_0": "server_label", "column_1": "string", "column_4": "MCP Server label." },
{ "key": 9104, "column_0": "arguments", "column_1": "string", "column_4": "JSON string of parameters passed to the tool." },
{ "key": 9105, "column_0": "name", "column_1": "string", "column_4": "The name of the tool to run." },
{ "key": 9106, "column_0": "error", "column_1": "string", "column_4": "Errors encountered during the tool call (if any)." },
{ "key": 9107, "column_0": "output", "column_1": "string", "column_4": "The output result of the tool call." },
{ "key": 9108, "column_0": "action", "column_1": "object", "column_4": "The object representing the specific operation performed in this search call.", "children": [
{ "key": 91081, "column_0": "type", "column_1": "string", "column_4": "Generally search." },
{ "key": 91082, "column_0": "query", "column_1": "string", "column_4": "Search content." },
{ "key": 91083, "column_0": "source", "column_1": "string[]", "column_4": < div> Additional content sources for online search.< ul>< li> toutiao: Additional Toutiao graphic and text content source for online search.</ li>< li> douyin: Additional Douyin Encyclopedia content source for online search.</ li>< li> moji: Additional Moji Weather content source for online search.</ li></ ul></ div> }
            ]},
{ "key": 9109, "column_0": "point", "column_1": "object", "column_4": < div> Feature toggle for drawing points/connecting lines.< ul>< li> type:'enabled': This feature is enabled.</ li>< li> type:'disabled': This feature is disabled.</ li></ ul></ div> },
{ "key": 9110, "column_0": "grounding", "column_1": "object", "column_4": < div> Feature toggle for box selection/cropping.< ul>< li> type:'enabled': This feature is enabled.</ li>< li> type:'disabled': This feature is disabled.</ li></ ul></ div> },
{ "key": 9111, "column_0": "zoom", "column_1": "object", "column_4": < div> Feature toggle for zoom (supports 0.5–2.0x).< ul>< li> type:'enabled': This feature is enabled.</ li>< li> type:'disabled': This feature is disabled.</ li></ ul></ div> },
{ "key": 9112, "column_0": "rotate", "column_1": "object", "column_4": < div> Feature toggle for rotation (supports 0–359 degrees).< ul>< li> type:'enabled': This feature is enabled.</ li>< li> type:'disabled': This feature is disabled.</ li></ ul></ div> },
{ "key": 9113, "column_0": "tools", "column_1": "array", "column_4": "Server-side available tools (MCP List).", "children": [
{ "key": 91131, "column_0": "input_schema", "column_1": "object", "column_4": "JSON schema describing the tool input." },
{ "key": 91132, "column_0": "name", "column_1": "string", "column_4": "Name of the tool to run." },
{ "key": 91133, "column_0": "annotations", "column_1": "object", "column_4": "Additional notes about the tool." },
{ "key": 91134, "column_0": "description", "column_1": "string", "column_4": "Tool description." }
            ]}
          ]
        }
      ]
    },
    {
      "key": 10,
      "column_0": "previous_response_id",
      "column_1": "string / null",
"column_4": "The historical response ID passed in for this request."
    },
    {
      "key": 11,
      "column_0": "thinking",
      "column_1": "object / null",
"column_4": "Whether to enable deep thinking mode.",
      "children": [
        {
          "key": 111,
          "column_0": "type",
          "column_1": "string",
"column_4": < div> Value range: enabled, disabled, auto. < ul>< li> enabled: Enables thinking mode. The model will always think before answering. </ li>< li> disabled: Disables thinking mode. The model will answer directly without thinking. </ li>< li> auto: Automatic thinking mode. The model will decide whether to think based on the question. For simple questions, it will answer directly. </li></ul></div>
        }
      ]
    },
    {
      "key": 12,
      "column_0": "service_tier",
      "column_1": "string",
"column_4": < div> Whether the TPM protection package was used for this request. < ul>< li> default: The TPM protection package quota was not used for this request. </li></ul></div>
    },
    {
      "key": 13,
      "column_0": "status",
      "column_1": "string",
"column_4": < div> Status of the generated response. < ul>< li> completed: The response is complete. </ li>< li> failed: The response failed. </ li>< li> in_progress: The response is in progress. </ li>< li> incomplete: The response is incomplete. </li></ul></div>
    },
    {
      "key": 14,
      "column_0": "text",
      "column_1": "object",
"column_4": < div> Used to define the output format. For details, see< a href="https://www.volcengine.com/docs/82379/1568221" target="_blank"> Structured Output</ a>. </div>,
      "children": [
        {
          "key": 141,
          "column_0": "format",
          "column_1": "object",
"column_4": "Object specifying the format the model must output.",
          "children": [
{ "key": 1411, "column_0": "type", "column_1": "string", "column_4": "Type of reply format (text, json_object, json_schema)." },
{ "key": 1412, "column_0": "name", "column_1": "string", "column_4": "Name of the user-defined JSON structure." },
{ "key": 1413, "column_0": "schema", "column_1": "object", "column_4": "JSON format definition of the reply format, described as a JSON Schema object." },
{ "key": 1414, "column_0": "description", "column_1": "string / null", "column_4": "Description of the reply purpose. The model will decide how to reply in this format based on this description." },
{ "key": 1415, "column_0": "strict", "column_1": "boolean / null", "column_4": < div> Whether to enable strict compliance mode when generating output.< ul>< li> true: The model will always follow the format defined in the schema field.</ li>< li> false: The model will follow the structure defined in the schema field as much as possible.</ li></ ul></ div> }
          ]
        }
      ]
    },
    {
      "key": 15,
      "column_0": "tools",
      "column_1": "array",
"column_4": "List of tools that the model can call.",
      "children": [
        {
          "key": 151,
          "column_0": "function",
          "column_1": "object",
"column_4": "List of tools of type function that the model can call.",
          "children": [
{ "key": 1511, "column_0": "name", "column_1": "string", "column_4": "Name of the function to call." },
{ "key": 1512, "column_0": "parameters", "column_1": "object", "column_4": < div> Function request parameters, described in < a href="https://json-schema.org/understanding-json-schema" target="_blank"> JSON Schema</ a> format.</ div> },
{ "key": 1513, "column_0": "type", "column_1": "string", "column_4": "Type of tool invocation, always set to \"function\"." },
{ "key": 1514, "column_0": "description", "column_1": "string", "column_4": "Description of the invoked function." }
          ]
        }
      ]
    },
    {
      "key": 16,
      "column_0": "top_p",
      "column_1": "float / null",
"column_4": "Nucleus sampling probability threshold."
    },
    {
      "key": 17,
      "column_0": "usage",
      "column_1": "object",
"column_4": "Token usage and tool usage details for this request.",
      "children": [
{ "key": 171, "column_0": "input_tokens", "column_1": "integer", "column_4": "Number of input tokens." },
        {
          "key": 172,
          "column_0": "input_tokens_details",
          "column_1": "object",
"column_4": "Detailed information about input tokens.",
          "children": [
{ "key": 1721, "column_0": "cached_tokens", "column_1": "integer", "column_4": "Number of cached tokens." }
          ]
        },
{ "key": 173, "column_0": "output_tokens", "column_1": "integer", "column_4": "Number of output tokens." },
        {
          "key": 174,
          "column_0": "output_tokens_details",
          "column_1": "object",
"column_4": "Detailed information about output tokens.",
          "children": [
{ "key": 1741, "column_0": "reasoning_tokens", "column_1": "integer", "column_4": "Number of tokens used for reasoning." }
          ]
        },
{ "key": 175, "column_0": "total_tokens", "column_1": "integer", "column_4": "Total number of tokens consumed." },
        {
          "key": 176,
          "column_0": "tool_usage",
          "column_1": "object",
"column_4": "Information about tool usage.",
          "children": [
{ "key": 1761, "column_0": "image_process", "column_1": "integer", "column_4": "Number of times the image processing tool was invoked." },
{ "key": 1762, "column_0": "mcp", "column_1": "integer", "column_4": "Number of times the mcp tool was invoked." },
{ "key": 1763, "column_0": "web_search", "column_1": "integer", "column_4": "Number of times the web search tool was invoked." }
          ]
        },
        {
          "key": 177,
          "column_0": "tool_usage_details",
          "column_1": "object",
"column_4": "Detailed information about tool usage (including sub-objects such as image_process, mcp, web_search, and others)."
        }
      ]
    },
    {
      "key": 18,
      "column_0": "store",
      "column_1": "boolean",
"column_4": < div> Whether to store the generated model response. < ul>< li> false: Do not store. The conversation content cannot be retrieved by subsequent API calls. </ li>< li> true: Store the current model response. The conversation content can be retrieved by subsequent API calls. </li></ul></div>
    },
    {
      "key": 19,
      "column_0": "caching",
      "column_1": "object",
"column_4": "Whether to enable caching.",
      "children": [
        {
          "key": 191,
          "column_0": "type",
          "column_1": "string",
"column_4": < div> Value range: enabled, disabled. < ul>< li> enabled: Enable caching. </ li>< li> disabled: Disable caching. </li></ul></div>
        }
      ]
    },
    {
      "key": 20,
      "column_0": "expire_at",
      "column_1": "integer/null",
"column_4": "Validity period of the stored data."
    },
    {
      "key": 21,
      "column_0": "temperature",
      "column_1": "float/null",
"column_4": "Sampling temperature."
    },
    {
      "key": 22,
      "column_0": "context_management",
      "column_1": "object",
"column_4": "Context management response.",
      "children": [
        {
          "key": 221,
          "column_0": "applied_edits",
          "column_1": "array",
"column_4": "List of applied context editing strategies.",
          "children": [
{ "key": 2211, "column_0": "type", "column_1": "string", "column_4": "Type of context editing strategy (clear_thinking, clear_tool_uses)." },
{ "key": 2212, "column_0": "cleared_thinking_turns", "column_1": "integer", "column_4": "Number of cleared reasoning turns." },
{ "key": 2213, "column_0": "cleared_tool_uses", "column_1": "integer", "column_4": "Number of cleared tool invocations." }
          ]
        }
      ]
    }
  ]
}); 
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```
