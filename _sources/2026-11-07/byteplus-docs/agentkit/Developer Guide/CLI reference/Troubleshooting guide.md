---
title: "Troubleshooting guide"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Troubleshooting_guide"
---

|Category |Issue |
|---|---|
|Installation issues |* [agentkit command not found](https://docs.byteplus.com/en/docs/347/89577#2yebbAsZ)<br><br>* [Dependency conflicts](https://docs.byteplus.com/en/docs/347/89577#tUML9Yau) |
|Configuration issues |* [Environment variables not taking effect](https://docs.byteplus.com/en/docs/347/89577#VCJp3CPo)<br><br>* [Configuration file format error](https://docs.byteplus.com/en/docs/347/89577#z7qXrWec) |
|Deployment issues |* [CR creation failure](https://docs.byteplus.com/en/docs/347/89577#6Yl7zSzC)<br><br>* [Image build failure](https://docs.byteplus.com/en/docs/347/89577#SFE5VGAK)<br><br>* [Runtime deployment timeout](https://docs.byteplus.com/en/docs/347/89577#CWrbyUB8)<br><br>* [Abnormal runtime status](https://docs.byteplus.com/en/docs/347/89577#g9pzM24L) |
|Call issues |* [Invoke call failure](https://docs.byteplus.com/en/docs/347/89577#DwslXj4Q)<br><br>* [Model call failure](https://docs.byteplus.com/en/docs/347/89577#Q2PY7WSB) |
|Permission issues |* [AK/SK authentication failure](https://docs.byteplus.com/en/docs/347/89577#c6glE1T3)<br><br>* [Resource access denied](https://docs.byteplus.com/en/docs/347/89577#EkYiMced) |
|Log issues |* [Log file not created](https://docs.byteplus.com/en/docs/347/89577#M56NQihT)<br><br>* [No log output in the console](https://docs.byteplus.com/en/docs/347/89577#KLHHyjsM)<br><br>* [Too many or too few logs](https://docs.byteplus.com/en/docs/347/89577#40Vn8jMK) |

> **tip**

> If the following solutions fail to resolve your AgentKit issues, you can contact us via [GitHub Issues](https://github.com/volcengine/agentkit-sdk-python/issues) or BytePlus technical support. Provide the following information:

* > Detailed error messages and logs.

* > Clear steps to reproduce the issue.

* > Relevant configuration files (caution: mask sensitive information).

## agentkit command not found

* **Symptom**: When you execute the `agentkit` command in the terminal, the system prompts `command not found`.

* **Cause**: The path of the executable file installed by `pip` has not been added to the `PATH` environment variable of the system.

* **Solution**:

   * Verify the installation path: Execute `pip show agentkit-sdk-python` or `uv pip show agentkit-sdk-python` to locate the installation path indicated by the `Location` field.

   * Locate the executable file: In the `bin` directory under the installation path (for example, `.../site-packages/bin`), you can find the `agentkit` executable file.

   * Add to `PATH`: Add the absolute path of this `bin` directory to `~/.bashrc`, `~/.zshrc`, or another Shell configuration file.

      ```Bash
      export PATH="/path/to/your/python/bin:$PATH"
      ```

   * Reload the configuration: Execute `source ~/.bashrc` or restart the terminal to apply the changes.

## Dependency conflicts

* **Symptom**: When you install `agentkit-sdk-python`, `pip` reports a dependency version conflict.

* **Cause**: Your Python environment may have existing library versions incompatible with AgentKit.

* **Solution**:

   * Use a virtual environment (recommended): We recommend that you use `uv` or `venv` to create a clean virtual environment in your project to avoid conflicts with the system\-level Python package.

      ```Bash
      uv venv
      source .venv/bin/activate
      uv pip install agentkit-sdk-python
      ```

   * Clean up the environment and reinstall: If you have to use the existing environment, uninstall the package first and then reinstall it:

      ```Bash
      pip uninstall agentkit-sdk-python
      pip install agentkit-sdk-python
      ```

## Environment variables not taking effect

* **Symptom**: A prompt indicates a failure to connect to AgentKit or an authentication failure.

* **Cause**: Required environment variables are not set or incorrect environment variable names are used.

* **Solution**:

   * Make sure that the required environment variables have been set.

      ```Bash
      echo $BYTEPLUS_ACCESS_KEY
      echo $BYTEPLUS_SECRET_KEY
      ```

   * Make sure there are no extra spaces or quotation marks.

   * Re\-run `export` to set the environment variables in the current Shell session.

## Configuration file format error

* **Symptom**: When you execute `agentkit launch`, a prompt indicates that configuration file parsing failed.

* **Cause**: Incorrect file format.

* **Solution**:

   * Check whether the `agentkit.yaml` file format is correct (caution: check indentation).

   * Re\-execute `agentkit config` to regenerate the configuration file.

## CR creation failure

* **Symptom**:

   ```Plain Text
   CreateRegistry: QuotaExceeded.Registry The quota of Registry is exceeded.
   ```

* **Cause**: The account quota is insufficient.

* **Solution**:

   * The number of CR instances exceeds the quota limit.

   * Configure an existing CR instance name in `agentkit config`.

   * Or contact the administrator to increase the quota.

## Image build failure

* **Symptom**: Pipeline build fails with dependency installation errors.

* **Cause**: Dependency installation fails.

* **Solution**:

   * Check whether the dependencies in `requirements.txt` are correct.

   * Confirm that the dependency versions are compatible with Python 3.12.

   * View the Pipeline logs for detailed error information (Logs are automatically downloaded to your local root directory. You can check the prompt on the interactive interface and find a log file named like `pipeline_failed_****ff20ce223.log` in the root directory).

## Runtime deployment timeout

* **Symptom**: The runtime remains in the `Releasing` state for a long time.

* **Cause**: The first deployment takes a long time, or resources may be insufficient.

* **Solution**:

   * The first deployment usually takes 2\-3 minutes. Wait patiently.

   * Use `agentkit status` to check the status.

   * If it is not ready after more than 5 minutes, insufficient resources may be the cause. Try executing `agentkit destroy` and redeploy.

## Abnormal runtime status

* **Symptom**: The runtime status is `Failed` or `Error`.

* **Cause**: An internal exception of the runtime occurs.

* **Solution**:

   * Check whether the environment variable configuration is correct (especially the model API Key).

   * View the logs in the AgentKit console.

   * Confirm that there are no startup errors in the application code.

   * Try cleaning up with `agentkit destroy` and redeploying.

## Invoke call failure

* **Symptom**: When you execute `agentkit invoke`, a prompt indicates connection failure or timeout.

* **Cause**: Network issues or an endpoint configuration error occurs.

* **Solution**:

   * Use `agentkit status` to confirm that the runtime status is `Ready`.

   * Check the network connection.

   * Confirm that the Endpoint address is correct.

   * Check firewall or proxy settings.

## Model call failure

* **Symptom**: The agent returns an error indicating a model access failure.

* **Cause**: The model API Key configuration is incorrect, or the model quota is exhausted.

* **Solution**:

   * Check whether the ModelArk API Key configuration is correct.

   * Check whether the endpoint ID is valid.

   * Check whether the model quota is exhausted.

   * Log in to the ModelArk platform to check API Key permissions.

## AK/SK authentication failure

* **Symptom**: A prompt indicates `InvalidAccessKeyId` or `SignatureDoesNotMatch`.

* **Cause**: The AK/SK configuration is incorrect, or the permissions are insufficient.

* **Solution**:

   * Confirm that the AK/SK is correct and valid.

   * Check whether permission to access the AgentKit service is granted.

   * Confirm that the AK/SK has not been disabled or expired.

   * Contact the administrator to assign relevant permissions.

## Resource access denied

* **Symptom**: A prompt indicates `AccessDenied` or insufficient permission.

* **Cause**: The account does not have sufficient permissions to perform the operation.

* **Solution**:

   * Confirm that the account has operation permissions for the corresponding resources.

   * Check the IAM role configuration.

   * Contact the administrator to grant the necessary permissions.

## Log file not created

**Possible causes**:

* File logging is disabled.

* Insufficient directory permissions.

**Solution**:

```Bash
# 1. Check whether file logging is disabled.
echo $AGENTKIT_FILE_ENABLED  # Should be true or empty.

# 2. Check directory permissions.
ls -la .agentkit/logs/

# 3. Manually create the directory.
mkdir -p .agentkit/logs

# 4. Ensure environment variables are correct.
unset AGENTKIT_FILE_ENABLED  # Reset to default.
```

## No log output in the console

**Possible causes**:

* Console logging is disabled by default.

* The log level is set too high.

**Solution**:

```Bash
# 1. Enable console logging.
export AGENTKIT_LOG_CONSOLE=true

# 2. Set an appropriate log level.
export AGENTKIT_CONSOLE_LOG_LEVEL=INFO

# 3. Execute the command.
agentkit status
```

## Too many or too few logs

**Adjust the log level**:

```Bash
# Too many logs - view only important information.
export AGENTKIT_LOG_LEVEL=WARNING

# Too few logs - view detailed information.
export AGENTKIT_LOG_LEVEL=DEBUG
```
