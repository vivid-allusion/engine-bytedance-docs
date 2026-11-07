---
title: "Retrieve response context"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Get_response_context"
---

Retrieve all context information associated with a specific model response.

# Request description

* **Base URL**: In Asia Pacific (Johor), the Base URL is `https://operator.las.ap-southeast-1.bytepluses.com`. When using the API, use the Base URL for the region where your LAS service is deployed. For details, see [Usage methods](https://docs.byteplus.com/docs/Byteplus_LAS/Usage_methods).

* **Path**：api/v1/responses/{response_id}/input_items?after={after}&before={before}&limit={limit}&order={order}&include[]=

* **Method**: GET

* **Content\-type**: application/json

# Request parameters

## Path parameters

|Parameter name |Data type |Required |Parameter description |
|---|---|---|---|
|response_id |string |Required |The response ID to be retrieved. |

## Query parameters

```mixin-react
const properties = ({
  "columns": [
    {
"title": "Parameter name",
      "dataIndex": "column_0",
      "key": "column_0",
      "width": 150
    },
    {
"title": "Data type",
      "dataIndex": "column_1",
      "key": "column_1",
      "width": 100
    },
    {
"title": "Required",
      "dataIndex": "column_2",
      "key": "column_2",
      "width": 100
    },
    {
"title": "Default value",
      "dataIndex": "column_3",
      "key": "column_3",
      "width": 100
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
      "column_0": "after",
      "column_1": "string/ null",
"column_2": "No",
      "column_3": "-",
"column_4": "Returns input items after this ID."
    },
    {
      "key": 2,
      "column_0": "before",
      "column_1": "string/ null",
"column_2": "No",
      "column_3": "-",
"column_4": "Returns input items before this ID."
    },
    {
      "key": 3,
      "column_0": "include[]",
      "column_1": "array/ null",
"column_2": "No",
      "column_3": "-",
"column_4": "Specifies additional fields to include in the response. Some endpoints return only basic fields by default; using include allows the server to return more information.",
      "children": [
        {
          "key": 31,
          "column_0": "message.input_image.image_url",
          "column_1": "-",
"column_2": "No",
          "column_3": "-",
"column_4": < div> Includes the image URL in the input message. < ul>< li> If the image is a URL, returns the URL. </ li>< li> If the image is base64 encoded, returns the base64 encoded information. </li></ul></div>
        }
      ]
    },
    {
      "key": 4,
      "column_0": "limit",
      "column_1": "integer",
"column_2": "No",
      "column_3": "20",
"column_4": "Controls the maximum number of items returned per request.<br>Value range: 1 ~ 100."
    },
    {
      "key": 5,
      "column_0": "order",
      "column_1": "string",
"column_2": "No",
      "column_3": "desc",
"column_4": < div> Controls the sorting method for input items. < ul>< li> asc: Sort in ascending order. </ li>< li> desc: Sort in descending order. </li></ul></div>
    }
  ]
});
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```

# Response parameters

```mixin-react
const properties = ({
  "columns": [
    {
"title": "Parameter name",
      "dataIndex": "column_0",
      "key": "column_0",
      "width": 140
    },
    {
"title": "Data type",
      "dataIndex": "column_1",
      "key": "column_1",
      "width": 120
    },
    {
"title": "Default value",
      "dataIndex": "column_3",
      "key": "column_3",
      "width": 100
    },
    {
"title": "Parameter description",
      "dataIndex": "column_4",
      "key": "column_4",
      "width": 480
    }
  ],
  "data": [
    {
      "key": 1,
      "column_0": "object",
      "column_1": "string",
      "column_3": "-",
"column_4": "The value is always \"list\"."
    },
    {
      "key": 2,
      "column_0": "data",
      "column_1": "object[] / null",
      "column_3": "-",
"column_4": < div> List of context elements, identical in structure to the < b> input (list of input elements)</ b> field in the create model request. < br/> If the request references previous_response_id, the server also returns the context contained in previous_response. </div>
    },
    {
      "key": 3,
      "column_0": "first_id",
      "column_1": "string",
      "column_3": "-",
"column_4": "ID of the first item in the list."
    },
    {
      "key": 4,
      "column_0": "has_more",
      "column_1": "boolean",
      "column_3": "-",
"column_4": < div> Indicates whether there is more data that has not been returned. < ul>< li> true: There is data that has not been returned. </ li>< li> false: All data has been returned. </li></ul></div>
    },
    {
      "key": 5,
      "column_0": "last_id",
      "column_1": "string",
      "column_3": "-",
"column_4": "ID of the last item in the list."
    }
  ]
});
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```

# Example

* request

   ```Bash
   curl --location 'https://operator.las.ap-southeast-1.bytepluses.com/api/v1/responses/resp_0217******/input_items' \
   --header "Authorization: Bearer $LAS_API_KEY" \
   --header 'Content-Type: application/json'
   ```

* response

   ```JSON
   {
       "object": "list",
       "data": [
           {
               "type": "message",
               "role": "assistant",
               "content": [
                   {
                       "type": "output_text",
                       "text": "# Ember and Amber Eyes\n\n## Verse\nWind moves through the meadow, scattering threads of gold.\nA red-haired girl leans close while an amber-eyed fox keeps watch.\n\n## Chorus\nWe are reflections found in the wild,\nTwo quiet hearts learning to trust.\nUnder the fading light, loneliness gives way\nTo a home made of warmth and companionship."
                   }
               ],
               "status": "completed",
               "id": "msg_0217****"
           },
           {
               "type": "message",
               "role": "user",
               "content": [
                   {
                       "type": "input_text",
                       "text": "Write another song inspired by the image."
                   }
               ],
               "id": "msg_0217****"
           },
           {
               "type": "message",
               "role": "assistant",
               "content": [
                   {
                       "type": "output_text",
                       "text": "The image shows a red-haired girl resting her cheek against a red fox in a quiet meadow. The girl's auburn hair echoes the fox's warm coat, while the fox's white chest, dark ears, and amber eyes stand out in the soft light. Their relaxed posture conveys trust and companionship, creating a calm and comforting scene."
                   }
               ],
               "status": "completed",
               "id": "msg_0217****"
           },
           {
               "type": "message",
               "role": "user",
               "content": [
                   {
                       "type": "input_text",
                       "text": "What do you see in the image?"
                   },
                   {
                       "type": "input_image"
                   }
               ],
               "id": "msg_0217****"
           }
       ],
       "first_id": "msg_****d2d1",
       "last_id": "msg_****6c67",
       "has_more": false
   }
   ```
