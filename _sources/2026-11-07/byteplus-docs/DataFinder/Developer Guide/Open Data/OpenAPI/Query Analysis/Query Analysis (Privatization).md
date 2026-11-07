---
title: "Query Analysis (Privatization)"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Query_Analysis_Privatization"
---

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Privatization and SaaS are different in that they need to be divided into two interfaces to obtain query results.</div>


<span id="033866f7"></span>
## Request description


* **Context\-Path**: /datafinder

* **Path**：/openapi/v1/analysis

* **Method**: POST

* **Content\-type**: application/json


<span id="5fc8761e"></span>
## Request parameters


* **Body**:

   * Request parameters are described in query DSL, see[4. DSL structure description](https://docs.byteplus.com/docs/DataFinder/API_Description_and_Public_Parameters_Query_Analysis#8af6aa94)

   * Data is encoded in UTF\-8.


<span id="fd394e47"></span>
## Return parameters


* **Response**:

   ```json
   {
           "code": 200,
           "message": "success"
           "data":  {
               "result_id": xxx
           }
   }
   ```
   

   Field meaning description:

   
   |**Field** |**Type** |**Description** |
   |---|---|---|
   |result_id |int |query result ID |
