---
title: "Intelligent Data Query API Description and Public Parameters (old version)"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Intelligent_Data_Query_API_Description_and_Public_Parameters_old_version"
---

<span id="926bddaf"></span>
# Overview

This document introduces the Open API related to the smart query functionality of the intelligent analysis Agent. You will learn how to use the API to enable the Agent to query data using natural language.

Caution: Before using the API described in this document, you must complete the preliminary steps of integrating JWT\-Token, applying for a Token, and configuring the Agent in advance. Please review the invocation method first. For details, refer to [Invocation Methods](https://docs.byteplus.com/docs/dataagent/Invocation_Methods).

<span id="06525895"></span>
# API public parameters


* **Context\-path**: https://{domain}/aeolus/llm/openApi/v2/chatbi/query

* **Path\-parameters:** 

   
   |**Parameter** |**Type** |**Required** |**Description** |
   |---|---|---|---|
   |domain |string |Yes |* SaaS environment domain: `https://console.volcengine.com/bi/datawind`<br><br>* Private deployment domain: Actual deployed environment domain address`${domain}/bi` |
   

* **Response**:

   ```json
   {
           "code": "llm/ok",
           "data": [{REULT_OBJECT}],
           "message": {}
   }
   ```
   

   * code Status code, "llm/ok" indicates success, other values indicate failure

   * message Success or failure information

   * data Result data, which is a JSON object array


<span id="e457027f"></span>
# API list


|API |Description |
|---|---|
|[Intelligent Data Query for Lark Client](https://docs.byteplus.com/docs/dataagent/Intelligent_Data_Query_for_Lark_Client) |Invoke the OpenAPI interface to query data using the intelligent analysis Agent on the Lark client. |
|[Intelligent Data Query for PC](https://docs.byteplus.com/docs/dataagent/Intelligent_Data_Query_for_PC) |Invoke the OpenAPI interface to query data using the intelligent analysis Agent on the PC client. |
