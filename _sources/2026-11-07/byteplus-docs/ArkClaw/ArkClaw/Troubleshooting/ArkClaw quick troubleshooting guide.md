---
title: "ArkClaw quick troubleshooting guide"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_quick_troubleshooting_guide"
---

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This guide is only applicable to personnel with ArkClaw message sending permissions and <a href="https://docs.byteplus.com/en/docs/ArkClaw/Accessing_from_terminals">ArkClaw terminal</a> login permissions.</div>


<span id="PGplewEl"></span>
## Debugging information

Enter the following commands in channels such as WebUI:


|**Command** |**Usage** |**Example** |
|---|---|---|
|`/help` |Show help information |`/help` |
|`/commands` |List all available commands |`/commands` |
|`/status`<br><br> |Current status: model, token usage, provider quota |`/status` |
|`/whoami`<br><br> |Show the sender ID (alias: `/id`) |`/whoami` |
|`/context`<br><br> |Context composition details |`/context list`, `/context detail`, `/context json` |
|`/usage`<br><br> |Control token/cost display per turn |`/usage off`, `/usage tokens`, `/usage full`, and `/usage cost` |
|`/verbose` |Detailed output mode |`/verbose on` |


<span id="tu9nBEBT"></span>
## Quick troubleshooting

<span id="2hlG23f1"></span>
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


<span id="1rGuSDtH"></span>
### **Three essential troubleshooting commands**

When you encounter any issue, execute the following commands to determine the cause.

> 90% of issues can be diagnosed from the output of these three commands.


```Bash
openclaw status --all
openclaw doctor --repair
openclaw logs --follow
```


<span id="HI7J8m81"></span>
### **Quick reference for key commands**


|**Command** |**Usage** |
|---|---|
|`openclaw status` |Overall status overview |
|`openclaw status --all` |Full diagnostic report (safe to share) |
|`openclaw status --deep` |Deep inspection including provider checks |
|`openclaw gateway status` |Service/process status |
|`openclaw gateway restart` |Restart the gateway |
|`openclaw doctor` |Automatic diagnosis |
|`openclaw doctor --fix` |Auto healing |
|`openclaw doctor --repair` |Aggressive fix |
|`openclaw models status` |Model authentication status |
|`openclaw channels status --probe` |Channel connection status |
|`openclaw logs --follow` |Real\-time logs |
|`openclaw security audit` |Security audit |


<span id="qawDDUjX"></span>
## Quick issue resolution

<span id="hLM9G9Bb"></span>
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


<span id="k6ZvzzCW"></span>
### **Command not responding or executing slowly**

<span id="FDD2NqsV"></span>
#### **Symptoms**


* The user receives no response after sending commands such as `/new`, `/reset`, and `/status`.

* The user obtains a response after a long delay.


<span id="e3F7NiG7"></span>
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
   |No message reached the gateway |No log output |Restart the gateway. |
   |Command not recognized |Message received but not processed by executing commands<br><br> |Check commands.text and commands.native. |
   |Session operation stuck |Logs show processing started but no API call was made. |Check the session file size and clean up if necessary. |
   |Model API timeout<br><br> |Logs show the API request was sent.<br><br> |Check provider status, network connectivity, and API key. |
   |Slow response generation |API responded but streaming is slow |The model itself is slow (normal for large models such as Opus). |
   

4. Common root causes & solutions.

   * **Root cause A: Overly large startup prompt**

      * The `/new` command triggers the startup prompt when BOOTSTRAP.md exists.

      * If the system prompt is large and includes multiple project context files, the first response will be slow.

      * Solution: Simplify the content in BOOTSTRAP.md and remove unnecessary startup checks.

   * **Root cause B: Oversized session files**

      ```Bash
      ls -lhS ~/.openclaw/agents/*/sessions/*.jsonl | head -10
      du -sh ~/.openclaw/agents/*/sessions/
      ```
      

      * If a single JSONL file exceeds 50 MB, manually compress it or reset the session.

      * Solution: `openclaw gateway restart`


<span id="IlJB8pjf"></span>
### **Model authentication/API error**

<span id="9Nm5654r"></span>
#### **Symptoms**


* "429 You have exceeded the weekly usage quota. It will reset at 2026\-03\-23 00:00:00 +0800 CST. We recommend upgrading your plan for more quota, or waiting for the reset"

* "401 The API key doesn't exist. "


<span id="sn0b45rj"></span>
#### **Common causes & solutions**


* **Cause A: Coding Plan quota exhausted.** 

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_61359cf932e7b49b2a75928446486c84.png) </span>

* **Cause B: Incorrect API Key**

   Check whether the API Key is correct.

* **Cause C: Model not activated**

   Go to the [Model activation page in the ModelArk console](https://console.byteplus.com/ark/region:ark+cn-beijing/openManagement?LLM=%7B%7D&advancedActiveKey=model) and activate the model.


<span id="rUtzh4fa"></span>
### **Message not triggered/no response received**

<span id="YbkXpeWm"></span>
#### **Symptoms**


* No response when sending messages to the bot.

* No response when @mentioning the bot in group chats.

* The bot works for some users but not others.


<span id="eW5yOdix"></span>
#### **Troubleshooting process**

```Bash
# View the allowlist and channel configuration.
openclaw status

# Confirm whether the logs contain blocked/skip/unauthorized.
tail -f /tmp/openclaw/openclaw-$(date +%Y-%m-%d).log | grep "blocked\|skip\|unauthorized"
```


<span id="TtdBmEvi"></span>
#### **Common causes & solutions**


|**Cause** |**Check method** |**Solution** |
|---|---|---|
|The sender is not in the allowlist. |Execute the `openclaw status` command and check AllowFrom. |Add the user to `channels.<provider>.allowFrom`. |
|@mentioning required in group chats |Check `requireMention` settings. |Specify `requireMention: false` or make sure that the bot is properly @mentioned. |
|Incorrect `dmPolicy` setting |Check `dmPolicy`. |Set to `open` or `allowlist`. |
|Group chat not in the allowlist |Check `groups` or `guilds` configuration. |Add the group ID to the configuration. |
|Telegram bot received no messages |Check the bot token and webhook. |Make sure the bot token is correct. |
|Pending approval in pairing mode |`openclaw pairing list <channel>` |Approve the pairing or adjust dmPolicy. |


<span id="V6mVPuAn"></span>
###
