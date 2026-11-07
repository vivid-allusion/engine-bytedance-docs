---
title: "AI Search: Search Results Sorting"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/AI_Search_Sorting"
---

<span id="0a7f2d1f"></span>
# Search Results/List Sorting Overview

The Search API provides sorting functionality, allowing you to customize the order of search results based on any field in the dataset. The sorting function works with search filters to help users quickly find the most relevant content.

&nbsp;

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Important</div>


<div data-tips="true" data-tips-type="warning"><strong>Search List Sorting</strong> is a <strong>post\-search sorting</strong> mechanism, meaning it performs a global re\-sorting operation on the retrieved search results. </div>


<div data-tips="true" data-tips-type="warning"><strong> </strong><strong>T</strong><strong>his configuration </strong><strong>is different from </strong><strong><em>C</em></strong><strong><em>ustomized Sorting rules</em></strong><strong><em>.</em></strong> (Refer to <a href="https://docs.byteplus.com/docs/393/Configure_search_strategy#39776d7b">Configure customized Sorting rules</a>)</div>


<div data-tips="true" data-tips-type="warning">While both use item field attributes to arrange results in ascending or descending order, Search List Sorting <strong>completely disregards the relevance score</strong> between the item and the user's query. It rearranges the entire returned list based strictly on the specified field values.</div>


<span id="b088cda9"></span>
# Implementation Guide

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">For complete API usage instructions, see: <a href="https://www.volcengine.com/docs/85296/1544974">API Reference \> Search</a></div>


When calling the Search API, use the `sort_by` and `sort_order` parameters to specify sorting syntax. As shown in the example below:

```Bash
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/application/{application_id}/search/{configuration_id}' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer API key' \
  -d '{
    "query": {
        "text": "query text string",
        "image_url": "image file"
    },
    "page_number": search page number,
    "page_size": number of search results per page,
    "user": {
        "user_id": user ID
    },
    "filter": search filter conditions,
    "dataset_id": "target dataset id",
    "sort_by": pecified sort field,
    "sort_order": sort order e.g. "asc" or "desc"
}'
```


<span id="e6fc3efb"></span>
## Parameter description


|**Parameter** |**Required** |**Description** |
|---|---|---|
|`sort_by` |No |**Specify the field name used for sorting**<br><br><br>* **Supported field types**: Supports sorting of basic field types:`int32`,`int64`,`float`,`bool`,`string`<br><br>* **Requirements**:<br><br>   * Fields must exist in the dataset<br><br>   * **For nested objects**, use dot notation. (Example:`"product.price"`,`"user.rating"`) |
|`sort_order` |No  |**Specify the sorting direction**<br><br><br>* **Accepted values**:<br><br>   * `"desc"`: Descending order  **(Default)** <br><br>   * `"asc"`: Ascending order |


<span id="1a1412f0"></span>
## Sample API Request

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">For complete API usage instructions, see: <a href="https://www.volcengine.com/docs/85296/1544974">API Reference \> Search</a></div>


<span id="e27308a1"></span>
### Example 1: Sort by price in ascending order

```JSON
{
    "query": {
        "text": "Sneakers"
    },
    "dataset_id": "<your_dataset_id>",
    "page_number": 1,
    "page_size": 20,
    "sort_by": "price",
    "sort_order": "asc"
}
```


<span id="d71329d2"></span>
### Example 2: Sort by creation time in descending order

```JSON
{
    "query": {
        "text": "New Dresses"
    },
    "dataset_id": "<your_dataset_id>",
    "page_number": 1,
    "page_size": 20,
    "sort_by": "create_at",
    "sort_order": "desc"
}
```


<span id="fe5f7f0c"></span>
### Example 3: Sort by Nested Field

```JSON
{
    "query": {
        "text": "Mobile Phones"
    },
    "dataset_id": "<your_dataset_id>",
    "page_number": 1,
    "page_size": 20,
    "sort_by": "product.sales_volume",
    "sort_order": "desc"
}
```


<span id="faee63ff"></span>
## Example 4: Complete API Request 

```Bash
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/application/{application_id}/search/{configuration_id}' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <API Key>' \
  -d '{
    "query": {
        "text": "Women Shoes Spring/Summer"
    },
    "dataset_id": "<your_dataset_id>",
    "page_number": 1,
    "page_size": 20,
    "sort_by": "price",
    "sort_order": "asc",
    "filter": {
        "op": "must",
        "field": "status",
        "conds": [1]
    }
}'
```
