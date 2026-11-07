---
title: "FAQ"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/CLI_FAQ"
---

## Configuration file not found

* **Issue:**

   ```Bash
   Error: Configuration file not found: agentkit.yaml
   ```

* **Cause**: No configuration file exists in the current directory.

* **Solution:**

   ```Bash
   # If it is a new project
   agentkit init my_agent
   
   # If it is an existing project
   agentkit config
   ```

## Docker not running (Local mode)

* **Issue**

   ```Bash
   Error: Docker daemon not running
   ```

* **Cause**: The Docker service is not started.

* **Solution**:

   * Windows/macOS: Open Docker Desktop.

   * Linux: `sudo systemctl start docker`.

## Cloud credentials not configured (Cloud mode)

* **Issue:**

   ```Bash
   Error: BYTEPLUS_ACCESSKEY or BYTEPLUS_SECRETKEY not set
   ```

* **Cause**: The BytePlus AK/SK credentials are not configured.

* **Solution**:

   ```Bash
   # Recommended: Use secure global configuration.
   agentkit config --global --init
   agentkit config --global --set byteplus.access_key="your_access_key"
   agentkit config --global --set byteplus.secret_key="your_secret_key"
    
   # Alternative: Temporary environment variables (for development and testing only)
   export BYTEPLUS_ACCESSKEY="Your AccessKey"
   export BYTEPLUS_SECRETKEY="Your SecretKey"
   ```

## Build failure

```Bash
Build failed: ...
```

**Possible causes and solutions**:

* **Dependency issue**: Check whether the requirements.txt file is correctly configured.

* **Code error:**  Check whether the Python code has syntax errors.

* **Network issue:**  Check network connectivity and retry the build.

* **Permission issue:**  Make sure that you have operation permissions for Docker and cloud services.

### Testing tips

1. View detailed logs.

   ```Bash
   # Set the detailed log level.
   export LOG_LEVEL=DEBUG
   agentkit build
   ```

2. Verify the configuration file.

   ```Bash
   # Check whether the configuration is correct.
   cat agentkit.yaml
   ```

3. Execute commands step by step.

   ```Bash
   # Execute the commands separately for easier troubleshooting.
   agentkit build # Build first.
   agentkit deploy # Then deploy.
   # Instead of using the combined launch command directly.
   ```

4. Check the running status.

   ```Bash
   # Check whether the agent is running as expected.
   agentkit status
   ```

## Invalid YAML format

* **Issue:**

   ```Bash
   Error: Invalid YAML format
   ```

* **Solution:**

   * Use spaces for indentation (do not use tabs).

   * Make sure that there is a space after each colon.

   * Enclose strings containing special characters in quotation marks.

   * Wrap template variables in double quotes: `""`.

## Required field missing

* **Issue:**

   ```Bash
   Error: agent_name is required
   ```

* **Solution:**

   ```Bash
   agentkit config  # Reconfigure and fill in required fields.
   ```

## Template variable rendering failure

* **Issue:**

   ```Bash
   Error: Config field 'cr_instance_name' template variables were not fully rendered
   ```

* **Possible causes:**

   * The BytePlus credentials are not configured.

   * The permissions for the configured AK/SK are insufficient.

* **Solution:**

   ```Bash
   # Check environment variables.
   echo $BYTEPLUS_ACCESSKEY
   echo $BYTEPLUS_SECRETKEY
   # Or check the global configuration.
   cat ~/.agentkit/config.yaml
   ```

## Environment variables not taking effect

* **Possible causes:**

   * Typo in the variable name.

   * Configuration changes are not saved.

   * The service is not redeployed after configuration updates.

   * Confusion between `common.runtime_envs` and policy\-level `runtime_envs`.

* **Solution:**

   ```Bash
   # 1. Check the configuration.
   cat agentkit.yaml
   
   # 2. Confirm the environment variables are placed in the correct location.
   # common.runtime_envs - shared by all modes
   # launch_types.<mode>.runtime_envs - dedicated for this mode
   
   # 3. Redeploy the service.
   agentkit deploy
   ```
