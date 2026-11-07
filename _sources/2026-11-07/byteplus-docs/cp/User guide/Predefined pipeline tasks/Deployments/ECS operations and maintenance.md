---
title: "ECS operations and maintenance"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/ECS_operations_and_maintenance"
---

Code Pipeline provides **ECS** The **operations and maintenance** task supports batch deployment and operations and maintenance of BytePlus ECS instances through a pipeline.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The ECS instance has been purchased. For specific operations, refer to [Purchase method overview](https://docs.byteplus.com/en/docs/ecs/Overview-of-methods-for-buying-ECS-instances).

* The Operations Assistant has been installed on each ECS instance. For specific operations, refer to [Install the batch job client](https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client).


<span id=".5re75Yqg5Lu75Yqh"></span>
## Add task

When creating or editing a pipeline, go to the **Process Orchestration** tab, click **Add Job**, and the **Add Job** drawer will pop up. Task template selection **Deploy \>**  **ECS** **Operations and maintenance**.

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter description

The following describes the parameters of this preset task.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">ECS operations and maintenance tasks do not support adding other steps.</div>



|Configuration Item |Descriptions |
|---|---|
|Task name |Defaults to ECS operations and maintenance. Supports custom task names. |
|Upstream task |Display the name of the upstream serial task for the current task. Displayed as "none" when there is no upstream task.`-`.<br><br>Can be used together with [artifact upload](https://docs.byteplus.com/en/docs/cp/Artifact_upload) to enable the complete scenario of deploying ECS with upstream artifacts. |
|Artifact download |(Optional) Supports selecting artifacts built by an upstream **artifact upload** task. The artifacts will be downloaded to the file path specified in your configuration.<br><br><br>* Supports adding multiple artifacts as needed.<br><br>* Enter the artifact download path. The path must be an absolute file path. Example: `/home/app/foo`. |
|Region |Select the Region where the ECS instance is located. |
|ECS instances |Select ECS instances for batch operations; selecting multiple instances is supported.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">ECS instances must have Operations Assistant installed; otherwise, the task will fail.</div><br> |
|Execution path |Enter the command execution path. For Linux instances, the default is in the `/home` directory. |
|Execute user |You can specify that a command is executed by a user who exists in an instance. It is recommended to avoid using the root user to reduce security risks.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Please specify a user with permission to execute commands.</div><br> |
|Timeout duration |Set the timeout period for command execution on each instance. If execution exceeds the timeout, the batch job will determine that the task has failed on the corresponding instance. The default timeout is 1 minute. |
|Command type |Select the type of command to execute; currently, **Shell** and **Python** are supported. |
|Command content |Enter the script you want to run on the ECS instance.<br><br>Example: JRE configuration commands for initializing a JAVA ECS deployment environment.<br><br>```shell```<br>```#!/bin/bash```<br>``````<br>```# Check if Java has already been installed```<br>```if ! command -v java &> /dev/null```<br>```then```<br>```    echo "Java could not be found, installing OpenJDK..."```<br>```    # Update package list```<br>```    sudo apt update```<br>```# Install OpenJDK 11```<br>```    sudo apt install -y openjdk-11-jdk```<br>```# Set Java environment variables```<br>```    echo "Setting JAVA_HOME environment variable..."```<br>```    export JAVA_HOME=$(dirname $(dirname $(readlink -f $(which java))))```<br>```    echo "export JAVA_HOME=$JAVA_HOME" >> ~/.bashrc```<br>```    echo "export PATH=\$PATH:\$JAVA_HOME/bin" >> ~/.bashrc```<br>```    source ~/.bashrc```<br>```else```<br>```    echo "Java is already installed."```<br>```fi```<br>``````<br>```# Verify Java installation```<br>```java -version```<br> |
|Task output |This preset task has no output artifacts. |
|Advanced settings |[Webhook notification](https://docs.byteplus.com/en/docs/cp/Webhook_notification): Supports sending task\-level messages via Webhook and Lark bot to help you stay up to date with task updates. |


<span id=".6L-Q6KGM57uT5p6c"></span>
## Execution results

On the run details page of the current pipeline, view information such as the run log and configuration of the current task.


* Click **Log** to view the pipeline execution log for the current task.

* Click **View batch tasks** to be redirected to the cloud server console, where you can view the execution status of ECS batch tasks.
