---
title: "Downloading files to multiple instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Download_files_to_multiple_instances"
---

You can batch download the target file to multiple instances directly in the ECS console without logging in to the instances in advance.  Additionally, this method supports file upload or download actions for instances without public network access.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This feature relies on the cloud assistant Agent and operation orchestration. You can also directly download files to designated instances on the Operation Orchestration page. For details, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Creating_a_batch_actions_instance_task">Creating batch instance tasks to directly download files</a>.</div>


<span id="frwr0IPx"></span>
## Prerequisites


* When using the Operation Orchestration Service for the first time, you need to create the CustomRoleForOOS role to complete the authorization. [Learn more](https://docs.byteplus.com/en/docs/ecs/Preparation).

* When batch downloading files, the selected instances must meet the following conditions:

   * All instances must be either Linux or Windows instances.

   * All instances must be in the **Running** state.

   * The cloud assistant Agent has been installed on all instances, and its state is **Running**.


<span id="DlHhGw92"></span>
## Precautions

Only one file can be uploaded per task.

<span id="gszUAQby"></span>
## Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the project and region to which the target instance belongs.

4. On the Instances page, select one or more instances, and click the "... \> Download file" button at the bottom of the list.

5. The system displays a "In bulk download file" window. Here, you can view operable instances, inoperable instances, and their reasons.

   > If there are inoperable instances, this indicates that some instances do not meet the conditions required to perform this action. You can address the issue based on prompts and try again once the conditions are met.   
   

6. Click the "Continue" button to go to the operation orchestration page and configure related arguments. For specific configurations, please refer to [Creating batch instance task - Download file](https://docs.byteplus.com/en/docs/ecs/Creating_a_batch_actions_instance_task).

7. [Log in to the instance](https://docs.byteplus.com/en/docs/ecs/Overview-1) and check whether the file has been uploaded.


<span id="uNdG1jot"></span>
## Related document


* [Install the cloud assistant Agent](https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client)

* [Operations orchestration](https://docs.byteplus.com/en/docs/ecs/Overview_of_Process_Orchestration)

* For more methods to upload or download files, see [Uploading or downloading files](https://docs.byteplus.com/en/docs/ecs/Local-data-uploading-overview).
