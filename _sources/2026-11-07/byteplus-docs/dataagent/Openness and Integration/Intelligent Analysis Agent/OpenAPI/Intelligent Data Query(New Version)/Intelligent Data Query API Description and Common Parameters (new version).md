---
title: "Intelligent Data Query API Description and Common Parameters (new version)"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Intelligent_Data_Query_API_Description_and_Common_Parameters_new_version"
---

<span id="926bddaf"></span>
# Overview

This document introduces the Open API related to the intelligent query feature of the intelligent analysis Agent. You will learn how to use the API to enable the agent to query data using natural language.

Caution: Before using the API described in this document, you must complete the preliminary steps of integrating JWT\-Token, applying for a Token, and configuring the agent in advance. Please review the invocation method first. For details, refer to [Invocation Methods](https://docs.byteplus.com/docs/dataagent/Invocation_Methods).

<span id="38093ebd"></span>
# Notes

The new version of the intelligent query OpenAPI does not support invocation from the Feishu platform. For Feishu, it is recommended to use the intelligent analysis Agent's query feature by directly integrating the Feishu bot.

<span id="54ecf614"></span>
# API common parameters


* **Context\-path**: https://{domain}/bi

* **Path\-parameters:** 

   
   |**Parameter** |**Type** |**Required** |**Example value** |**Description** |
   |---|---|---|---|---|
   |domain |string |Yes |None |* SaaS environment domain: `https://console.volcengine.com/bi/datawind`<br><br>* Private deployment domain: Actual deployed environment domain address`${domain}/bi` |
   

* **Response**:

   ```json
   {
           "code": "llm/ok",
           "data": [{REULT_OBJECT}],
           "message": {}
   }
   ```
   

   * code: Status code, "llm/ok" indicates success, others indicate failure

   * message: Success or failure information

   * data: Result data, which is a JSON object array


<span id="83c19a56"></span>
# API list


|API |Description |
|---|---|
|[Create a Session](https://docs.byteplus.com/docs/dataagent/Create_a_Session) |Create session |
|[Retrieve Session Information](https://docs.byteplus.com/docs/dataagent/Retrieve_Session_Information) |Get session information |
|[Update Session](https://docs.byteplus.com/docs/dataagent/Update_Session) |Update session |
|[Session Completion](https://docs.byteplus.com/docs/dataagent/Session_Completion) |Chat completion |
|[Retrieve Session Result](https://docs.byteplus.com/docs/dataagent/Retrieve_Session_Result) |Get conversation result |
