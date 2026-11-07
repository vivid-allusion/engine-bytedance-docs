---
title: "ArkClaw usage path analysis"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/ArkClaw-usage-path-analysis"
---

This topic describes how to install the path analysis Skill in ArkClaw. You can perform path analysis directly from the ArkClaw page.

## Prerequisites

* You can already log in to and use **ArkClaw** (OpenClaw agent). For operations, see [Getting a dedicated ArkClaw in one click (Personal edition)](https://docs.byteplus.com/en/docs/ArkClaw/Employee-side_console_usage_overview) and [Applying for an ArkClaw instance (Enterprise edition)](https://docs.byteplus.com/en/docs/ArkClaw/Applying_for_ArkClaw_instances_).

* You have applied for an **Access Key ID** and **Secret Access Key** with read\-only/diagnostic permissions for NA instances in the BytePlus console, and you have obtained the region ID where the target instance resides (this topic uses cn\-beijing as an example). For operations, see [API Keys (Access Key and API Key)](https://docs.byteplus.com/en/docs/IAM/about-access-keys).

   > **warning**

   > Protect your Access Key ID and Secret Access Key to avoid exposing them externally.

## Procedures

### Step 1: Install the path analysis skill

1. Open [findskill.com](https://findskill.com/) in a browser on your local computer.

2. In the search box, search for byted\-na\-path\-analysis.

3. In the search results, click **byted\-na\-path\-analysis** to open the details page, and copy the installation command, for example:

   ```Bash
   npx skills add https://skills.volces.com/skills/volcengine/na -s byted-na-path-analysis --agent openclaw
   ```

4. Return to ArkClaw, create a new task session, paste and send the preceding command in the input field, and wait for the installation to complete.

### Step 2: Configure access credentials

The Skill itself does not carry any credentials. You need to write your own BytePlus keys into the cloud computer environment variables.

1. Click the **cloud computer** icon on the right side of the ArkClaw page.

2. In the cloud computer, open the terminal.

3. Run the following command to create and edit credentials.​

   ```Bash
   vim ~/env.sh
   ```

4. Press `i` to enter the edit mode and input the following content.

   ```Bash
   export VOLCENGINE_ACCESS_KEY="YOUR_ACCESS_KEY_ID"     Replace #YOUR_ACCESS_KEY_ID with your AK
   export VOLCENGINE_SECRET_KEY="YOUR_SECRET_ACCESS_KEY" Replace #YOUR_SECRET_ACCESS_KEY with your SK
   export VOLCENGINE_REGION="cn-beijing"                 Replace #cn-beijing with your region
   ```

5. Press `Esc` to exit edit mode, then type `:wq` and press Enter.

### Step 3: Load credentials in the session

1. In the left navigation tree, click **My tasks.**

2. In the ArkClaw task session input field, enter the following content and send it:

   ```Plain Text
   Please refer to ~/env.sh to configure the environment variables.
   ```

   > **tip**

   > Each newly opened task session requires loading credentials.

   ## Verification

   1. In the ArkClaw task session input field, enter the following content and send it:

   ```Plain Text
   Can <your-instance-a> and <your-instance-b> connect to each other?
   ```

2. After the path analysis runs, the model provides a connectivity conclusion between the two instances in the session, typically including:

   * **Connectivity**: A clear "reachable/unreachable" conclusion.

   * **Path summary**: The main network nodes and forwarding path from the source instance to the destination instance.

   * **Blocking point** (if unreachable): Identifies the specific link such as security group, route table, ACL, network policy, or subnet configuration, and provides adjustment suggestions.
