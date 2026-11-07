---
title: "Obtain and configure the API Key"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Obtain_and_configure_the_API_Key"
---

Before invoking LAS operators, you must first generate an API Key for operator authentication. Because API Key information is sensitive, leaking your API Key may result in your model usage being consumed by others, causing losses. Therefore, after obtaining the API Key, it is recommended to store the API Key in an environment variable to facilitate safe and proper usage of the API Key.

# Create and obtain the API Key

After logging in to the [LAS console](https://console.byteplus.com/las/region:las+ap-southeast-1/next/home), go to **Operator service \> API key management** and click **Create API key** in the upper\-left corner. Create the API key according to the on\-screen instructions.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bbe482d73a0c4e2facce1d53d7fdf501~tplv-goo7wpa0wc-image.image)

> **警告**

* > Currently, LAS supports creating up to 20 API keys.

* > Please keep your API key information safe to prevent unauthorized disclosure.

# (Optional) Configure the API Key

When using the LAS development environment to invoke operators for data processing task development, it is recommended to configure the API Key in environment variables rather than hardcoding it in code. This prevents the API Key from being leaked with the code, which could result in your quota being used by others and incurring additional costs.

## Basic concepts

Environment variables are operating system\-level key\-value pairs used to store configuration information and can affect the behavior of running processes. They are divided into two categories:

* **Temporary variables**: Valid only within the terminal session in which they are created. They become invalid after the terminal is closed.

* **Permanent variables**: Persistently stored in system configuration files and remain valid in new terminal sessions or after system reboot.

Configuration overview examples for mainstream operating systems are as follows.

|Operating system |Shell |Temporary setting (current session) |Permanent setting (recommended file) |
|---|---|---|---|
|**macOS / Linux** |Bash / Zsh |`export LAS_API_KEY="value"` |`~/.zshenv` or `~/.bash_profile` |
||PowerShell |`$env:LAS_API_KEY = "value"` |`Microsoft.PowerShell_profile.ps1` |
|**Windows** |Command Prompt |`set LAS_API_KEY=value` |`setx LAS_API_KEY "value"` |
||PowerShell |`$env:LAS_API_KEY = "value"` |`[Environment]::SetEnvironmentVariable(...)` |

Detailed configuration guidance can be found below.

## macOS & Linux configuration instructions

In Unix\-like systems, environment variable configuration is closely related to the Shell you use.

### Understand Shell configuration files

* `~/.bash_profile`: Loaded when Bash login Shell starts. Typically used to define variables intended to be available throughout the entire user session.

* `~/.bashrc`: Loaded when Bash interactive non\-login Shell starts. Suitable for defining aliases and functions.

* `~/.zshenv`:  **(Recommended for environment variables)**  Loaded every time Zsh starts, regardless of whether it is a login or interactive Shell. This is the most reliable place to set environment variables.

* `~/.zprofile`: Loaded when Zsh login Shell starts, after `.zshenv`.

* `~/.zshrc`: Loaded when Zsh interactive Shell starts. Suitable for configuring Shell interaction\-related settings (such as prompts and aliases).

> **说明**

> To ensure that environment variables are available in all scenarios (including GUI applications), it is recommended to place the `export` statement in the `~/.zshenv` (Zsh) or `~/.bash_profile` (Bash) file.

### Bash / Zsh configuration

#### Temporary configuration

Run the `export` command in the terminal.

```Bash
# Example: Temporarily set LAS_API_KEY
export LAS_API_KEY="your-las-api-key-here"
```

#### Permanent configuration

1. Open the terminal and use the following command to check the default shell type.

   ```Bash
   echo $SHELL
   
   # Returns /bin/zsh: The default shell type is Zsh (Z shell).
   
   # Returns /bin/bash: The default shell type is Bash.
   ```

2. Open your shell configuration file. For Zsh users, `~/.zshenv` is recommended.

   ```Bash
   # Zsh users
   nano ~/.zshenv
   
   # Bash users
   nano ~/.bash_profile
   ```

3. Add an `export` statement at the end of the file.

   ```Bash
   # Set the LAS_API_KEY environment variable
   export LAS_API_KEY="your-las-api-key-here"
   ```

4. Save the file, then run the `source` command or restart the terminal to apply the configuration.

   ```Bash
   # Zsh users
   source ~/.zshrc
   
   # Bash users
   source ~/.bash_profile
   ```

### PowerShell (macOS / Linux)

The behavior of PowerShell is generally consistent across all platforms.

#### Temporary configuration

```Bash
$env:LAS_API_KEY = "your-las-api-key-here"
```

#### Permanent configuration

1. Edit the PowerShell profile file.

   ```Bash
   # This will automatically open the configuration file with the default editor
   code $profile
   ```

2. Add the following line to the file:

   ```Bash
   $env:LAS_API_KEY = "your-las-api-key-here"
   ```

3. Save the file, then run the `.` command or restart PowerShell.

   ```Bash
   . $profile
   ```

## Windows configuration instructions

Windows divides environment variables into "User variables" and "System variables". The former is only effective for the current user, while the latter applies to all users.

### Command Prompt (CMD)

#### Temporary configuration

Use the `set` command.

```Bash
set LAS_API_KEY=your-las-api-key-here
```

#### Permanent configuration

Use the `setx` command.

```Bash
:: Set user variables
setx LAS_API_KEY "your-las-api-key-here"

:: Set system variables (requires administrator privileges)
setx LAS_API_KEY "your-las-api-key-here" /m
```

**Caution**: Variables set by `setx` only take effect in **new** Command Prompt windows and do not affect the current window.

### PowerShell

#### Temporary configuration

```Bash
$env:LAS_API_KEY = "your-las-api-key-here"
```

#### Permanent configuration

Using the .NET API is the most reliable method.

```Bash
# Set user variable
[Environment]::SetEnvironmentVariable("LAS_API_KEY", "your-las-api-key-here", "User")

# Set system variable (requires administrator privileges)
[Environment]::SetEnvironmentVariable("LAS_API_KEY", "your-las-api-key-here", "Machine")
```

### Graphical user interface (GUI)

1. Search for "Edit system environment variables" in the Start menu and open it.

2. In the "System Properties" dialog box, click the "Environment Variables..." button.

3. In the pop\-up window, you can add or modify "User variables" for your user account in the upper section, or add or modify "System variables" for all users in the lower section.

4. Click "New..." and enter the variable name `LAS_API_KEY` and your key as the variable value.

5. Click "OK" at each level to close all dialog boxes.

## Verify the configuration

After completing the configuration, you can verify it in the following ways:

* **macOS / Linux**:

   ```Bash
   echo $LAS_API_KEY
   ```

* **Windows (CMD)** :

   ```Bash
   echo %LAS_API_KEY%
   ```

* **PowerShell (all platforms)** :

   ```Bash
   echo $env:LAS_API_KEY
   # Or
   Get-ChildItem env:LAS_API_KEY
   ```

For permanent configuration, be sure to **restart your terminal or IDE** and check again to ensure the configuration is loaded correctly.

## Advanced tips and practices

### Security: Protect your key

**Warning**: Never commit configuration files containing sensitive information such as `LAS_API_KEY` to Git or other version control systems.

* **Use**  **`.gitignore`**: Ensure that local configuration files containing sensitive information (such as `.envrc`, `.env`) are added to the `.gitignore` file.

* **Project\-level environment variables**: For specific projects, it is recommended to use the `.env` file to manage environment variables, and to load them at application startup using libraries such as `dotenv` (Node.js) and `python-dotenv` (Python).

### Directory\-level environment variables: `direnv`

`direnv` is a powerful tool that can automatically load or unload environment variables when entering or leaving a project directory.

1. **Installation** (using macOS Homebrew as an example):

   ```Bash
   brew install direnv
   ```

2. **Configuration**: Create a `.envrc` file in the root directory of the project.

   ```Bash
   # .envrc
   export LAS_API_KEY="your-project-specific-key"
   ```

3. **Authorization**: When entering the directory for the first time, run `direnv allow`. From then on, each time you enter the directory, the variables in `.envrc` will automatically take effect.
