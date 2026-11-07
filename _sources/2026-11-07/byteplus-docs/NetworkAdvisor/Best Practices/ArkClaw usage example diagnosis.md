---
title: "ArkClaw usage example diagnosis"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/ArkClaw-usage-example-diagnosis"
---

This topic describes how to install the instance diagnostics Skill in ArkClaw. You can perform instance diagnostics directly from the ArkClaw page.

## Prerequisites

* You can already log in to and use **ArkClaw** (OpenClaw agent). For operations, see [Getting a dedicated ArkClaw in one click (Personal edition)](https://docs.byteplus.com/en/docs/ArkClaw/Employee-side_console_usage_overview) and [Applying for an ArkClaw instance (Enterprise edition)](https://docs.byteplus.com/en/docs/ArkClaw/Applying_for_ArkClaw_instances_).

* You have applied for an **Access Key ID** and **Secret Access Key** with read\-only/diagnostic permissions for NA instances in the BytePlus console, and you have obtained the region ID where the target instance resides (this topic uses cn\-beijing as an example). For the procedures, see [API Keys (Access Key and API Key)](https://docs.byteplus.com/en/docs/IAM/about-access-keys).

   > **warning**

   > Protect your Access Key ID and Secret Access Key to avoid exposing them externally.

   ## Procedures

### Step 1: Install the diagnosis skill

1. Open [findskill.com](https://findskill.com/) in a browser on your local computer.

2. In the search box, search for byted\-na\-diagnosis.

3. In the search results, click **byted\-na\-diagnosis** to open the details page, and copy the installation command, for example:

   ```Bash
   npx skills add https://skills.volces.com/skills/volcengine/na -s byted-na-diagnosis --agent openclaw
   ```

4. In the ArkClaw console, click **Initiate task** on the left side.

5. Paste and send the above command in the input field, wait for the installation to complete, and create a new task session.

### Step 2: Configure access credentials

The Skill itself does not carry any credentials. You need to write your own BytePlus keys into the cloud computer environment variables.

1. Click the **cloud computer** icon on the right side of the ArkClaw page.

2. In the cloud computer, double\-click the Terminal icon to open the terminal.

3. Run the following command to create and edit credentials.​

   ```Bash
   vim ~/env.sh
   ```

4. Press `i `to enter edit mode, and enter the following content.

```Bash
export VOLCENGINE_ACCESS_KEY="YOUR_ACCESS_KEY_ID"     Replace #YOUR_ACCESS_KEY_ID with your AK
export VOLCENGINE_SECRET_KEY="YOUR_SECRET_ACCESS_KEY" Replace #YOUR_SECRET_ACCESS_KEY with your SK
export VOLCENGINE_REGION="cn-beijing"                 Replace #cn-beijing with your region
```

5. Press `Esc `to exit edit mode, then enter `:wq` and press Enter.

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
   Please check the <instance ID>
   ```

2. After the diagnostic task runs, the model outputs the diagnostic conclusion for the instance in the session, typically including:

   * Basic instance information (status, specification, region, network).

   * Pass or abnormal status of key checks such as network connectivity and security group/route configuration.

   * If exceptions are found, possible causes and next\-step suggestions are provided.
