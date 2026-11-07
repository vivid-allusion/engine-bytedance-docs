---
title: "Batch Query Analysis"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Batch_Query_Analysis"
---

At present, the event analysis OpenAPI supports queries for up to 50,000 pieces of grouped data. In the use of some customers, there may be a large packet base, and the limit of 50,000 cannot meet the situation where customers obtain data. Therefore, after the privatization 4.6 version (inclusive), it supports obtaining CSV format file data through OpenAPI, and up to 1 million pieces of data can be obtained at one time through this method.

<span id="2ad7e348"></span>
## Request description


* **Context\-Path**: /datafinder

* **Path**：/openapi/v1/{app_id}/downloads

* **Method**: POST

* **Content\-type**: application/json


<span id="734f0dfa"></span>
## Request parameters


* **Body**:

   
   |**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
   |---|---|---|---|---|
   |result_id |string |No |123456 |Choose one of DSL, priority result_id, download data according to result_id |
   |dsl |string |No |without |Choose one of the two result_id, give priority to result_id, download the data according to dsl, use the limit field in the page of dsl to limit the number of returned items, and the offset is invalid |
   


<span id="a2311005"></span>
## Return parameters


* **Response**

   Return to zip file

* **Header**

   * Content\-Disposition: attachment; filename={file_name}.zip

   * Content\-Type: application/zip


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">Number of bars limit: Maximum number of returned bars 100 w</div>


2. <div data-tips="true" data-tips-type="tip">Concurrency limit: 1 per project_id/app_id in Saas; no limit for privatization.</div>


3. <div data-tips="true" data-tips-type="tip">Custom indicator limitations: Currently, only atomic indicators are supported for export, and custom indicators after secondary calculation are not supported.</div>
