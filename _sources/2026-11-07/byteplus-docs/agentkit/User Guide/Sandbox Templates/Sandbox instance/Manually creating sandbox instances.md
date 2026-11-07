---
title: "Manually creating sandbox instances"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Creating_tool_instances"
---

When you want to launch a fully functional runtime environment based on a sandbox template, you can create an AgentKit sandbox instance. This initializes a session instance for the sandbox template that tracks state and preserves context, enabling coherent multi\-turn operations. This topic describes how to create an AgentKit sandbox instance.

> **warning**

* > **Method description**: This topic describes how to manually create a sandbox instance in the console. If your agent is integrated with a sandbox template, a sandbox instance will be automatically created and started when the sandbox is used to process tasks.

* > **Billing notes**: After a sandbox instance is created, the system charges CPU and memory fees based on the actual running duration of the instance. Fees continue to accrue while the instance is running. If public outbound traffic is also generated, additional public traffic fees are charged. For more information about billing rules, see [**Billing instructions**](https://docs.byteplus.com/en/docs/agentkit/Billing_items?lang=en#bXVZPstX).

## Prerequisites

[A sandbox template has been created](https://docs.byteplus.com/en/docs/agentkit/Creating_tools).

## Limits

The maximum concurrency for a single sandbox instance is **5**. To increase the quota, submit a request in [Quota Center](https://console.byteplus.com/quota/productList/ParameterList?ProviderCode=ecs).

## Procedure

### Creating sandbox instances

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Sandbox Templates".

3. In the "Sandbox templates" list, click the name of the target template.

4. Click the "Instance management" tab and select "AgentKit instance". Then, click "Create instance".

5. In the pop\-up dialog box, specify the "**Execution duration" and "Session information" parameters, add a TOS mount point (optional), and add an EFS mount point (optional).**

   |Parameter |Description |
   |---|---|
   |Execution duration |The lifecycle of a sandbox instance.<br><br><br>* Value range: 60 seconds to 86400 seconds (24 hours).<br><br>* Default value: 3600 seconds.<br><br><br>> **warning**<br><br><br>> The sandbox instance lifecycle refers to the lifetime of a sandbox instance from creation to automatic destruction. **During this period, fees are continuously charged based on the configuration of the sandbox instance.**For details, see [**Billing instructions**](https://docs.byteplus.com/en/docs/agentkit/Billing_items?lang=en#bXVZPstX).<br> |
   |Session information |User session information. |
   |TOS mount (optional) |Add a TOS mount point to the sandbox instance as a configuration entry for accessing TOS.<br><br><br>* **Sandbox template status**<br><br>   * **TOS mounting enabled for sandbox template**<br><br>      No additional configuration is required. The storage configuration of the tool is automatically inherited when you create an instance. To specify a bucket subdirectory separately, click "Add TOS mount point", select a local directory, and configure the bucket subdirectory.<br><br>   * **TOS mounting not enabled for sandbox template**<br><br>      * To mount TOS, first [enable TOS mounting](https://docs.byteplus.com/en/docs/agentkit/Update_storage_configuration) for the tool, and then add a TOS mount point when creating an instance.<br><br>* **Configuration parameters**<br><br>   * **Local directory**: Specify the local directory in the sandbox template instance where the storage is to be mounted (such as `/home/app`). You can select only a local directory configured in the sandbox template.<br><br>   * **Bucket**: The value is fixed to an existing bucket in the local directory.<br><br>   * **Bucket subdirectory**: Specify the subdirectory of the bucket (for example, `tmp/abc`). If this parameter is not specified or the specified subdirectory does not exist, the system automatically creates it. |
   |EFS mount (optional) |Add an EFS mount point to the sandbox instance as a configuration entry for the sandbox instance to access [EFS](https://docs.byteplus.com/en/docs/nas/What_is_Elastic_File_Storage?lang=en).<br><br><br>* **Configuration parameters**:<br><br>   * **File space name**: A unique identifier for the persistent storage space. We recommend using a meaningful and easily recognizable name, such as `shentang-shared` and `user-a-workspace`.<br><br>   * **Local mount path**: Specify the mount path in the sandbox (such as `/home/data`) and read\-write permissions.<br><br>* **Feature characteristics**<br><br>   * **Persistence**: Data is saved independently of the sandbox instance lifecycle. Data is not lost after the instance is destroyed or recreated.<br><br>   * **Sharing**: Multiple sandbox instances mount the same file system and can concurrently read and write the same data.<br><br>   * **Standard file semantics**: POSIX\-compatible, supporting random read/write, directory structures, and file permissions. Existing code does not need changes.<br><br>   * **User\-level isolation**: You can use independent file systems or access points (subdirectories and permissions) to create storage spaces that are isolated from one another for different users. |

6. Click "Confirm". After the instance is created, you can view its information on the "Instance management" tab.

   After the instance is created, you can click "Terminal" to enter the Web Terminal page to view instance runtime logs, command execution output, program status, test information, and business\-related real\-time data.

### Manually test the sandbox instance

1. On the sandbox template details page in the console, click the **Instance management** tab and find the target instance in the instance list.

   * **WebChat address**: Click the WebChat address link. On the sandbox page that appears, perform testing as needed.

   * **Address for public network access**: Click the copy icon in the **Address for public network access** column to copy the public access address of the instance. Enter the copied public access address in the browser address bar to access it.

2. (Optional) Supported only for Code Sandbox and AIO Sandbox instances.

   Select the required sandbox type in the top area. After selection, the corresponding panel will be displayed on the page. Test it as needed.

   > **tip**

   * > Sandbox types supported by Code Sandbox instances: Terminal, OpenCode, Codex, DSH (DeepSeek Harness), VNC,  and Browser.

   * > Sandbox types supported by AIO Sandbox instances: Terminal, OpenCode, VNC, Browser, and Codex.
