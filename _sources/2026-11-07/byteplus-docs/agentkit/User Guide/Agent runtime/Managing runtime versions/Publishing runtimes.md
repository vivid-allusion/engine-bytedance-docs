---
title: "Publishing runtimes"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Releasing_runtimes"
---

After updating an agent runtime's code or configuration, publish the runtime. The changes then take effect in the live environment. This topic describes how to publish an agent runtime.

<span id="T1SVttiY"></span>
## Release methods

AgentKit supports grey release and full release. Before publishing a runtime, we recommend that you confirm whether **preview mode** is enabled for the runtime. The version used for runtime changes and publishing differs depending on the mode.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The first release uses full release by default.</div>


* <div data-tips="true" data-tips-type="default">You can select a release method for subsequent releases.</div>



<span id="Q9lDdqvn"></span>
### Grey release


* The traffic ratio for the new version can be set from 10% to 100%. After the configured ratio is reached, you need to manually confirm the next operation, such as adjusting the ratio, performing a full release, or rolling back.

* In a grey release, if the traffic ratio of the new version does not reach 100%, the runtime is in the **Publishing** state, and you cannot initiate a new release.


<span id="9JKrVAKW"></span>
### Full release


* The traffic ratio for the new version is 100%.

* After a full release succeeds, you can initiate a new release.


&nbsp;

<span id="ePHG3Kd8"></span>
## Prerequisites

You have [created an agent runtime](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console).

<span id="Z7Gt6ol1"></span>
## Procedure


1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit). 

2. In the left\-side navigation pane, select "Agent Runtime".

3. In the agent runtime list, click the name of the target agent runtime.

4. In the upper right corner of the agent runtime details page, click the "Release" button and configure the release parameters.

   
   |Parameter​ |Description |
   |---|---|
   |Edition |The available release version depends on whether preview mode is enabled:<br><br><br>* **Preview mode enabled**: Only the **Latest version** can be selected. After release, the runtime code and configuration in the Latest version are updated to the official version and take effect in production.<br><br>* **Preview mode not enabled**: You can select the **Latest version** or a specific version number.<br><br>   * **Latest version (default)** : Creates a new version based on the most recently edited runtime code and configuration, and releases it to the live environment.<br><br>   * **Specific version number**: Releases the selected version to the live environment. When a historical version is selected, live traffic is rolled back to that version and a new release task is created. |
   |Version description |Enter a description for the agent runtime version to be released. The maximum length is 200 characters, and this field can be left blank. |
   |Release method |For subsequent agent runtime releases, you can select a release method based on your needs.<br><br><br>* Full release: The traffic ratio of the new version is 100%.<br><br>* Grey release: You can customize the traffic ratio between the online version and the grey version to be released. Select "Grey release" if you want to observe the behaviors of the new and old agent runtime versions.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When a grey version exists for an agent runtime, requests are randomly sent to the new and old agent runtime versions based on the traffic ratio.</div><br> |
   

5. Review the change comparison and confirm that the information is correct. Click "Confirm". The system opens "**Version management \> Release history**" and starts the release.


<span id="NhcMecxE"></span>
## What to do next

<span id="kPKezMxB"></span>
### View the release process

During the release of an agent runtime, you can view the release progress in real time. In a grey release, after the configured ratio is reached, you can drag the progress bar to perform a full release. For detailed instructions, see [Viewing release process](https://docs.byteplus.com/en/docs/agentkit/Viewing_release_process).

<span id="48kTRbF2"></span>
### Roll back a runtime

After the agent runtime is published, if the current runtime does not meet expectations, you can quickly roll back to a previously successful release version.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">A rollback will initiate a new release task and roll back online traffic to the historical version of the selected release task.</div>


   <div data-tips="true" data-tips-type="default">Example: To roll back the runtime to V5, select the release task with historical version V5 in the <a href="https://docs.byteplus.com/en/docs/agentkit/Viewing_release_history">Release history</a> and click "Roll back". The system will initiate a new release task with V5 as the target version.   </div>
   

* <div data-tips="true" data-tips-type="default">Associated components are rolled back at the same time. If associated components have been deleted, the rollback may fail.</div>


1. Go to the agent runtime details page and navigate to "Version management \> Release history".

2. Select the target release task and click "Roll back" in the "Actions" column.

3. In the dialog box, confirm the version information to be rolled back, and click "Confirm" to complete the operation.
