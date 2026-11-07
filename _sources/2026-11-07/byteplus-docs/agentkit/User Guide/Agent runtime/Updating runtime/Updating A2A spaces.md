---
title: "Updating A2A spaces"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Updating_A2A_spaces"
---

This topic describes how to update the **A2A space ** associated with an agent runtime.

<span id="oprtDdfo"></span>
## Applicable scenario

You need to change the ** A2A space** associated with an agent runtime in the following scenarios:


* You need to switch the agent to another ** A2A space** for registration and operation.

* The currently associated ** A2A space** no longer meets your requirements for business isolation, environment segmentation, or resource management.

* You need to adjust the registration address of the agent based on the network access method.

* If the runtime environment of the agent changes, you need to verify its registration information and identity identifier again.


If the agent is running properly and the associated **A2A space**, network access method, and registration address require no adjustment, you do not need to perform this operation.

<span id="GTWpdrs7"></span>
## Usage notes


* **Version requirement**: In preview mode, you can update the configuration only for the Latest version. In non\-preview mode, you do not need to specify a version and can update directly.

* **Effect**: After you update the **A2A space**, the platform registers the agent again in the target **A2A space**. It also updates the identifier, network connection information, and registration address.

   Where:

   * If private network access is enabled, the private network address is used for registration.

   * If private network access is not enabled, the public network address is used by default for registration.

   Before you perform the update, we recommend that you confirm whether the target **A2A space** and network access method meet expectations. This helps prevent impact on subsequent access paths or call relationships. For more information, refer to [A2A Center overview](https://docs.byteplus.com/en/docs/agentkit/A2A_Center_overview).


<span id="Up4I14jN"></span>
## Prerequisites

[An A2A agent space has been created](https://docs.byteplus.com/en/docs/agentkit/Creating_A2A_agent_spaces).

<span id="SrGrZ8Mj"></span>
## Procedure


1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit). 

2. In the left\-side navigation pane, select "Agent Runtime".

3. In the agent runtime list, click the name of the target agent runtime.

4. In the "Basic information" section of the **Configuration information** tab, locate **Register to A2A space** and click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1a5bf12c121e79c81297d621ca1c2dd4.png) </span> button under it **.** 

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">In preview mode, configuration updates are supported only for the Latest version. Switch the version to Latest before you perform the operation.   </div>
   

5. In the dialog box that appears, select the target A2A space, and then click "Confirm" to complete the operation.


&nbsp;

&nbsp;
