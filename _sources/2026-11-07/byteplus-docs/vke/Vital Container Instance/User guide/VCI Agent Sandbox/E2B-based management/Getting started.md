---
title: "Getting started"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Getting_started"
---

This topic demonstrates the complete workflow for creating an AI Agent instance and persisting data by using the Python SDK based on the minimum viable product (MVP) principle. This example workflow includes common operations, such as creating templates, creating Sandboxes, reading/writing files, running code and commands, pausing/resuming Sandboxes, and querying status.

<span id="6T61d2Av"></span>
## Preparation


1. Configure E2B\-related parameters in the YAML file for the VCI Agent Sandbox controller.

   
   <Tabs>
   <Tab zoneid="iGpj8KQraj" title="VCI Agent Sandbox not installed">
   <TabTitle>VCI Agent Sandbox not installed</TabTitle>
   
   Follow the steps in the [installation guide](https://docs.byteplus.com/en/docs/vke/Installation_guide?lang=en) to install VCI Agent Sandbox. During the installation process, set `enableE2BServer` to `true` in the `values.yaml` file. Configure the remaining parameters as needed.
   
   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>
   
   
   <div data-tips="true" data-tips-type="warning">When installing VCI Agent Sandbox, select v0.1.1\-vke.3 or later for the Chart version of the <strong>agent\-sandbox</strong> application template. Earlier versions do not have built\-in E2B parameters.</div>
   
   
   
   </Tab>
   <Tab zoneid="TuA8tSK84Q" title="VCI Agent Sandbox installed">
   <TabTitle>VCI Agent Sandbox installed</TabTitle>
   
   In the [VKE console](https://console.byteplus.com/vke), go to **Application center** \> **Helm** and select the target cluster and namespace where your VCI Agent Sandbox is installed.  Locate the Helm application corresponding to the VCI Agent Sandbox controller and update its configuration:
   
   
   * For the Chart version of the application template, select v0.1.1\-vke.3 or later.
   
   * In the YAML file, set `enableE2BServer` to `true` to enable E2B. Update other parameters according to your actual requirements.
   
   
   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5311cbe86ba68d89cb2aa4997672807f.png) </span>)
   
   
   </Tab>
   </Tabs>
   

2. Install the E2B Python SDK.

   ```Bash
   pip install e2b-code-interpreter==2.4.1 e2b==2.10.2 anthropic python-dotenv
   ```
   

3. Ensure that you have an available E2B API Key and configure the address and key (such as `API_BASE_URL` and `ADMIN_API_KEY`) required to access the E2B API in your environment. By default, the E2B API Key is saved in the `e2b-key-store` Secret in the `agent-sandbox-system` namespace. For details, see the [installation guide](https://docs.byteplus.com/en/docs/vke/Installation_guide?lang=en). You can also obtain the API Key by calling the API via the SDK. For details, see [Managing API Keys](https://docs.byteplus.com/en/docs/vke/SDK_reference#MTTm3HJ5).

4. Expose the E2B service externally via an ALB Ingress. For details, see [Exposing the E2B service via an Ingress](https://docs.byteplus.com/en/docs/vke/Installation_guide#tvYM2kxn).


<span id="RtpN4Tkh"></span>
## Procedure

<span id="ONuXBkTU"></span>
### Step 1: Create a template

A template defines Sandbox startup parameters. You can create a template in your cluster via the [Kubernetes API](https://kubernetes.io/zh-cn/docs/concepts/overview/kubernetes-api/). Alternatively, you can create a template via the VCI SDK. For details, see [Managing templates](https://docs.byteplus.com/en/docs/vke/SDK_reference).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">In the sample code below, replace the image, resource, and annotation settings with your actual information. For other parameters in the code, you can keep the existing settings.</div>


* <div data-tips="true" data-tips-type="default">After the template is created, obtain the template ID for use in subsequent Sandbox instance creation.</div>



```YAML
apiVersion: extensions.agents.x-k8s.io/v1alpha1
kind: SandboxTemplate
metadata:
  name: code-interpreter-template
  namespace: default
spec:
  podTemplate:
    metadata:
      annotations:
        agent.sandbox.io/enable-envd-injection: "true"  # Inject envd into the primary container.
        vci.vke.volcengine.com/enable-auto-create-imc: "true"  # Enable automatic image caching.
        vci.vke.volcengine.com/preferred-instance-family: vci.u1,vci.n3i  # The VCI specification.
        vci.volcengine.com/persistent-container: "true"  # Specify whether to enable persistence for the container writable layer data. Valid values: true (enable) and false (disable).
        vci.volcengine.com/tls-enable: "false"  # Enable log collection to collect logs to TLS.
        vci.volcengine.com/usable-disk-capacity: "40"  # Specify the available space of the system volume (writable layer space).
        vke.volcengine.com/burst-to-vci: enforce  # Enforce VCI-based deployment.
    spec:
      containers:
      - image: e2bdev/code-interpreter:latest # Use the executable code image provided by E2B.
        name: main
        resources:
          limits:
            cpu: "2"
            memory: 4Gi
          requests:
            cpu: "2"
            memory: 4Gi
      terminationGracePeriodSeconds: 1
```


<span id="RkukkhjF"></span>
### Step 2: Create a Sandbox

Use the Python SDK to create a Sandbox instance with the template ID obtained in the previous step.

```Python
from e2b_code_interpreter import Sandbox

sbx = Sandbox.create(
    template="default--code-interpreter-template",
    secure=True,
    timeout=600,
    metadata={"scene": "quickstart"}
)

print(f"sandbox id: {sbx.sandbox_id}")
```


The following table describes the parameters.


|Parameter |Description |
|---|---|
|template |The template ID of the SandboxTemplate created in the previous step.<br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When you create a SandboxTemplate through the <a href="https://kubernetes.io/zh-cn/docs/concepts/overview/kubernetes-api/">Kubernetes API</a>, the Template ID is <code><metadata.namespace value--metadata.name value></code>, such as <code>default--code-interpreter-template</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When you create a SandboxTemplate through the VCI SDK, the Template ID is the returned value of the <code>template_id</code> parameter.</div><br> |
|secure |Specifies whether to enable `envd` authentication:<br><br><br>* **True**: Enable this option. We recommend enabling authentication in production.<br><br>* **False**: Disable this option. |
|timeout |The lifetime of the Sandbox. When the timeout expires, the Sandbox is automatically reclaimed.<br><br><br>* Unit: seconds<br><br>* Default value: 300 |
|metadata |Optional information that can be added to help distinguish Sandboxes during subsequent queries or O&M. The data type is `Dict[str, str]`. |


<span id="TDbB5HsI"></span>
### Step 3: Write and read files

After you create the Sandbox, read and write files in the Sandbox. The following example writes the local `./test.txt` file to the Sandbox, reads it from the Sandbox, and prints the file content.

```Python
def write_and_read_file(sbx):
    # Write a local file to /test.txt inside the Sandbox.
    with open("./test.txt", "rb") as file:
        sbx.files.write("/test.txt", file)

    # Read file content from the Sandbox.
    file_content = sbx.files.read("/test.txt")
    print("content in sandbox:", file_content)
```


The following table describes the parameters.


|Parameter |Description |
|---|---|
|files.write(path, file) |Writes a file to the Sandbox. `path` specifies the file path inside the Sandbox. |
|files.read(path) |Reads and returns the file content from the Sandbox. |


<span id="aGMuKHk1"></span>
### Step 4: Run code and commands

After the file is ready, run Python code and shell commands inside the Sandbox.

```Python
def run_code_and_command(sbx):
    # Run Python code.
    sbx.run_code("print('hello world')")
    
    # Run a shell command.
    sbx.commands.run("echo hello")
```


The following table describes the parameters.


|Parameter |Description |
|---|---|
|run_code(code: str) |Runs Python code in the Sandbox. It is suitable for scenarios such as quick calculations and data processing. |
|commands.run(cmd: str) |Run command\-line instructions in the Sandbox. It is suitable for invoking system tools or running scripts. |


<span id="diuVc6Ec"></span>
## Subsequent operations

<span id="ZKc0OexX"></span>
### Pause and resume Sandboxes

When you need to temporarily stop using a Sandbox or release computing power (stop billing), while retaining the current status of the data generated by the Sandbox, you can use the Sandbox pause/resume feature.

```Python
def pause_and_resume(sbx):
    #  Pause the Sandbox. The underlying system will asynchronously create a snapshot and reclaim the Pod.
    sbx.beta_pause()
    sandbox_id = sbx.sandbox_id

    # When resumption is needed, call the connection method to get it automatically resumed based on the last snapshot.
    sbx = Sandbox.connect(sandbox_id=sandbox_id)
    return sbx
```


The following table describes the parameters.


|Parameter |Description |
|---|---|
|beta_pause() |Pauses the current Sandbox. This API is asynchronous, meaning that upon successful invocation, the corresponding Pod will be immediately reclaimed while the snapshot is created in the background. |
|Sandbox.connect(sandbox_id=...) |During subsequent connections to the same sandbox (identified by `sandbox_id`), the Sandbox data will be automatically restored using the writable layer snapshot generated during the last pause. |


<span id="f671qig7"></span>
### View the information and list

When a Sandbox is running, you can view its status.

```Python
def print_sandbox_info(sandbox_id: str) -> None:
    sbx = Sandbox.connect(sandbox_id=sandbox_id)
    info = sbx.get_info()

    print("sandbox_id =", info.sandbox_id)
    print("template_id =", info.template_id)
    print("state =", info.state)
    print("started_at =", info.started_at)
    print("end_at =", info.end_at)
    print("metadata =", info.metadata)
```


The following table describes the parameters.


|Parameter |Description |
|---|---|
|get_info() |Returns the Sandbox details, such as the associated bound template, status, start time, end time, and `metadata`. |
