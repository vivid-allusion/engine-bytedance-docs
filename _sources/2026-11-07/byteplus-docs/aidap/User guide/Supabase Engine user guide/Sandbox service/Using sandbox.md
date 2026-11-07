---
title: "Using sandbox"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Using_sandbox"
---

Sandbox is an isolated runtime environment provided by AI Native BaaS for Supabase to workspaces using the Supabase engine. It runs commands, calls large models, or executes code in a controlled and recyclable environment. You can select a template, enter commands, and quickly create sandbox execution on the console's sandbox usage page.

<span id="h9GmvhGu"></span>
## Background


* Sandboxes are created based on templates. The platform has pre\-installed multiple templates (such as opencode, claude, base, code\-interpreter, codex, etc.), each with different runtimes and tools.

* Each sandbox has a remaining TTL (time to live) and is automatically reclaimed upon expiration.

* In addition to creating and executing manually on the Console, sandboxes can also be called within business code via the SDK.


<span id="bruHdAer"></span>
## Prerequisites


* A workspace is created and its status is **Running**.

* The target current branch is in **running** status.

* The number of sandboxes created on the day did not exceed the quota configuration.


<span id="Jrsf8g5z"></span>
## Procedure


1. Login to [AI Native Database Platform](https://console.byteplus.com/aidap).

2. Select the target project and target region in the top navigation bar.

3. Enter the **Branch management** page of the target workspace. You can enter the **Branch management** page of the target workspace by either of the following two ways.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d6a6bd14e29a4147670589c8181cc1a.png)<sub> </sub></span>**Branch management** in the center navigation bar of the page, then click the icon<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name at the top left of the page to select the target workspace from the dropdown list and enter the **Branch management** page of the target workspace.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)<sub> </sub></span>**Workspaces** in the center navigation bar to enter the **Workspaces** page **.**  Click the target workspace name on the **Workspaces** page to enter the target workspace **Overview** page. On the **Overview** page, click **All branches** at the top right of the branches list to enter the target workspace **Branch management** page.

4. On the **Branch management** page, click the name of the target branch to access the **Branch overview** page.

5. On the **Branch overview** page, select **Sandbox service** \> **Sandbox usage** tab.

6. Select the required template from the **Template list** on the left. After selecting, the template’s description, template size, preinstalled tools, and last updated time display on the right.

7. Enter the command to execute in the sandbox in the command input box. For example, when using the opencode template, enter opencode run "Please help me create a universal sales target improvement plan."

8. Click **Create sandbox and run**.

9. View sandbox output in the **Execution result** area at the bottom of the page. During execution, **streaming output in progress** is displayed at the top right of the page, the command input box is read\-only, and the **stop** button appears. Click **Stop** to abort execution.

10. After execution:

   * When execution succeeds, the **execution result** area displays the complete output.

   * When execution fails, the **execution result** area displays error logs and the exit code (non\-zero). Adjust the command based on the error information and click **create sandbox and run** to retry.


<span id="Bo6xoEw9"></span>
## Template description

The **Template list** shows currently available sandbox templates. After selecting a template, detailed information is shown on the right:


|**Field** |**Decscription** |
|---|---|
|Template description |Template usage description, for example, the opencode template is described as e2b sandbox opencode template. |
|Template size |Template size, for example, 800MB. |
|Preinstalled tools |The template includes preinstalled runtime and tools, such as python, node, git, and opencode. |
|Last updated |Last updated time of the template. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Different templates come preinstalled with different toolchains. Choose the appropriate template according to the commands to be executed. For example, select the template pre\-installed with Python when running Python code, and select the opencode template when calling opencode.</div>


<span id="o1b2itmb"></span>
## Call the sandbox through SDK

The **Sandbox usage** page provides **Usage example** code samples for creating and calling the sandbox through SDK. The typical process is: log in with Supabase account password to obtain an access token, call initBytedSupabaseSandbox to complete initialization, then create the sandbox and execute commands through Sandbox.create. Example code:

```JavaScript
import { createClient } from '@supabase/supabase-js'
import { initBytedSupabaseSandbox } from '@byted-supabase/sandbox'

const supabase = createClient(
  process.env.SUPABASE_URL,
  process.env.SUPABASE_ANON_KEY,
)

const { data, error } = await supabase.auth.signInWithPassword({
  email: 'user@example.com',
  password: '••••••••',
})
if (error) throw error

initBytedSupabaseSandbox({
  url: process.env.SUPABASE_URL,
  apiKey: data.session.access_token,
})

import { Sandbox } from 'e2b'

const sbx = await Sandbox.create()
try {
  const cmd = await sbx.commands.run(
    'uname -a',
    { timeoutMs: 60_000 },
  )
  console.log(cmd.stdout)
} finally {
  await sbx.kill()
}
```


<span id="ZCpT9UKe"></span>
## Execution status description


|**State** |**Decscription** |
|---|---|
|Waiting for execution |Command input completed, but "Create sandbox and run" has not been clicked. The command input box is editable, and the page displays a "Create sandbox and run" button. |
|Streaming output in progress |Sandbox created and running, the page shows "Creating sandbox and waiting for output...", the command input box is read\-only, and the action button changes to Stop. |
|Execution completed |Command executed successfully, the Execution result area displays the output, and the exit code is 0. |
|Execution failed |Command execution abnormal, the "Execution result" area shows the error log and a non\-zero exit code. |


<span id="DHwpO6gE"></span>
## Related Actions


* View all sandboxes and their status under the current branch, refer to [Viewing sandbox list](https://docs.byteplus.com/en/docs/aidap/Viewing_sandbox_list).

* View or adjust the daily sandbox creation quota, refer to [Quota management](https://docs.byteplus.com/en/docs/aidap/Quota_management).
