---
title: "Enable or update security protection for existing ArkClaw instances"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Enable_or_update_security_protection_for_existing_ArkClaw_instances"
---

After the ClawSentry service is activated in the security management module, newly created ArkClaw Enterprise Edition instances will automatically have security protection enabled. To enable security protection (ClawSentry) for existing ArkClaw Enterprise Edition instances, or to upgrade the ClawSentry version installed on ArkClaw instances to the latest version, refer to the instructions in this document.

This procedure applies to ArkClaw Enterprise Edition instances in the following scenarios:

* ArkClaw Enterprise Edition instances created before ClawSentry service activation—in other words, instances that have never had the protection plugin installed.

* ArkClaw Enterprise Edition instances created after ClawSentry service activation, but need to be upgraded to the latest protection version.

* ArkClaw Enterprise Edition instances created after ClawSentry service activation that had the plugin manually uninstalled and need to be reinstalled.

## Notes

* **If the security plugin is offline, the upgrade may not succeed.**

* The latest ClawSentry plugin version for BytePlus is **1.4.0**.

* Version compatibility: Compatible with BytePlus ArkClaw versions 1.1.0, 1.1.1, or 1.1.2.

## Prerequisites

* The administrator has activated the ClawSentry service in the ArkClaw Enterprise Edition console. For details, please refer to [Enable security protection](https://docs.byteplus.com/en/docs/ArkClaw/Enable_security_protection).

* The employee has created an ArkClaw instance.

* The account performing the upgrade operation must have the following permissions.

   * **ArkClawFullAccess**: Required for read and write access to ArkClaw Enterprise Edition

   * **ClawSentryFullAccess**: Required for read and write access to ClawSentry

## Procedure

1. Log in to the [ArkClaw Enterprise Edition console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left menu bar, select **O&M and Security \> O&M \> Batch O&M**, and click **Create Job**.

3. Configure job\-related information.

   1. Enter the job name.

   2. Paste the modified [code sample](https://docs.byteplus.com/en/docs/ArkClaw/Enable_or_update_security_protection_for_existing_ArkClaw_instances#tluZ17qW) below the system preset command  **(starting from line 10), and make sure to retain the original command**.

> **warning**

> The system preset Shell content cannot be modified; please start input from line 10.

   3. Click **Add** to select the execution target.

4. Select the target execution object, then click Confirm.

> **warning**

> **If the security plugin is offline, the upgrade may not succeed.**

After creation, the created job will appear in the job list.

5. Once the status is "Successful", go to the security management list to check the upgraded Claw instance version.

> **tip**

> If the version number is 1.4.0, it indicates that the upgrade to the latest version has been completed.

## Code example

The following code is used to execute related commands in batch O&M jobs. Copy the code and replace the corresponding parameter values before use. For information on how to obtain parameters, see [Parameter description](https://docs.byteplus.com/en/docs/ArkClaw/Enable_or_update_security_protection_for_existing_ArkClaw_instances#hrigcCHf).

> **warning**

> Caution: Replace the parameter values in the code (lines 6 to 12).

```Bash
# ========================================
# Enter the configuration values below. Required parameters must be set.
# ========================================

# BytePlus credentials
VOLC_ACCESS_KEY_ID="YOUR_VOLC_ACCESS_KEY_ID"   # Required: BytePlus Access Key
VOLC_SECRET_KEY="YOUR_VOLC_SECRET_KEY"         # Required: BytePlus Secret Key

# Claw configuration
SPACE_ID="csi-****"                            # ArkClaw space ID
REGION="cn-hongkong"                          # Region: cn-hongkong
CONFIG_FILE="/root/.openclaw/openclaw.json"  # OpenClaw configuration file path
TARGET_VERSION="1.9.1"                      # Target version

# Optional: Set these values to change the assistant name and owner displayed in Security Management. Leave them empty when upgrading multiple ArkClaw assistants to avoid overwriting their information.
NAME=""                           # Optional: Custom ArkClaw assistant name
USER_UID=""                       # Optional: Unique owner identifier (user email)

# Optional: Required when using temporary credentials
TOKEN=""                           # Optional: Temporary credential token

# ========================================

# Load environment variables from the OpenClaw environment file
ENV_FILE="/root/.openclaw/.env"
if [[ -f "${ENV_FILE}" ]]; then
    set -a
    source "${ENV_FILE}"
    set +a
fi
ARK_CLAW_ID="${CLAW_INSTANCE_ID:OTEL_SERVICE_NAME}"

# Debug information
echo "  ARK_CLAW_ID = '${ARK_CLAW_ID}'"
echo ""

# ========================================

set -euo pipefail
export HOME="${HOME:-/root}"

SCRIPT_DIR="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"

# Plugin names
PLUGIN_NAME="agent-sentry"
LEGACY_PLUGIN_NAME="claw-sentry"
OLD_PLUGIN_NAME="ai-assistant-security-openclaw"
EXTENSIONS_DIR="${HOME}/.openclaw/extensions"

# TOS download settings (default: cn-beijing)
CS_TOS_BASE_URL="https://claw-sentry.tos-cn-beijing.volces.com"
CS_TEMP_DIR="/tmp/agent-sentry"

# Go binary download settings (default: cn-beijing)
GO_BINARY_URL="https://clawsentry-arkclaw-update.tos-cn-beijing.volces.com/clawsentry${TARGET_VERSION}/initgo_arkclaw_online"
GO_BINARY_PATH="/tmp/initgo_arkclaw_online"

# Select download URLs based on the region
if [[ "$REGION" == "cn-hongkong" ]]; then
    echo "Using cn-hongkong region download addresses"
    CS_TOS_BASE_URL="https://claw-sentry-hongkong.tos-cn-hongkong.volces.com"
    GO_BINARY_URL="https://clawsentry-arkclaw-update-hongkong.tos-cn-hongkong.volces.com/clawsentry${TARGET_VERSION}/initgo_arkclaw_online"
else
    echo "Using cn-beijing region download addresses"
fi

echo "======================================="
echo "agent-sentry configure (with Go binary)"
echo "======================================="

echo ""
echo "[1/5] Checking dependencies..."

if ! command -v wget &>/dev/null; then
    echo "Error: wget not found"
    echo "Please install wget first"
    exit 1
fi

echo ""
echo "[2/5] Checking and removing old plugins..."

# Remove old plugin (ai-assistant-security-openclaw)
OLD_PLUGIN_DIR="${EXTENSIONS_DIR}/${OLD_PLUGIN_NAME}"
if [[ -d "$OLD_PLUGIN_DIR" ]]; then
    echo "Old plugin found: $OLD_PLUGIN_NAME, uninstalling..."
    if command -v openclaw &>/dev/null; then
        echo "y" | openclaw plugins uninstall "$OLD_PLUGIN_NAME" 2>/dev/null || true
    else
        echo "openclaw command not found, skipping uninstall"
    fi

    # Double-check and force delete if directory still exists
    if [[ -d "$OLD_PLUGIN_DIR" ]]; then
        echo "Directory $OLD_PLUGIN_DIR still exists, force deleting..."
        rm -rf "$OLD_PLUGIN_DIR"
    fi
fi

# Remove existing agent-sentry plugin (will be reinstalled)
NEW_PLUGIN_DIR="${EXTENSIONS_DIR}/${PLUGIN_NAME}"
if [[ -d "$NEW_PLUGIN_DIR" ]]; then
    echo "Existing $PLUGIN_NAME plugin found, removing..."
    if command -v openclaw &>/dev/null; then
        echo "y" | openclaw plugins uninstall "$PLUGIN_NAME" 2>/dev/null || true
    else
        echo "openclaw command not found, skipping uninstall"
    fi

    # Double-check and force delete if directory still exists
    if [[ -d "$NEW_PLUGIN_DIR" ]]; then
        echo "Directory $NEW_PLUGIN_DIR still exists, force deleting..."
        rm -rf "$NEW_PLUGIN_DIR"
    fi
fi

LEGACY_PLUGIN_DIR="${EXTENSIONS_DIR}/${LEGACY_PLUGIN_NAME}"
if [[ -d "$LEGACY_PLUGIN_DIR" ]]; then
    echo "Legacy plugin found: $LEGACY_PLUGIN_NAME, uninstalling..."
    if command -v openclaw &>/dev/null; then
        echo "y" | openclaw plugins uninstall "$LEGACY_PLUGIN_NAME" 2>/dev/null || true
    else
        echo "openclaw command not found, skipping uninstall"
    fi

    if [[ -d "$LEGACY_PLUGIN_DIR" ]]; then
        echo "Directory $LEGACY_PLUGIN_DIR still exists, force deleting..."
        rm -rf "$LEGACY_PLUGIN_DIR"
    fi
fi

echo ""
echo "[3/5] Downloading and installing agent-sentry from TOS..."

CS_TGZ_PATH="/tmp/agent-sentry-${TARGET_VERSION}.tgz"
echo "Downloading from: ${CS_TOS_BASE_URL}/agent-sentry-${TARGET_VERSION}.tgz"
if ! wget -q "${CS_TOS_BASE_URL}/agent-sentry-${TARGET_VERSION}.tgz" -O "$CS_TGZ_PATH"; then
    echo "Warning: Failed to download agent-sentry from TOS, will continue with Go binary"
else
    echo "Extracting to: ${CS_TEMP_DIR}"
    rm -rf "$CS_TEMP_DIR"
    mkdir -p "$CS_TEMP_DIR"
    if ! tar -xzf "$CS_TGZ_PATH" -C "$CS_TEMP_DIR"; then
        echo "Warning: Failed to extract agent-sentry, will continue with Go binary"
    else
        echo "Installing from local package..."
        INSTALL_DIR="${CS_TEMP_DIR}/package"
        if command -v openclaw &>/dev/null; then
            if ! openclaw plugins install "$INSTALL_DIR" 2>/dev/null; then
                echo "Warning: Failed to install agent-sentry, will continue with Go binary"
            else
                echo "agent-sentry installed successfully"
            fi
        else
            echo "openclaw command not found, skipping installation"
        fi
    fi

    echo "Cleaning up TOS download..."
    rm -f "$CS_TGZ_PATH"
    rm -rf "$CS_TEMP_DIR"
fi

echo ""
echo "[4/5] Downloading Go binary..."
echo "Downloading from: $GO_BINARY_URL"
if ! wget -q "$GO_BINARY_URL" -O "$GO_BINARY_PATH"; then
    echo "Error: Failed to download Go binary"
    exit 1
fi

# Make it executable
chmod +x "$GO_BINARY_PATH"

echo ""
echo "[5/5] Running Go binary..."

# Set environment variables
export VOLC_ACCESS_KEY_ID="$VOLC_ACCESS_KEY_ID"
export VOLC_SECRET_KEY="$VOLC_SECRET_KEY"

# Build command
CMD_ARGS=()
CMD_ARGS+=("-space_id" "$SPACE_ID")
CMD_ARGS+=("-ark_claw_id" "$ARK_CLAW_ID")
CMD_ARGS+=("-region" "$REGION")
CMD_ARGS+=("-config_file" "$CONFIG_FILE")

if [[ -n "$TOKEN" ]]; then
    CMD_ARGS+=("-token" "$TOKEN")
fi

if [[ -n "$NAME" ]]; then
    CMD_ARGS+=("-name" "$NAME")
fi

if [[ -n "$USER_UID" ]]; then
    CMD_ARGS+=("-user_uid" "$USER_UID")
fi

echo "Executing: $GO_BINARY_PATH ${CMD_ARGS[*]}"
if ! "$GO_BINARY_PATH" "${CMD_ARGS[@]}"; then
    rc=$?
    echo "Error: failed to execute: $GO_BINARY_PATH ${CMD_ARGS[*]} (exit_code=${rc})" >&2
    exit $rc
fi


echo ""
echo "Checking openclaw version and setting hooks..."
echo "======================================="
if command -v openclaw &>/dev/null; then
    # Get the OpenClaw version
    if version_output=$(openclaw --version 2>&1); then
        echo "Openclaw version command output: $version_output"
        # Parse the version number using a regular expression
        if [[ "$version_output" =~ OpenClaw[[:space:]]+([0-9]+)\.([0-9]+)\.([0-9]+) ]]; then
            year=${BASH_REMATCH[1]}
            month=${BASH_REMATCH[2]}
            patch=${BASH_REMATCH[3]}
            echo "Openclaw version $year.$month.$patch detected"

            # Check whether the version is 2026.4.27 or later
            should_set_hook=false
            if (( year > 2026 )); then
                should_set_hook=true
            elif (( year == 2026 )); then
                if (( month > 4 )); then
                    should_set_hook=true
                elif (( month == 4 )) && (( patch >= 27 )); then
                    should_set_hook=true
                fi
            fi

            if [ "$should_set_hook" = true ]; then
                echo "Setting allowConversationAccess hook..."
                openclaw config set plugins.entries.agent-sentry.hooks.allowConversationAccess true 2>/dev/null || echo "Warning: Failed to set hook configuration"
            else
                echo "Openclaw version $year.$month.$patch is older than 2026.4.27, skipping hook configuration"
            fi
        else
            echo "Could not parse openclaw version from: $version_output"
        fi
    else
        echo "Could not get openclaw version, skipping hook configuration"
    fi
else
    echo "openclaw command not found, skipping hook configuration"
fi


echo ""
echo "Cleaning up..."
echo "======================================="
rm -f "$GO_BINARY_PATH"

echo "Restarting OpenClaw gateway..."
if command -v openclaw &>/dev/null; then
    openclaw gateway restart
else
    echo "Warning: openclaw command not found, skipping gateway restart"
fi

echo ""
echo "Done!"
```

## Parameter description

Obtain the following parameters before calling the API to register the service.

|**Configuration item** |**Data type** |**Required** |**Description** |
|---|---|---|---|
|VOLC_SECRET_KEY |String |Yes |* The Secret Access Key and Access Key ID owned by the ClawSentry service account that has been enabled.<br><br>* **How to obtain**: <br><br>   1. Log in to the [IAM Console](https://console.byteplus.com/iam/keymanage).<br><br>   2. Create an access key or view your access key.<br><br><br>> **tip**<br><br><br><br>* > Use the Secret Access Key and Access Key ID corresponding to the primary account.<br><br><br>* > To configure a sub\-account, grant the **ClawSentryFullAccess** and **ArkClawFullAccess** permissions. For authorization instructions, see [How to grant permissions to a sub\-account](https://docs.byteplus.com/en/docs/ArkClaw/Enable_or_update_security_protection_for_existing_ArkClaw_instances#gmU7ipM0).<br> |
|VOLC_ACCESS_KEY_ID |String |Yes ||
|SPACE_ID |String |Yes |* Space ID of ArkClaw Enterprise Edition.<br><br>* **How to obtain**:<br><br>   1. Log in to the [ArkClaw Enterprise Edition Console](https://console.byteplus.com/arkclaw/enterprise/).<br><br>   2. Obtain the space ID in the Space Overview module, for example, csi\-\*\*\*\*. |
|REGION |String |No |* The region to which ArkClaw belongs. By now, only `cn-hongkong` is supported.<br><br>* **How to obtain**:<br><br>   1. Log in to the [ ArkClaw Enterprise Edition Console](https://console.byteplus.com/arkclaw/enterprise/).<br><br>   1. Check the region of the service in the top menu bar. |
|TARGET_VERSION |String |Yes |* The target version of AgentSentry. |
|CONFIG_FILE |String |No |* The path to the OpenClaw configuration file (openclaw.json), defaulting to `/root/.openclaw/openclaw.json`. If not specified, the default path is used.<br><br>* **How to obtain the path**: You can obtain the detailed path directly from the AI assistant, or use the command `find / -name openclaw.json` in the terminal to search for it. |
|NAME |String |No |* Leave blank.<br><br>* To modify the name displayed for a single assistant in the Security Management module, you can configure this parameter.<br><br>* Do not configure this parameter when upgrading multiple ArkClaw assistants in bulk, or it will overwrite the name information of multiple assistants. |
|USER_UID |String |No |* Leave blank.<br><br>* To modify the unique identifier of the user associated with a single assistant in the Security Management module, you can configure this parameter.<br><br>* Do not configure this parameter when upgrading multiple ArkClaw assistants in bulk, or it will overwrite the user information of multiple assistants. |

## Frequently asked questions

### How to confirm the version of ArkClaw?

Different versions of ArkClaw correspond to different versions of the OpenClaw framework. To check, follow these steps:

1. Log in to the [ArkClaw Enterprise Edition Console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select **Instance list**.

3. In the **Instance list**, view the **Current version** corresponding to the ArkClaw instance.

### How to grant permissions to a sub\-account?

#### Batch grant the same permission to multiple sub\-accounts

1. Log in to the [IAM Console](https://console.byteplus.com/iam/identitymanage/user) using the primary account.

2. In the left navigation pane, select **Permission policies**.

3. Enter the corresponding permission name in the search box and press Enter.

   * **ArkClawFullAccess**: Used to obtain read and write permissions for ArkClaw Enterprise Edition

   * **ClawSentryFullAccess**: Used to obtain read and write permissions for ClawSentry

4. In the search results, click **Authorize** for the corresponding policy.

5. Select the sub\-account users to be authorized.

6. After confirmation, click **Submit**.

After authorization, the AK and SK of the sub\-account can be used for O&M operations.

#### Batch grant multiple permissions to the same sub\-account

1. Log in to the [IAM Console](https://console.byteplus.com/iam/identitymanage/user) using the primary account.

2. In the left navigation pane, select **Users**.

3. Enter the corresponding user name in the search box and press Enter.

4. In the search results, click **Add permission** for the corresponding user.

5. Search for the following permission names separately and select them.

   * **ArkClawFullAccess**: Used to obtain read and write permissions for ArkClaw Enterprise Edition

   * **ClawSentryFullAccess**: Used to obtain read and write permissions for ClawSentry

6. After confirmation, click **Submit**.

After authorization, the AK and SK of the sub\-account can be used for O&M operations.

### The O&M job was executed successfully, but why was the assistant version not updated?

* Reason: It may be because the account used to perform the upgrade does not have the required permissions.

* Troubleshooting:

   1. Click the execution result corresponding to the job.

   2. Click to view the log.

   3. Check the error message for the failure.

   If the message 'User is not authorized to perform: arkclaw:GetClawInstance on resource:' appears, it indicates that the account lacks the **ArkClawFullAccess permission.**

* Solution: Refer to How to grant permissions to a sub\-account to add the **ArkClawFullAccess** permission to the account.
