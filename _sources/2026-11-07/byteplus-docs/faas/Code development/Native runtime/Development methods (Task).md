---
title: "Development methods (Task)"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Native_runtime_Development_methods_Task"
---

**Task** in the function Service specifically refers to a one\-off script Task executed based on **non\-WebServer mode** in response to requests asynchronously. This document introduces the standards and methods that need to be followed when developing tasks.

<span id="service-standards"></span>
## Service standards

When developing a task, the following standards must be adhered to:


* **Startup command**

   The task is executed by default through the startup command in **function configuration**, and allows for a custom startup command when submitting the task.

   * Once local development is completed, configure the default startup command when [Create tasks](https://docs.byteplus.com/en/docs/faas/Creating_tasks) in the console.

   * After the service discovery is successfully released, the custom startup command is supported when [Submit task](https://docs.byteplus.com/en/docs/faas/Submit_task).

   * If the startup process is complex, it is recommended to provide a startup script in the project.

* **Listening port**

   The task runs in a non\-WebServer mode, therefore it doesn't need to listen on any ports within the Service; you only need to specify the command or script that the task should execute through the start command.

* **Database/Storage mount**

   The function Service itself is stateless, not relying on local memory cache or disk data to start. If state is required, it can be stored in a remote Redis or MySQL database, or mount remote storage like NAS or TOS (For details, refer to [Mount FileNAS](https://docs.byteplus.com/en/docs/faas/Mount_FileNAS), [Mount TOS](https://docs.byteplus.com/en/docs/faas/Mount_TOS)).

* **Disk Limit**

   The maximum writable temporary storage space (in the `/tmp` directory) for a Task Instance is 512 MiB. Exceeding this limit may trigger instance eviction. Please take care to limit usage size, or implement your own file cleanup or rotation logic.


<span id="task-script-example"></span>
## Task script example

For complex tasks, you can provide a start script in the project, and then specify this start script when setting the start command later. Here is a simple example of a task script:

```bash
#!/bin/bash # Specify the script to use the bash interpreter (users can specify as needed)

# Set strict error handling options (users can specify as needed):
# -E: Enable ERR trap in functions and sub-shells
# -e: Exit the script when a command returns a non-zero status
# -u: Treat usage of undefined variables as errors
-o pipefail: If any command in the pipeline fails, the whole pipeline returns a non-zero status.
set -Eeuo pipefail

Change the working directory to the directory where the current script is located
cd "$(dirname"$0")"

# log print task start time
echo "Script started at $(date)"

# Print the contents of the current directory
ls

# Simulate a simple task: sleep for 10 seconds
echo "Simulating task: Sleeping for 10 seconds"
sleep 10

# Log printing task end time
echo "Script done at $(date)"
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The start script must have the corresponding executable permission. Otherwise, the task will fail with an <strong>permission denied</strong> error. Refer to the following command to add execute permission for the script to all user groups on Linux systems.</div>


```shell
# Execute this command when you need to package the code locally or create a custom image (The default template provided by the function Service has the executable permission already added to the run.sh script, no extra action needed by the user)
# Assuming the startup script is run.sh
chmod a+x run.sh
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When deploying using a custom image, ensure that the provided image has the corresponding Shell built\-in. Deployment using code packages can be ignored, as the image provided by the Serverless platform by default contains sh and bash shell interpreters.</div>


```shell
# Execute the following command in a custom image container to view the shells supported by the current system:
cat /etc/shells

# After executing the above command, the terminal will display content similar to the following, which is the list of shells available in your image:
/bin/sh
/bin/bash
/bin/rbash
/bin/dash
```
