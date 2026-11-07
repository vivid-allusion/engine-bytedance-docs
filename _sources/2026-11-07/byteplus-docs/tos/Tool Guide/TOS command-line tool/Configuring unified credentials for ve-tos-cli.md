---
title: "Configuring unified credentials for ve-tos-cli"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Configuring_unified_credentials_for_ve-tos-cli"
---

This topic explains how to configure unified access credentials for `ve-tos-cli`. `ve-tos-cli` allows you to access TOS with unified credentials managed by `ve`. Once configured, there is no need to configure the access key ID and secret access key separately in `ve-tos-cli`. This method is useful for sharing unified credentials across multiple tools, avoiding the use of hardcoded access keys in automated tasks, and centrally managing access credentials across environments.

<span id="da329271"></span>
## Prerequisites


* You have installed the `ve` tool.

* You have installed the `ve-tos-cli` tool. For instructions, see [Installation](https://docs.byteplus.com/en/docs/tos/Quick_start_with_ve-tos-cli).


<span id="09b3521f"></span>
## Notes


* The credentials obtained by `ve login` are temporary. Run `ve login` again after the credentials expire.

* After logging in with a `non-default profile`, run `ve configure profile --profile <profile-name>` to switch profiles. Alternatively, you can specify `--profile` when calling `ve-tos-cli`.

* In unified authentication mode, `ve-tos-cli` ignores the access key ID and secret access key in its local configuration. These local credentials are not used as fallback credentials either.

* Do not commit local credential configuration files to code repositories. Do not print credential content in logs or scripts.

* Before running automation tasks, we recommend running `ve sts GetCallerIdentity` and `ve-tos-cli ls` to confirm the login status and access permissions are normal.


<span id="2aff26d4"></span>
## Configuration workflow


1. Run `ve login` to log in to your BytePlus account and save temporary credentials locally.

2. Run `ve-tos-cli config set auth_mode unified` to set `ve-tos-cli` authentication mode to unified.

3. Run `ve-tos-cli` commands to verify that the configuration has taken effect.


<span id="a9289e47"></span>
## Step 1: Generate temporary credentials


1. Run `ve login` to log in to your account using the default `profile`.

   `ve login` uses OAuth 2.0 device authorization. After running the command, the terminal displays a login URL and user code and attempts to open a browser automatically.

2. After completing authorization in the browser, `ve` saves the temporary credentials locally. The authentication information is written to the `~/.volcengine/config.json` file by default.

   If the current device cannot open a browser — such as a remote server or a container without a GUI — run `ve login --no-browser`. Then, open the login URL displayed in the terminal on another device. Enter the user code and authorize. Do not terminate the current command while authorizing, as `ve` continuously polls for the login result.

3. To specify a `profile` and region, run `ve login --profile dev --region cn-beijing`.

   Replace `cn-beijing` with the region you need. For a list of regions supported by the `--region` parameter, see [Regions and endpoints](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint).

4. After logging in with a `non-default profile`, run `ve configure profile --profile dev` to switch profiles.

5. After logging in, run `ve sts GetCallerIdentity` to verify the login identity.


<span id="40622ccc"></span>
## Step 2: Enable unified authentication mode


1. Run `ve-tos-cli config set auth_mode unified` to set `ve-tos-cli` authentication mode to unified.

   Once the configuration is complete, `ve-tos-cli` will use the unified credentials managed by `ve`. You will no longer need to provide an access key ID and a secret access key separately.

2. Run `ve-tos-cli config show --output json` to view the current configuration.

   Confirm that `auth_mode` in the output is `unified`.


<span id="e29fd350"></span>
## Step 3: Verify access to TOS


1. Run `ve-tos-cli ls` to list TOS resources.

2. Run `ve-tos-cli ls tos://<bucket-name>/<prefix>/` to list objects in a specific bucket or directory.

   Replace `<bucket-name>` with the actual bucket name and `<prefix>` with the target directory. If you do not need to specify a directory, you can omit the `<prefix>/` part.

3. Run `ve-tos-cli ls tos://<bucket-name>/<prefix>/ --output table` to display results in a table format.


If the command returns a normal result, then `ve-tos-cli` has successfully accessed TOS using unified credentials.

<span id="97d95455"></span>
## Configuration example


* Using the default `profile`:

   ```Shell
   # Log in and save temporary identity credentials locally
   ve login 
    
   # Configure ve-tos-cli to use unified credentials
   ve-tos-cli config set auth_mode unified 
    
   # Verify the ve login identity
   ve sts GetCallerIdentity 
    
   # Verify access to TOS
   ve-tos-cli ls 
   ```
   



&nbsp;

* Using a custom `profile`:

   ```Shell
   # Log in by using the specified profile
   ve login --profile dev --region cn-beijing 
    
   # Set this profile as the current profile
   ve configure profile --profile dev 
    
   # Configure ve-tos-cli to use unified credentials
   ve-tos-cli config set auth_mode unified 
    
   # Access TOS by using the same profile
   ve-tos-cli --profile dev ls 
   ```
   


In unified authentication mode, use the same `profile` for `ve` and `ve-tos-cli`. Otherwise, `ve-tos-cli` may fail to detect the correct login state.

The configuration items are explained below.


|Configuration item |Description |
|---|---|
|ve login |Authorizes a login using the console device code and saves the temporary credentials locally. |
|\-\-profile |Specifies the `profile` for logging in or making calls. The default value is `default`. |
|\-\-region |Specifies the region for login and resource access. |
|\-\-no\-browser |Prevents the browser from opening automatically. It is ideal for remote servers and containers. |
|auth_mode unified |Specifies that `ve-tos-cli` uses the unified credentials managed by `ve`. |
|ve sts GetCallerIdentity |Returns the current login identity to verify whether the `ve` credentials are valid. |
|ve\-tos\-cli config show |Returns the current configuration of `ve-tos-cli`. |


<span id="e600df48"></span>
## FAQ


* `ve-tos-cli` reports that no credentials are found.

   Run the following commands in sequence:

   ```Shell
   ve login 
   ve sts GetCallerIdentity 
   ve-tos-cli config set auth_mode unified 
   ve-tos-cli config show --output json 
   ```
   

   Confirm that you have logged in to your account with`ve` and set `auth_mode` to `unified`.

* You cannot access TOS after using a custom `profile`.

   Confirm that you are using the same `profile` for `ve` and `ve-tos-cli`.

   ```Shell
   ve configure profile --profile dev 
   ve-tos-cli --profile dev ls 
   ```
   

* The browser will not open automatically.

   Run the following command:

   ```Shell
   ve login --no-browser 
   ```
   

   On another device that can access a browser, open the URL displayed in the terminal, enter the user code, and complete authorization.

* How do I log out?

   ```Shell
   # Log out of the default profile
   ve logout 
   # Log out of the specified profile
   ve logout --profile dev 
   # Log out of all login states created by ve login
   ve logout --all 
   ```
   

   After logging out, you will no longer be able to access TOS with `ve-tos-cli` in unified authentication mode. To restore access, run `ve login` again.
