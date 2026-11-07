---
title: "Webhook notification"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Webhook_notification"
---

Code Pipeline provides job\-level notification reminders, supporting two methods for pushing job\-level messages via Webhook and Feishu bot, helping you stay informed about job\-level updates in a timely manner.

<span id=".6aOe5Lmm5py65Zmo5Lq6"></span>
## Feishu bot

By calling the hookurl address of the Feishu bot from the server side, job\-level notification reminders are instantly pushed to Feishu. 


* **Webhook address**: Required. Enter the hookurl address of the Feishu bot.

* **Token**: Optional. Include in the request header to verify the legitimacy of the push.

* **Notification content**: Feishu bot supports customizing notification content templates. The available options are **Basic information, trigger user, trigger event, trigger time, trigger details, link address**. All options are selected by default; at least one option must be selected.

* **Custom notification content**: In addition to the built\-in notification content templates, you can enter custom notification content in the text box. Custom notification content can reference pipeline variables, with a length limit of 200 characters.

* **Notification condition**: You can select multiple options. Optional scope: **Job started, job succeeded, job failed, job waiting, job canceled**.


<span id=".d2ViaG9vay3pgJrnlKjmoLzlvI8="></span>
## Webhook general format

Push job\-level notification reminders to your Webhook receiving platform.


* **Webhook address**: Required. Enter the hookurl address of the platform that will receive notifications.

* **Token**:  Optional. If specified, the system will include authentication information in the request header of each push request to verify the legitimacy of the push. The request header format is as follows:

   * **Key**: Authorization

   * **Value**: base64(default:{token}), where {token} is the Token value you specified.

* **Notification content**: Supports entering custom notification content, with a length limit of 200 characters. The complete notification content will be sent via a POST request. Detailed sample is as follows:

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Custom notification content can reference pipeline variables. For reference methods, please refer to <a href="https://docs.byteplus.com/en/docs/cp/Use_variables">Use variables</a>.   </div>
   

   ```json
   //Webhook general format notification sample for job-level
   {
     "ID": "630443044b292aae4c91****",  //Notification record ID
     "PipelineName":  "Java project-dev",  //Pipeline name
     "PipelineRunID": "630443044b292aae4c91****",  //Pipeline run record ID
     "URL": "https://console.byteplus.com/cp/workspace/****/pipeline/****/detail/record/****",  //Pipeline run record URL
     "TriggerBy": {
       "AccountId": 210013****,  //Main account ID
       "UserId": 107****,  //Runner ID
       "Name": ""  //Username
     },
     "Status": "Running",  //Job status, possible values include Pending, Running, Succeeded, Canceled, Timeout, Waiting, Failed
     "StageName": "stage1",  //Stage nameo
     "StageID": "***",  //Stage ID
     "TaskName": "command",  //Job name
     "TaskID": "***",  //Job ID
     "CustomContent": "***"  //Custom content
   }
   ```
   

* **Notification condition** :

   You can select multiple options. Optional scope: **Job started, job succeeded, job failed, job waiting, job canceled**.
