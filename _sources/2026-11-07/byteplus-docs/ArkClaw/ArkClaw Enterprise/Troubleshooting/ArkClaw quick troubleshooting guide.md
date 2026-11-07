---
title: "ArkClaw quick troubleshooting guide"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_quick_troubleshooting_guid_"
---

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This guide is only applicable to personnel with ArkClaw message sending permissions and <a href="http://volcengine.com/docs/87732/2272767">ArkClaw terminal</a> login permissions.</div>


<span id="Dnk46xP6"></span>
## Debugging information

Enter the following commands in conversations via channels such as Feishu or WebUI:


|**Command** |**Usage** |**Sample value** |
|---|---|---|
|`/help` |Show help information. |`/help` |
|`/commands` |List all available commands. |`/commands` |
|`/status`<br><br> |Current status: model, token usage, provider quota. |`/status` |
|`/whoami`<br><br> |Show the sender ID (alias: `/id`). |`/whoami` |
|`/context`<br><br> |Context composition details. |`/context list`, `/context detail`, `/context json` |
|`/usage`<br><br> |Control token/cost display per turn. |`/usage off`, `/usage tokens`, `/usage full`, `/usage cost` |
|`/verbose` |Detailed output mode. |`/verbose on` |


<span id="J50Eyn1A"></span>
## Quick troubleshooting

<span id="1FCSXrYL"></span>
### **Quick classification**

Quickly identify the problem layer:

```Bash
# Step 1: Overall status (most important)
openclaw status

# Step 2: Gateway service status
openclaw gateway status

# Step 3: Automatic diagnosis
openclaw doctor

# Step 4: Real-time logs
openclaw logs --follow
```


<span id="eGs43ooC"></span>
### **Three essential troubleshooting commands**

When you encounter any issue, execute the following commands to determine the cause.

> 90% of issues can be diagnosed from the output of these three commands.


```Bash
openclaw status --all
openclaw doctor --repair
openclaw logs --follow
```


<span id="uJmRRkNI"></span>
### **Quick reference for key commands**


|**Command** |**Usage** |
|---|---|
|`openclaw status` |Overall status overview. |
|`openclaw status --all` |Full diagnostic report (safe to share) |
|`openclaw status --deep` |Deep inspection including provider checks |
|`openclaw gateway status` |Service/process status |
|`openclaw gateway restart` |Restart the gateway. |
|`openclaw doctor` |Automatic diagnosis. |
|`openclaw doctor --fix` |Auto healing. |
|`openclaw doctor --repair` |Aggressive fix. |
|`openclaw models status` |Model authentication status |
|`openclaw channels status --probe` |Channel connection status |
|`openclaw logs --follow` |Real\-time logs |
|`openclaw security audit` |Security audit |


<span id="OdHnu6B1"></span>
## Quick issue resolution

<span id="EP5htZIz"></span>
### **No messages received in Feishu**

```Bash
openclaw channels status --probe
openclaw pairing list --channel feishu
openclaw config get channels
openclaw logs --follow
```


**Troubleshooting checklist:** 


1. **DM pairing:**  Confirm that user pairing requests have been approved.

   ```Bash
   openclaw pairing list --channel feishu
   openclaw pairing approve <requestId>
   ```
   

2. **Group mention:**  In group chats, the bot only responds when it is  **@mentioned**.

   Check whether the `requireMention` setting is correct.

3. **Permission/Scope:**  View logs for `403` error code or the `missing_scope` key field.


<span id="yqH6mwuj"></span>
### No streaming output in Feishu


1. Upgrade the Feishu plugin to the latest version.

   ```Bash
   npx -y @larksuite/openclaw-lark-tools update
   ```
   

2. Enable streaming output.

   ```Bash
   openclaw config set channels.feishu.streaming true
   ```
   

3. Make sure the Feishu application has been granted the `cardkit:card:write` permission.


<span id="cfK3mwNy"></span>
### Other Feishu issues


1. Run the Feishu diagnostic tool.

   ```Bash
   # Execute in the terminal
   npx @larksuite/openclaw-lark-tools doctor
   ```
   

2. Manually resolve the issues or execute the following command in the terminal to resolve them automatically.

   ```Bash
   # Execute in the terminal
   npx @larksuite/openclaw-lark-tools doctor --fix
   ```
   


<span id="CEjnv27r"></span>
### **No response or error occurred**

```Bash
openclaw models status
openclaw models status --probe
openclaw logs --follow
```


**Common issues:** 


|Error |Solution |
|---|---|
|HTTP 429 rate limit |Reduce request frequency or upgrade API quota. |
|HTTP 401/403 |The API Key has expired or is invalid. Reconfigure it. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">We recommend that you switch models. For the Coding Plan, modifications on the page will take effect in 3–5 minutes.</div>


<span id="URW7kClw"></span>
### **Command not responding or executing slowly**

<span id="wPkGwLds"></span>
#### Issue


* The user receives no response after sending commands such as `/new`, `/reset`, and `/status`.

* The user obtains a response after a long delay.


<span id="cOpEVU1o"></span>
#### **Troubleshooting process**


1. Confirm that the gateway is running.

   ```Bash
   openclaw gateway status
   ```
   

   * Confirm that `Runtime` status is `running`.

   * Confirm that `RPC probe` is `ok`.

2. Check whether message reception records exist in the logs.

   ```Bash
   # Enable the log service and ask the customer to send a message.
   tail -f /tmp/openclaw/openclaw-$(date +%Y-%m-%d).log
   ```
   

3. Locate the stage where the issue occurs.

   
   |**Stage** |**How to check** |**Solution** |
   |---|---|---|
   |No message reached the gateway |No log output. |Restart the gateway. |
   |Command not recognized |Message received in logs, but no command was processed.<br><br> |Check commands.text and commands.native. |
   |Session operation stuck |Logs show processing started but no API call was made. |Check the session file size and clean up if necessary. |
   |Model API timeout<br><br> |Logs show the API request was sent.<br><br> |Check provider status, network connectivity, and API key. |
   |Slow response generation |API responded but streaming is slow. |The model itself is slow (normal for large models such as Opus). |
   

4. Common root causes & solutions.

   * Root cause A: Overly large startup prompt

      * The `/new` command triggers the startup prompt when BOOTSTRAP.md exists.

      * If the system prompt is excessively large and multiple project context files are added, the first response will be slow.

      * Solution: Simplify the content in `BOOTSTRAP.md` and remove unnecessary startup check logic.

   * Root cause B: Oversized session files

      ```Bash
      ls -lhS ~/.openclaw/agents/*/sessions/*.jsonl | head -10
      du -sh ~/.openclaw/agents/*/sessions/
      ```
      

      * Criteria: Single JSONL file \> 50 MB.

      * Solution:

         1. Manually compress oversized session files or reset the session.

         2. Restart the gateway.

            ```Bash
            openclaw gateway restart
            ```
            

&nbsp;


<span id="i2IDuCXx"></span>
### **Model authentication/API error**

<span id="LtqwwBOV"></span>
#### Issue


* "429 You have exceeded the weekly usage quota. It will reset at 2026\-03\-23 00:00:00 +0800 CST. We recommend upgrading your plan for more quota, or waiting for the reset"

* "401 The API key doesn't exist. "


<span id="vvbg5ePb"></span>
#### **Common causes & solutions**


* Cause A: Coding Plan quota exhausted.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1b6728d9cedf625dad347d52a4abf9cd.png) </span>

* Cause B: Incorrect API Key

   Check whether the API Key is correct.

* Cause C: Model not activated

   Go to the [Model activation page in the ModelArk console](https://console.byteplus.com/ark/region:ark+cn-beijing/openManagement?LLM=%7B%7D&advancedActiveKey=model) and activate the model.


<span id="CpiLWGlZ"></span>
### **Message not triggered/no response received**

<span id="d0Ly7MLS"></span>
#### **Issue**


* No response when sending messages to the bot.

* No response when  **@mentioning the bot** in group chats.

* The bot works for some users but not others.


<span id="h5bANpXE"></span>
#### **Troubleshooting process**

```Bash
# View the allowlist and channel configuration.
openclaw status

# Confirm whether the logs contain blocked/skip/unauthorized.
tail -f /tmp/openclaw/openclaw-$(date +%Y-%m-%d).log | grep "blocked\|skip\|unauthorized"
```


<span id="5ec03BHs"></span>
#### **Common causes & solutions**


|**Cause** |**Check method** |**Solution** |
|---|---|---|
|The sender is not in the allowlist. |Execute the `openclaw status` command and check AllowFrom. |Add the user to `channels.<provider>.allowFrom`. |
|`@`mentioning required in group chats. |Check `requireMention` settings. |Specify `requireMention: false` or make sure that the bot is properly `@mentioned`. |
|Incorrect `dmPolicy` setting. |Check `dmPolicy`. |Set to `open` or `allowlist`. |
|The group chat is not in the allowlist. |Check `groups` or `guilds` configuration. |Add the group ID to the configuration. |
|Telegram bot received no messages. |Check the bot token and webhook. |Make sure the bot token is correct. |
|Pending approval in pairing mode. |`openclaw pairing list <channel>` |Approve the pairing or adjust dmPolicy. |


<span id="VymUJUYq"></span>
### Failed to configure a scheduled task

<span id="DIDLTFXF"></span>
#### Issue

Failed to configure a scheduled task, with the error: Gateway authorization required.

<span id="PaB9vq0Z"></span>
#### Common causes & solutions

Enter the ArkClaw terminal and execute the following commands:

```Bash

npm install -g ./openclaw-2026.3.13.tgz

openclaw gateway restart
```
