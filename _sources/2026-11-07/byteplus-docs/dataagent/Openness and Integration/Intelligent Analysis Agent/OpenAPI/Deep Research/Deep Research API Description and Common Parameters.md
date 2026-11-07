---
title: "Deep Research API Description and Common Parameters"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Deep_Research_API_Description_and_Common_Parameters"
---

<span id="acd70345"></span>
# Overview

This document introduces the Open API related to the deep research features of the Intelligent Analysis Agent. You will learn how to perform deep research tasks and obtain deep research reports through the API.

Caution: Before using the APIs described in this document, you must complete the preliminary steps of integrating JWT\-Token, applying for a Token, and configuring the agent in advance. Please familiarize yourself with how to call the API. For details, refer to [Invocation Methods](https://docs.byteplus.com/docs/dataagent/Invocation_Methods).

<span id="537f939a"></span>
# API common parameters


* **Context\-path**: https://

* **Path\-parameters:** 

   
   |**Parameter** |**Type** |**Required** |**Description** |
   |---|---|---|---|
   |domain |string |Yes |* SaaS environment domain: `https://console.volcengine.com/bi/datawind`<br><br>* Domain address of the actual deployed environment: `${domain}/bi` |
   

* **Response**:

   ```json
   {
           "code": "llm/ok",
           "data": [{REULT_OBJECT}],
           "message": {}
   }
   ```
   

   * code Status code, "llm/ok" indicates success, others indicate failure

   * message Success or failure information

   * data Result data, which is a JSON object array


<span id="a8356e18"></span>
# API list


|API |Description |
|---|---|
|[Execute Deep Research Task](https://docs.byteplus.com/docs/dataagent/Execute_Deep_Research_Task) |Call the interface to perform a deep research task. |
|[Retrieve Task Status](https://docs.byteplus.com/docs/dataagent/Retrieve_Task_Status) |View the task status of a specific deep research task. |
|[Get Task Details](https://docs.byteplus.com/docs/dataagent/Get_Task_Details) |View the details of a specific deep research task. |
|[File Upload](https://docs.byteplus.com/docs/dataagent/File_Upload) |Upload files for scenarios in general agent deep research tasks where additional files need to be analyzed. |
