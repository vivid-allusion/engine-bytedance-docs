---
title: "Open API Description"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Open_API_Description"
---

<span id="926bddaf"></span>
# Overview

This article introduces you to the Open API of IDA, and you will learn how to use the agent's Q & A\-related functions through the API.

Note: Before you use the API described in this article, you need to complete the pre\-operation of accessing JWT\-Token and applying for Token and configure the agent in advance. Please understand the calling method first. Please read the details [Get jwt token](https://docs.byteplus.com/docs/dataagent/Get_jwt_token), [Set token and domain Global Variables](https://docs.byteplus.com/docs/dataagent/Set_token_and_domain_Global_Variables).

<span id="38093ebd"></span>
# API function call parameters


* **Context\-path**: https://{domain}/bi

* **Path\-parameters:** 

   
   |**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
   |---|---|---|---|---|
   |domain |string |Yes |without |* Privatized domain: the actual deployed environment domain address `${domain}/bi` |
   

* **Response**:

   ```json
   {
           "code": "llm/ok",
           "data": [{RESULT_OBJECT}],
           "message": {}
   }
   ```
   

   * Code status code, "llm/ok" for success, others for failure

   * Message Success or failure message

   * Data The result data is a json object array


<span id="83c19a56"></span>
# API List

<span id="1781fe11"></span>
## Create and acquire a session


|API |Explain |
|---|---|
|[iDA - Create Session](https://docs.byteplus.com/docs/dataagent/iDA_-_Create_Session) |Create a session |
|[iDA - Get Session List](https://docs.byteplus.com/docs/dataagent/iDA_-_Get_Session_List) |Get session list |
|[iDA - Get Session Details](https://docs.byteplus.com/docs/dataagent/iDA_-_Get_Session_Details) |Get session details |
|[iDA - Get Session History/Hide Specified Tasks](https://docs.byteplus.com/docs/dataagent/iDA_Get_Session_History_Hide_Specified_Tasks) |Get session history/hide specified tasks |


<span id="a97e214d"></span>
## Agent\-related operations


|API |Explain |
|---|---|
|[Read Agent List](https://docs.byteplus.com/docs/dataagent/Read_Agent_List) |Read agent list |
|[Get Default Agent](https://docs.byteplus.com/docs/dataagent/Get_Default_Agent) |Get default agent |
|[Get Agent Details](https://docs.byteplus.com/docs/dataagent/Get_Agent_Details) |Get agent details |
|[iDA - Acquisition Knowledge Base Project](https://docs.byteplus.com/docs/dataagent/iDA_-_Acquisition_Knowledge_Base_Project) |Acquire Knowledge Base Project |
|[iDA - Get List of Knowledge Bases Under the Project](https://docs.byteplus.com/docs/dataagent/iDA_-_Get_List_of_Knowledge_Bases_Under_the_Project) |Get the list of knowledge bases under the project |
|[iDA - Get a List of Documents Under the Knowledge Base](https://docs.byteplus.com/docs/dataagent/iDA_-_Get_a_List_of_Documents_Under_the_Knowledge_Base) |Get the list of documents under the Knowledge Base |
|[Agent Binding Knowledge Base](https://docs.byteplus.com/docs/dataagent/Agent_Binding_Knowledge_Base) |agent binding knowledge base |
|[View Agent Binding Knowledge](https://docs.byteplus.com/docs/dataagent/View_Agent_Binding_Knowledge) |View agent binding knowledge |
|[Delete Knowledge Base Bindings](https://docs.byteplus.com/docs/dataagent/Delete_Knowledge_Base_Bindings) |Delete Knowledge Base Bindings |
|[iDA - File Upload](https://docs.byteplus.com/docs/dataagent/iDA_-_File_Upload) |file upload |


<span id="2aa38f66"></span>
## Prompt template


|API |Explain |
|---|---|
|[iDA - Get List of Prompt Templates](https://docs.byteplus.com/docs/dataagent/iDA_-_Get_List_of_Prompt_Templates) |Get a list of prompt word templates |
|[iDA -Create Prompt Template](https://docs.byteplus.com/docs/dataagent/iDA_-Create_Prompt_Template) |Create a prompt word template |
|[iDA - Update Prompt Template](https://docs.byteplus.com/docs/dataagent/iDA_-_Update_Prompt_Template) |Update prompt word template |


<span id="1970b637"></span>
## A2A


|API |Explain |
|---|---|
|[iDA - Acquiring Available Scenes and Skills](https://docs.byteplus.com/docs/dataagent/iDA_-_Acquiring_Available_Scenes_and_Skills) |Acquire Available Scenes and Skills |
|[Start Streaming Q & A](https://docs.byteplus.com/docs/dataagent/Start_Streaming_Q_A) |Start streaming Q & A |
|[Resubscribe to the Task](https://docs.byteplus.com/docs/dataagent/Resubscribe_to_the_Task) |Subscribe to the task again |
|[Get a Task Snapshot](https://docs.byteplus.com/docs/dataagent/Get_a_Task_Snapshot) |Get a task snapshot |
|[Get Session Task List](https://docs.byteplus.com/docs/dataagent/Get_Session_Task_List) |Get session task list |
|[Cancel Task](https://docs.byteplus.com/docs/dataagent/Cancel_Task) |Cancel task |


<span id="aa146223"></span>
## Skill Center


|API |Explain |
|---|---|
|[Upload Skills to Skill Center](https://docs.byteplus.com/docs/dataagent/Upload_Skills_to_Skill_Center) |Upload skills to Skill Center |
