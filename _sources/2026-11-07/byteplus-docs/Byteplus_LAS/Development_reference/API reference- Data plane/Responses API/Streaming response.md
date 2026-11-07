---
title: "Streaming response"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Streaming_response"
---

When you create a response and set stream to true, the server pushes events to the client in real time via Server\-Sent Events (SSE) during the generation of the Response. This section describes the various types of events that the server will push.

```mixin-react
const properties = ({
  "columns": [
    {
"title": "Parameter name",
      "dataIndex": "column_0",
      "key": "column_0",
      "width": 240
    },
    {
"title": "Data type",
      "dataIndex": "column_1",
      "key": "column_1",
      "width": 120
    },
    {
"title": "Parameter description",
      "dataIndex": "column_4",
      "key": "column_4",
      "width": 580
    }
  ],
  "data": [
    {
      "key": 1,
      "column_0": "response.created",
      "column_1": "object",
"column_4": "Event triggered when the response is created.",
      "children": [
{ "key": 11, "column_0": "response", "column_1": "object", "column_4": < div> Response in the created state. Contains parameters that are consistent with those returned by non-streaming calls when requesting to create a model.</ div> },
{ "key": 12, "column_0": "sequence_number", "column_1": "integer", "column_4": "The sequence number of the event." },
{ "key": 13, "column_0": "type", "column_1": "string", "column_4": "The type of the event, always response.created." }
      ]
    },
    {
      "key": 2,
      "column_0": "response.in_progress",
      "column_1": "object",
"column_4": "Event triggered when the response is in progress.",
      "children": [
{ "key": 21, "column_0": "response", "column_1": "object", "column_4": < div> Response in the in-progress state. Contains parameters that are consistent with those returned by non-streaming calls when creating a model.</ div> },
{ "key": 22, "column_0": "sequence_number", "column_1": "integer", "column_4": "The sequence number of the event." },
{ "key": 23, "column_0": "type", "column_1": "string", "column_4": "The type of the event, always response.in_progress." }
      ]
    },
    {
      "key": 3,
      "column_0": "response.completed",
      "column_1": "object",
"column_4": "Event triggered when the response is completed.",
      "children": [
{ "key": 31, "column_0": "response", "column_1": "object", "column_4": < div> Response in the completed state. Contains parameters that are consistent with those returned by non-streaming calls when creating a model.</ div> },
{ "key": 32, "column_0": "sequence_number", "column_1": "integer", "column_4": "The sequence number of the event." },
{ "key": 33, "column_0": "type", "column_1": "string", "column_4": "The type of the event, always response.completed." }
      ]
    },
    {
      "key": 4,
      "column_0": "response.failed",
      "column_1": "object",
"column_4": "Event triggered when the response fails.",
      "children": [
{ "key": 41, "column_0": "response", "column_1": "object", "column_4": < div> Response in the failed state. Contains parameters that are consistent with those returned by non-streaming calls when creating a model.</ div> },
{ "key": 42, "column_0": "sequence_number", "column_1": "integer", "column_4": "The sequence number of the event." },
{ "key": 43, "column_0": "type", "column_1": "string", "column_4": "The type of the event, always response.failed." }
      ]
    },
    {
      "key": 5,
      "column_0": "response.incomplete",
      "column_1": "object",
"column_4": "Event triggered when the response ends in an incomplete state.",
      "children": [
{ "key": 51, "column_0": "response", "column_1": "object", "column_4": < div> Response in the incomplete state. Contains parameters that are consistent with those returned by non-streaming calls when creating a model.</ div> },
{ "key": 52, "column_0": "sequence_number", "column_1": "integer", "column_4": "The sequence number of the event." },
{ "key": 53, "column_0": "type", "column_1": "string", "column_4": "The type of the event, always response.incomplete." }
      ]
    },
    {
      "key": 6,
      "column_0": "response.output_item.added",
      "column_1": "object",
"column_4": "Indicates that a new output item has been added.",
      "children": [
        {
          "key": 61,
          "column_0": "item",
          "column_1": "object",
"column_4": "Model output content.",
          "children": [
            {
              "key": 611,
              "column_0": "content",
              "column_1": "array",
"column_4": "The content of the output message (text output).",
              "children": [
{ "key": 6111, "column_0": "text", "column_1": "string", "column_4": "Text output from the model." },
{ "key": 6112, "column_0": "type", "column_1": "string", "column_4": "The type of the output text, always output_text." }
              ]
            },
            {
              "key": 612,
              "column_0": "summary",
              "column_1": "array",
"column_4": "Reasoning text content (content chain).",
              "children": [
{ "key": 6121, "column_0": "text", "column_1": "string", "column_4": "Reasoning content generated by the model when producing a reply." },
{ "key": 6122, "column_0": "type", "column_1": "string", "column_4": "The type of the object, always summary_text." }
              ]
            },
{ "key": 613, "column_0": "arguments", "column_1": "string", "column_4": "The JSON string of parameters to be passed to the function (tool information)." },
{ "key": 614, "column_0": "call_id", "column_1": "string", "column_4": "The unique ID of the function tool call generated by the model." },
{ "key": 615, "column_0": "name", "column_1": "string", "column_4": "The name of the function to be executed." },
{ "key": 616, "column_0": "role", "column_1": "string", "column_4": "The role of the output information, always assistant." },
{ "key": 617, "column_0": "status", "column_1": "string", "column_4": "The status of the output message." },
{ "key": 618, "column_0": "id", "column_1": "string", "column_4": "The unique identifier of the request/message." },
{ "key": 619, "column_0": "type", "column_1": "string", "column_4": "The type of the output message (such as output_text, reasoning, function_call)." }
          ]
        },
{ "key": 62, "column_0": "output_index", "column_1": "integer", "column_4": "The index of the output item that was added." },
{ "key": 63, "column_0": "sequence_number", "column_1": "integer", "column_4": "The sequence number of the event." },
{ "key": 64, "column_0": "type", "column_1": "string", "column_4": "The type of the event, always response.output_item.added." }
      ]
    },
    {
      "key": 7,
      "column_0": "response.output_item.done",
      "column_1": "object",
"column_4": "Indicates the output item is completed (structure is the same as response.output_item.added).",
      "children": [
        {
          "key": 71,
          "column_0": "item",
          "column_1": "object",
"column_4": "The completed output item.",
          "children": [
            {
              "key": 711,
              "column_0": "content",
              "column_1": "array",
"column_4": "The content of the output message (text output).",
              "children": [
{ "key": 7111, "column_0": "text", "column_1": "string", "column_4": "The text output from the model." },
{ "key": 7112, "column_0": "type", "column_1": "string", "column_4": "The type of the output text, always output_text." }
              ]
            },
            {
              "key": 712,
              "column_0": "summary",
              "column_1": "array",
"column_4": "Reasoning text content (content chain).",
              "children": [
{ "key": 7121, "column_0": "text", "column_1": "string", "column_4": "Reasoning content generated by the model when replying." },
{ "key": 7122, "column_0": "type", "column_1": "string", "column_4": "The type of the object, always summary_text." }
              ]
            },
{ "key": 713, "column_0": "arguments", "column_1": "string", "column_4": "The JSON string of parameters to be passed to the function." },
{ "key": 714, "column_0": "call_id", "column_1": "string", "column_4": "The unique ID of the function tool call generated by the model." },
{ "key": 715, "column_0": "name", "column_1": "string", "column_4": "The name of the function to be executed." },
{ "key": 716, "column_0": "role", "column_1": "string", "column_4": "The role of the output information, always assistant." },
{ "key": 717, "column_0": "status", "column_1": "string", "column_4": "The status of the output message." },
{ "key": 718, "column_0": "id", "column_1": "string", "column_4": "The unique identifier of the request/message." },
{ "key": 719, "column_0": "type", "column_1": "string", "column_4": "The type of the output message." }
          ]
        },
{ "key": 72, "column_0": "output_index", "column_1": "integer", "column_4": "The index of the completed output item." },
{ "key": 73, "column_0": "sequence_number", "column_1": "integer", "column_4": "The sequence number of the event." },
{ "key": 74, "column_0": "type", "column_1": "string", "column_4": "The type of the event, always response.output_item.done." }
      ]
    },
    {
      "key": 8,
      "column_0": "response.content_part.added",
      "column_1": "object",
"column_4": "Triggered when a new content part is added.",
      "children": [
{ "key": 81, "column_0": "content_index", "column_1": "integer", "column_4": "The index of the content part." },
{ "key": 82, "column_0": "item_id", "column_1": "string", "column_4": "The ID of the output item added by the content part." },
{ "key": 83, "column_0": "output_index", "column_1": "integer", "column_4": "The index of the output item added by the content part." },
        {
          "key": 84,
          "column_0": "part",
          "column_1": "object",
"column_4": "The content part that was added.",
          "children": [
{ "key": 841, "column_0": "text", "column_1": "string", "column_4": "The text content output by the model." },
{ "key": 842, "column_0": "type", "column_1": "string", "column_4": "The type of output text, which should be output_text here." }
          ]
        },
{ "key": 85, "column_0": "sequence_number", "column_1": "integer", "column_4": "The sequence number of the event." },
{ "key": 86, "column_0": "type", "column_1": "string", "column_4": "The type of the event, always response.content_part.added." }
      ]
    },
    {
      "key": 9,
      "column_0": "response.content_part.done",
      "column_1": "object",
"column_4": "Triggered when the content is completed.",
      "children": [
{ "key": 91, "column_0": "content_index", "column_1": "integer", "column_4": "The index of the content part." },
{ "key": 92, "column_0": "item_id", "column_1": "string", "column_4": "The ID of the output item added by the content part." },
{ "key": 93, "column_0": "output_index", "column_1": "integer", "column_4": "The index of the output item added by the content part." },
        {
          "key": 94,
          "column_0": "part",
          "column_1": "object",
"column_4": "The content part that was completed.",
          "children": [
{ "key": 941, "column_0": "text", "column_1": "string", "column_4": "The text content output by the model." },
{ "key": 942, "column_0": "type", "column_1": "string", "column_4": "The type of output text, which should be output_text here." }
          ]
        },
{ "key": 95, "column_0": "sequence_number", "column_1": "integer", "column_4": "The sequence number of the event." },
{ "key": 96, "column_0": "type", "column_1": "string", "column_4": "The type of the event, always response.content_part.done." }
      ]
    },
    {
      "key": 10,
      "column_0": "response.output_text.delta",
      "column_1": "object",
"column_4": "Triggered when a new text fragment is added.",
      "children": [
{ "key": 101, "column_0": "content_index", "column_1": "integer", "column_4": "The index of the content block to which the incremental text belongs." },
{ "key": 102, "column_0": "delta", "column_1": "string", "column_4": "The content of the newly added text fragment." },
{ "key": 103, "column_0": "item_id", "column_1": "string", "column_4": "The unique ID of the output item to which the incremental text belongs." },
{ "key": 104, "column_0": "output_index", "column_1": "integer", "column_4": "The list index of the output item to which the incremental text belongs." },
{ "key": 105, "column_0": "sequence_number", "column_1": "integer", "column_4": "The sequence number of the event." },
{ "key": 106, "column_0": "type", "column_1": "string", "column_4": "The type of the event, always response.output_text.delta." }
      ]
    },
    {
      "key": 11,
      "column_0": "response.output_text.done",
      "column_1": "object",
"column_4": "Triggered when the text content is completed.",
      "children": [
{ "key": 111, "column_0": "content_index", "column_1": "integer", "column_4": "The index of the content block to which the text content belongs." },
{ "key": 112, "column_0": "item_id", "column_1": "string", "column_4": "The unique ID of the output item to which the text content belongs." },
{ "key": 113, "column_0": "output_index", "column_1": "integer", "column_4": "The list index of the output item to which the text content belongs." },
{ "key": 114, "column_0": "text", "column_1": "string", "column_4": "The completed text content." },
{ "key": 115, "column_0": "sequence_number", "column_1": "integer", "column_4": "The sequence number of the event." },
{ "key": 116, "column_0": "type", "column_1": "string", "column_4": "The type of the event, always response.output_text.done." }
      ]
    },
    {
      "key": 12,
      "column_0": "response.function_call_arguments.delta",
      "column_1": "object",
"column_4": "Triggered when there are function call argument fragments.",
      "children": [
{ "key": 121, "column_0": "delta", "column_1": "string", "column_4": "The incremental fragment of function call arguments added in this instance." },
{ "key": 122, "column_0": "item_id", "column_1": "string", "column_4": "The unique ID of the associated output item." },
{ "key": 123, "column_0": "output_index", "column_1": "integer", "column_4": "The list index of the associated output item." },
{ "key": 124, "column_0": "sequence_number", "column_1": "integer", "column_4": "The sequence number of the event." },
{ "key": 125, "column_0": "type", "column_1": "string", "column_4": "The event type, always response.function_call_arguments.delta." }
      ]
    },
    {
      "key": 13,
      "column_0": "response.function_call_arguments.done",
      "column_1": "object",
"column_4": "Triggered when function call arguments are completed.",
      "children": [
{ "key": 131, "column_0": "arguments", "column_1": "string", "column_4": "The arguments for the function call." },
{ "key": 132, "column_0": "item_id", "column_1": "string", "column_4": "The unique ID of the associated output item." },
{ "key": 133, "column_0": "output_index", "column_1": "integer", "column_4": "The list index of the associated output item." },
{ "key": 134, "column_0": "sequence_number", "column_1": "integer", "column_4": "The sequence number of the event." },
{ "key": 135, "column_0": "type", "column_1": "string", "column_4": "The event type, always response.function_call_arguments.done." }
      ]
    },
    {
      "key": 14,
      "column_0": "response.reasoning_summary_part.added",
      "column_1": "object",
"column_4": "Triggered when there is an added part in the reasoning chain.",
      "children": [
{ "key": 141, "column_0": "item_id", "column_1": "string", "column_4": "The ID of the associated output item." },
{ "key": 142, "column_0": "output_index", "column_1": "integer", "column_4": "The index of the associated output item." },
{ "key": 143, "column_0": "summary_index", "column_1": "integer", "column_4": "The sub-index of the reasoning summary part within the output item (if there are multiple summaries)." },
        {
          "key": 144,
          "column_0": "part",
          "column_1": "object",
"column_4": "The content part that was added.",
          "children": [
{ "key": 1441, "column_0": "text", "column_1": "string", "column_4": "The reasoning chain text output." },
{ "key": 1442, "column_0": "type", "column_1": "string", "column_4": "The type of part, always summary_text." }
          ]
        },
{ "key": 145, "column_0": "sequence_number", "column_1": "integer", "column_4": "The sequence number of the event." },
{ "key": 146, "column_0": "type", "column_1": "string", "column_4": "The event type, always response.reasoning_summary_part.added." }
      ]
    },
    {
      "key": 15,
      "column_0": "response.reasoning_summary_part.done",
      "column_1": "object",
"column_4": "Triggered when a reasoning chain part is completed.",
      "children": [
{ "key": 151, "column_0": "item_id", "column_1": "string", "column_4": "The ID of the associated output item." },
{ "key": 152, "column_0": "output_index", "column_1": "integer", "column_4": "The index of the associated output item." },
{ "key": 153, "column_0": "summary_index", "column_1": "integer", "column_4": "The sub-index of the reasoning summary part within the output item (if there are multiple summaries)." },
        {
          "key": 154,
          "column_0": "part",
          "column_1": "object",
"column_4": "The content part that was completed.",
          "children": [
{ "key": 1541, "column_0": "text", "column_1": "string", "column_4": "The reasoning chain text output." },
{ "key": 1542, "column_0": "type", "column_1": "string", "column_4": "The type of part, always summary_text." }
          ]
        },
{ "key": 155, "column_0": "sequence_number", "column_1": "integer", "column_4": "The sequence number of the event." },
{ "key": 156, "column_0": "type", "column_1": "string", "column_4": "The event type, always response.reasoning_summary_part.done." }
      ]
    },
    {
      "key": 16,
      "column_0": "response.reasoning_summary_text.delta",
      "column_1": "object",
"column_4": "Triggered when there is newly added reasoning chain text.",
      "children": [
{ "key": 161, "column_0": "delta", "column_1": "string", "column_4": "The incremental fragment of reasoning chain text output." },
{ "key": 162, "column_0": "item_id", "column_1": "string", "column_4": "The ID of the associated output item." },
{ "key": 163, "column_0": "output_index", "column_1": "integer", "column_4": "The index of the associated output item." },
{ "key": 164, "column_0": "summary_index", "column_1": "integer", "column_4": "The sub-index of the reasoning summary part within the output item (if there are multiple summaries)." },
{ "key": 165, "column_0": "sequence_number", "column_1": "integer", "column_4": "The sequence number of the event." },
{ "key": 166, "column_0": "type", "column_1": "string", "column_4": "The event type, always response.reasoning_summary_text.delta." }
      ]
    },
    {
      "key": 17,
      "column_0": "response.reasoning_summary_text.done",
      "column_1": "object",
"column_4": "Triggered when reasoning chain text is completed.",
      "children": [
{ "key": 171, "column_0": "item_id", "column_1": "string", "column_4": "The ID of the associated output item." },
{ "key": 172, "column_0": "output_index", "column_1": "integer", "column_4": "The index of the associated output item." },
{ "key": 173, "column_0": "summary_index", "column_1": "integer", "column_4": "The sub-index of the reasoning summary part within the output item (if there are multiple summaries)." },
{ "key": 174, "column_0": "text", "column_1": "string", "column_4": "The complete reasoning chain text." },
{ "key": 175, "column_0": "sequence_number", "column_1": "integer", "column_4": "The sequence number of the event." },
{ "key": 176, "column_0": "type", "column_1": "string", "column_4": "The event type, always response.reasoning_summary_text.done." }
      ]
    },
    {
      "key": 18,
      "column_0": "error",
      "column_1": "object",
"column_4": "Triggered when an error occurs.",
      "children": [
{ "key": 181, "column_0": "code", "column_1": "string/null", "column_4": "The error code." },
{ "key": 182, "column_0": "message", "column_1": "string", "column_4": "The cause of the error." },
{ "key": 183, "column_0": "param", "column_1": "string/null", "column_4": "The error parameter." },
{ "key": 184, "column_0": "sequence_number", "column_1": "integer", "column_4": "The sequence number of the event." },
{ "key": 185, "column_0": "type", "column_1": "string", "column_4": "The event type, always error." }
      ]
    }
  ]
}); 
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```
