---
title: "SDK reference"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/SDK_reference"
---

This topic provides SDK\-based development instructions for managing VCI Agent Sandbox by using the E2B protocol.

<span id="nq59Gpxk"></span>
## E2B compatibility


|**Category** |**API** |**Description** |**Compatibility** |**Compatibility remarks** |
|---|---|---|---|---|
|Sandbox lifecycle |create |Creates a VCI Agent Sandbox. |Partially compatible |The following capabilities are not supported: network access control, in\-place configuration change, and automatic pause. |
||get_info |Queries VCI Agent Sandbox instance information. |Fully compatible |None |
||list |Lists all VCI Agent Sandbox information. |Fully compatible |None |
||delete |Deletes the specified VCI Agent Sandbox instance. |Fully compatible |None |
||connect |Connects to the specified VCI Agent Sandbox instance. |Fully compatible |None |
||pause |Pauses the specified VCI Agent Sandbox instance. This interface is asynchronous. When the interface call is successful, the underlying Pod for the Sandbox is reclaimed while the snapshot is still being created. |Fully compatible |None |
||resume |Resumes the VCI Agent Sandbox instance. Data will be automatically restored from the writable layer snapshot generated during the last pause. |Fully compatible |None |
|File system |write |The `e2b-code-interpreter` component needs to run in the primary container. You can view the definition of the `e2b-code-interpreter` component in the `initcontainer` of the template. |Fully compatible |In addition to defining relevant settings in the `initcontainer` field in the template, you can also use the annotation `agent.sandbox.io/enable-envd-injection: "true"` to allow VCI to automatically inject the `envd` program. |
||read ||Fully compatible ||
|Code execution |run_code ||Fully compatible ||
|Command execution |commands.run ||Fully compatible ||
|API Key management |\- |Because the E2B code interpreter SDK does not include API Key management functionality, relevant operations are typically performed via the E2B web console, E2B CLI, or HTTP requests. VCI Agent Sandbox primarily supports HTTP request methods, including POST, DELETE, and GET. |N/A |None |
|Template management |post_templates |Creates the template based on the complete SandboxTemplate structure constructed. |Fully compatible |None |
||requests.delete |Deletes the specified template. This interface is not available in the native E2B SDK. We recommend using the API to operate on templates. |N/A |None |
||requests.patch |Updates the specified template. This interface is not available in the native E2B SDK. We recommend using the API to operate on templates. |N/A |None |
||requests.get |Queries the details of a single template. This interface is not available in the native E2B SDK. We recommend using the API to operate on templates. |N/A |None |
|Snapshot management |create_snapshot |Creates a snapshot. |Fully compatible |None |
||requests.delete |Deletes a snapshot. |No compatibility |None |
||list_snapshot |Queries a list of snapshots. It returns only snapshots that have been created and are available. |Fully compatible |None |
|Monitoring |get_metrics |Queries Sandbox monitoring data. |Partially compatible |You cannot specify a start or end time. |


<span id="4oWPWiWQ"></span>
## E2B SDKs

The official E2B website provides multiple SDK integration methods, such as `e2b` and `e2b_code_interpreter`. For the scenario described in this topic, we recommend using `e2b_code_interpreter`, which comes pre\-installed with Python libraries for data analysis.

```Python
pip install e2b-code-interpreter==2.4.1 e2b==2.10.2 anthropic python-dotenv
```


All code samples in this topic are in Python. For code samples in other programming languages, see the [E2B documentation](https://e2b.dev/docs/code-interpreting/supported-languages).

<span id="1aKr6rMW"></span>
## Standard E2B capabilities

<span id="xbDnBed4"></span>
### Sandbox lifecycle


<Tabs>
<Tab zoneid="tHNi96JpMy" title="Create Sandboxes">
<TabTitle>Create Sandboxes</TabTitle>

<span id="mODZOoBT"></span>
#### Request body parameters


|**Parameter Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|template |string |Yes |The template ID used for Sandbox creation. |
|timeout |int |No |Sandbox lifetime:<br><br><br>* Unit: seconds<br><br>* Default value: 300 |
|metadata |Dict[str, str] |No |Additional annotations that need to be added to the Sandbox. |
|secure |bool |No |Specifies whether to enable `envd` authentication for the Sandbox:<br><br><br>* **True**: Enables authentication for `envd`. You need to configure authentication information. After configuration is successful, authentication information is required to access `envd` for performing file or command operations. <br><br>* **False**: Disables `envd` authentication. |


<span id="7JNufF0J"></span>
#### Response parameters


|**Parameter Name** |**Type** |**Description** |
|---|---|---|
|SandboxInfo |Class |The class containing basic sandbox information. For sub\-parameter descriptions, see the **SandboxInfo** section of this topic. |


<span id="3KRGi7d6"></span>
##### **SandboxInfo**


|**Parameter Name** |**Type** |**Description** |
|---|---|---|
|template_id |string |The template ID used for Sandbox creation. |
|sandbox_id |string |The ID of the Sandbox instance. |
|envd_version |string |The `envd` version used. |
|_envd_access_token |string |`envd` authentication information. |
|domain |string |The domain name for accessing the E2B API. |


<span id="ksCmsohu"></span>
#### Examples

```Python
def create_sandbox(template):
    sbx = Sandbox.create(template=template, secure=True)
    print("created sandbox_id=", sbx.sandbox_id)
    return sbx
```



</Tab>
<Tab zoneid="Kofx0CjJ2m" title="Query Sandboxes">
<TabTitle>Query Sandboxes</TabTitle>

<span id="uKc53d7O"></span>
#### Response parameters


|**Parameter Name** |**Type** |**Description** |
|---|---|---|
|SandboxInfo |Class |The class containing basic sandbox information. For sub\-parameter descriptions, see the **SandboxInfo** section of this topic. |


<span id="lukRxrtP"></span>
##### **SandboxInfo**


|**Parameter Name** |**Type** |**Description** |
|---|---|---|
|template_id |string |The template ID used for Sandbox creation. |
|sandbox_id |string |The ID of the Sandbox instance. |
|envd_version |string |The `envd` version used. |
|_envd_access_token |string |`envd` authentication information. |
|domain |string |The domain name for accessing the E2B API. |


<span id="AsBiamH7"></span>
#### Examples

```Python
def get_sandbox_info(sandbox_id: str) -> None:
    sbx = Sandbox.connect(sandbox_id=sandbox_id)
    info = sbx.get_info()

    print("sandbox_id=", info.sandbox_id)
    print("template_id=", info.template_id)
    print("state=", info.state)
    print("started_at=", info.started_at)
    print("end_at=", info.end_at)
    print("metadata=", info.metadata)
```



</Tab>
<Tab zoneid="T2QVW2Q2hC" title="Delete Sandboxes">
<TabTitle>Delete Sandboxes</TabTitle>

<span id="7u2j6e8M"></span>
#### Examples

```Python
def delete_sandbox(sandbox_id: str) -> None:
    sbx = Sandbox.connect(sandbox_id=sandbox_id)
    ok = sbx.kill()
    print("killed:", ok)
```



</Tab>
<Tab zoneid="dSeCWKKBZz" title="Pause Sandboxes">
<TabTitle>Pause Sandboxes</TabTitle>

<span id="ZtBlj26z"></span>
#### Examples

```Python
def pause_sandbox(sandbox_id: str) -> None:
    sbx = Sandbox.connect(sandbox_id=sandbox_id)
    sbx.beta_pause()
```



</Tab>
<Tab zoneid="L6YnEzZFeV" title="Resume Sandboxes">
<TabTitle>Resume Sandboxes</TabTitle>

<span id="9ybRQkAu"></span>
#### Request path parameter


|**Parameter Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|sandboxId |string |Yes |The ID of the Sandbox instance. |


<span id="tR2GX46y"></span>
#### Response parameters


|**Parameter Name** |**Type** |**Description** |
|---|---|---|
|SandboxInfo |Class |The class containing basic sandbox information. For sub\-parameter descriptions, see the **SandboxInfo** section of this topic. |


<span id="zpq71HWs"></span>
##### **SandboxInfo**


|**Parameter Name** |**Type** |**Description** |
|---|---|---|
|template_id |string |The template ID used for Sandbox creation. |
|sandbox_id |string |The ID of the Sandbox instance. |
|envd_version |string |The `envd` version used. |
|_envd_access_token |string |`envd` authentication information. |
|domain |string |The domain name for accessing the E2B API. |


<span id="RcoQbQh6"></span>
#### Examples

```Python
def resume_sandbox(sandbox_id: str) -> None:
    sbx = Sandbox.connect(sandbox_id=sandbox_id)
```



</Tab>
</Tabs>


<span id="PvkHbCGJ"></span>
### File system


<Tabs>
<Tab zoneid="MFwv8Yz8c8" title="Upload files">
<TabTitle>Upload files</TabTitle>

<span id="2Aqhhi06"></span>
#### Examples

```Python
def upload_file(sbx):
    with open("./test.txt", "rb") as file:
        sbx.files.write("/test.txt", file)
```



</Tab>
<Tab zoneid="NqiyFAwffw" title="Download files">
<TabTitle>Download files</TabTitle>

<span id="kwULNWyQ"></span>
#### Examples

```Python
def read_file(sbx):
    file_content = sbx.files.read("/test.txt")
    print(file_content)
```



</Tab>
</Tabs>


<span id="CQKk21WX"></span>
### Code execution


<Tabs>
<Tab zoneid="ngedEkJUf6" title="Code execution">
<TabTitle>Code execution</TabTitle>

<span id="YKX33hoT"></span>
#### Examples

```Python
def run_code(sbx):
    sbx.run_code("print('hello world')")
```



</Tab>
</Tabs>


<span id="8qgpccar"></span>
### Command execution


<Tabs>
<Tab zoneid="qkjBguIsho" title="Command execution">
<TabTitle>Command execution</TabTitle>

<span id="saZ2ynM3"></span>
#### Examples

```Python
def run_command(sbx):
    sbx.commands.run('echo hello')
```



</Tab>
</Tabs>


<span id="MTTm3HJ5"></span>
### API Key management

VCI supports HTTP request methods such as POST, DELETE, and GET.


<Tabs>
<Tab zoneid="pj0M2KWIkx" title="Create API Keys">
<TabTitle>Create API Keys</TabTitle>

<span id="Ml9SZ0c3"></span>
#### Examples

```Python
# API Key configuration.
API_BASE_URL = os.getenv("API_BASE_URL", "your.domain")
ADMIN_API_KEY = os.getenv("ADMIN_API_KEY", "sk-local-test-123456")

# API request headers.
headers = {
    "X-API-KEY": ADMIN_API_KEY,
    "Content-Type": "application/json"
}

def create_api_key(name):
    """Create a new API key"""
    url = f"{API_BASE_URL}/api-keys"
    payload = {"name": name}
    
    print(f"Creating API key: {name}")
    response = requests.post(url, headers=headers, json=payload)
```



</Tab>
<Tab zoneid="WHtCnodVtc" title="Delete API Keys">
<TabTitle>Delete API Keys</TabTitle>

<span id="EqrZTGpq"></span>
#### Examples

```Python
url = f"{API_BASE_URL}/api-keys/{key_id}"
headers = {
    "X-API-KEY": ADMIN_API_KEY,
    "Content-Type": "application/json"
}

response = requests.delete(url, headers=headers)
```



</Tab>
<Tab zoneid="cnE9ePYbS9" title="Query API Keys">
<TabTitle>Query API Keys</TabTitle>

<span id="iuQZwhvM"></span>
#### Examples

```Python
url = f"{API_BASE_URL}/api-keys"
headers = {
    "X-API-KEY": ADMIN_API_KEY,
    "Content-Type": "application/json"
}
        
print(f"Getting API key list...")
response = requests.get(url, headers=headers)   
```



</Tab>
</Tabs>


<span id="q6NdDO1H"></span>
### Template management


<Tabs>
<Tab zoneid="fws4QZ0sBH" title="Create templates">
<TabTitle>Create templates</TabTitle>

<span id="zBf0PYbO"></span>
#### Examples

```Python
from e2b.connection_config import ConnectionConfig
from e2b.api.client_sync import get_api_client
from e2b.api.client.api.templates import post_templates
from e2b.api.client.models import TemplateBuildRequest

"""
    使用官方 E2B SDK 创建 SandboxTemplate
    
    Args:
        api_base_url: E2B API 服务基础地址
        api_key: API 认证密钥
        template_name: 模版名称
        namespace: Kubernetes 命名空间（默认 default）
        template_spec: 可选的模版 spec 配置
"""
    # 2. Configure the template spec.
    if template_spec is None:
        template_spec = {
            "podTemplate": {
                "metadata": {
                    "annotations": {
                        "agent.sandbox.io/snapshot-max-num": "2",
                        
                        "vci.vke.volcengine.com/enable-auto-create-imc": "true",
                        "vci.vke.volcengine.com/preferred-instance-family": "vci.u1,vci.n3i",
                        "vci.volcengine.com/persistent-container": "true",
                        "vci.volcengine.com/tls-enable": "false",
                        "vci.volcengine.com/usable-disk-capacity": "40",
                        "vke.volcengine.com/burst-to-vci": "enforce"
                    }
                },
                "spec": {
                    "containers": [
                        {
                            "env": [
                                {"name": "ENVD_DIR", "value": "/mnt/envd"},
                                {"name": "PORT", "value": "49999"}
                            ],
                            "image": "cr-cn-guilin-boe.volces.com/vke/code-interpreter:v0.1.0",
                            "lifecycle": {
                                "postStart": {
                                    "exec": {
                                        "command": ["/bin/bash", "-c", "/mnt/envd/envd-run.sh"]
                                    }
                                }
                            },
                            "name": "main",
                            "resources": {
                                "limits": {"cpu": "2", "memory": "4Gi"},
                                "requests": {"cpu": "2", "memory": "4Gi"}
                            },
                            "volumeMounts": [
                                {"mountPath": "/mnt/envd", "name": "envd-volume"}
                            ]
                        }
                    ],
                    "initContainers": [
                        {
                            "command": ["sh", "/workspace/entrypoint.sh"],
                            "env": [
                                {"name": "ENVD_DIR", "value": "/mnt/envd"},
                                {"name": "__IGNORE_RESOURCE__", "value": "true"}
                            ],
                            "image": "helm-cr-cn-guilin-boe.cr.volces.com/vke/agent-runtime:v0.0.4",
                            "name": "runtime",
                            "restartPolicy": "Always",
                            "volumeMounts": [
                                {"mountPath": "/mnt/envd", "name": "envd-volume"}
                            ]
                        }
                    ],
                    "terminationGracePeriodSeconds": 1,
                    "volumes": [{"emptyDir": {}, "name": "envd-volume"}]
                }
            }
        }

    # 3. Create the complete SandboxTemplate structure.
    sandbox_template = {
        "apiVersion": "extensions.agents.x-k8s.io/v1alpha1",
        "kind": "SandboxTemplate",
        "metadata": {
            "name": template_name,
            "namespace": namespace
        },
        "spec": template_spec
    }

    # 4. Initialize the E2B SDK connection configuration.
   try:
        config = ConnectionConfig(
            api_key=api_key,
            api_url=api_base_url
        )

        # Obtain the API client.
        api_client = get_api_client(
            config,
            require_api_key=True,
            require_access_token=False
        )
        print(f"  ✅ SDK 连接初始化成功！")
    except Exception as e:
        print(f"  ❌ SDK 连接初始化失败: {e}")
        return None

    # 5. Construct an SDK request object.
    # (Required) TemplateBuildRequest must include the dockerfile field. Even if the custom server does not use this field, you need to provide an empty value.
        build_request = TemplateBuildRequest(
            dockerfile=""
        )

        build_request["namespace"] = namespace
        build_request["sandboxTemplate"] = sandbox_template

        print(f"  ✅ 请求对象构建成功！")

    # 6. Call the official SDK interface to create the template.
    # To obtain the complete response, use sync_detailed.
        response = post_templates.sync_detailed(
            body=build_request,
            client=api_client
        )
```



</Tab>
<Tab zoneid="QlNlSVvs0b" title="Delete templates">
<TabTitle>Delete templates</TabTitle>

<span id="ZsVonNJ3"></span>
#### Examples

```Python
# Template request format: namespace--template-id
template_path = f"{namespace}--{template_id}"
url = f"{api_base_url}/templates/{template_path}"

headers = {
    "X-API-KEY": api_key,
    "Content-Type": "application/json",
}

params = {}
if owner:
    params["owner"] = owner
   
response = requests.delete(url, headers=headers, params=params)
```



</Tab>
<Tab zoneid="YqhnCythcq" title="Update templates">
<TabTitle>Update templates</TabTitle>

The native E2B SDK update interface only supports switching between the public and private states. In contrast, the E2B management functionality of the VCI Agent Sandbox supports modifying more template property definitions.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">When updating a template, construct a complete request by referring to the request parameters for <strong>template creation</strong>.</div>


* <div data-tips="true" data-tips-type="warning">When modifying the <code>annotations</code> or <code>containers</code> configuration, you need to pass in all information under the corresponding configuration block, even if only a single field within the block is adjusted.</div>



<span id="C4t3PR9N"></span>
#### Examples

```Python
import os
import sys
from e2b.connection_config import ConnectionConfig
from e2b.api.client_sync import get_api_client
from e2b.api.client.api.templates import patch_templates_template_id
from e2b.api.client.models import TemplateUpdateRequest

    """
    使用 E2B SDK 修改模板
    """  
    template_path = f"{namespace}--{template_id}"
    
    # 1. Create a connection configuration.
    config = ConnectionConfig(
        api_key=api_key,
        api_url=api_base_url
    )
    
    # 2. Obtain the API client.
    api_client = get_api_client(
        config,
        require_api_key=True,
        require_access_token=False
    )
    
    # 3. Create the update request object.
    update_request = TemplateUpdateRequest()
        
    # Similarly to template creation, create a complete request payload.
    # Only containers/annotations-level granular modifications are supported. To modify any field in the containers, pass in all fields of the containers structure.
    
    # It contains the namespace and sandboxTemplate fields.
    sandbox_template = {
        "apiVersion": "extensions.agents.x-k8s.io/v1alpha1",
        "kind": "SandboxTemplate",
        "metadata": {
            "name": template_id,
            "namespace": namespace
        },
        "spec": {
            "podTemplate": {
                "spec": {
                    "containers": [
                        {
                            "name": "main",
                            "image": new_image
                        }
                    ]
                }
            }
        }
    }
    
    payload = {
        "namespace": namespace,
        "sandboxTemplate": sandbox_template
    }
    
    # Add the fields to update_request by using additional_properties.
    update_request["namespace"] = namespace
    update_request["sandboxTemplate"] = sandbox_template
    
    # Send the request.
    print(f"\n🚀 发送更新请求...")
    url = f"{api_base_url}/templates/{template_path}"
    headers = {
        "X-API-KEY": api_key,
        "Content-Type": "application/json"
    }
    
    try:
        response = requests.patch(url, headers=headers, json=payload)
        
```



</Tab>
<Tab zoneid="DeSOyUmgwa" title="Query details of a template">
<TabTitle>Query details of a template</TabTitle>

<span id="328kni9u"></span>
#### Examples

```Python
# Template request format: namespace--template-id
template_path = f"{namespace}--{template_id}"
url = f"{api_base_url}/templates/{template_path}"

headers = {
    "X-API-KEY": api_key,
    "Content-Type": "application/json",
}

response = requests.get(url, headers=headers)
```


<span id="cxFIsbJ8"></span>
#### Response result

```JSON
{
    "templateID": "template-13ec94e0-ab32-4a26-837d-f0167ffb1004",
    "public": false, // Templates cannot be set as public or private.
    "aliases": [
        "template-13ec94e0-ab32-4a26-837d-f0167ffb1004"
    ],
    "names": [
        "template-13ec94e0-ab32-4a26-837d-f0167ffb1004"
    ],
    "createdAt": "2026-05-05T14:54:28Z",
    "updatedAt": "2026-05-05T14:54:28Z",
    "lastSpawnedAt": null, // Recording the time of the template use is not supported.
    "spawnCount": 0, // It does not support querying the number of times the template has been used.
    "builds": [
        {
            "buildID": "a9d48185-53f6-4baf-b0d4-e273e5230c66",
            "status": "ready"
        }
    ]
}
```



</Tab>
</Tabs>


<span id="8EPLawYI"></span>
### Snapshot management


<Tabs>
<Tab zoneid="ZDsig5oafI" title="Create snapshots">
<TabTitle>Create snapshots</TabTitle>

<span id="KjsyU0Wk"></span>
#### Response parameters


|**Parameter Name** |**Type** |**Description** |
|---|---|---|
|SandboxInfo |Class |The class containing basic sandbox information. For sub\-parameter descriptions, see the **SandboxInfo** section of this topic. |


<span id="f6G5Xm60"></span>
##### **SandboxInfo**


|**Parameter Name** |**Type** |**Description** |
|---|---|---|
|snapshotId |string |The snapshot ID. |


<span id="JU8Fu7Ve"></span>
#### Examples

```Python
def create_snapshot(sandbox_id: str) -> None:
    sbx = Sandbox.connect(sandbox_id)
    snap_shot_info = sbx.create_snapshot()
```



</Tab>
<Tab zoneid="YuzdrtuFNd" title="Delete snapshots">
<TabTitle>Delete snapshots</TabTitle>

<span id="OwQjkvfr"></span>
#### Request path parameter


|**Parameter Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|sandboxId |string |Yes |The ID of the Sandbox instance. |


<span id="5gi4f2hf"></span>
#### Examples

```Python
def delete_snapshot(snapshot_id: str) -> None:
    """    
    api_base_url: E2B API 服务基础地址
    api_key: API 认证密钥
    """
    url = f"{api_base_url}/snapshots/{snapshot_id}"

    headers = {
        "X-API-KEY": api_key,
        "Content-Type": "application/json",
    }
    
    response = requests.delete(url, headers=headers)
```



</Tab>
<Tab zoneid="zwwrvPDecA" title="Query snapshots">
<TabTitle>Query snapshots</TabTitle>

<span id="TadkYwGM"></span>
#### Examples

```Python
def list_snapshot(sandbox) -> None:
    paginator = sbx.list_snapshots()
    while paginator.has_next:
        snapshots = paginator.next_items()
        print(snapshots)
```



</Tab>
</Tabs>


<span id="vwLQOHUt"></span>
### Monitoring


<Tabs>
<Tab zoneid="cRo2F0BCb2" title="Get metrics">
<TabTitle>Get metrics</TabTitle>

<span id="GWxVYAQM"></span>
#### Response parameters


|**Parameter Name** |**Type** |**Description** |
|---|---|---|
|List[SandboxMetrics] |List |The list containing basic sandbox information. For sub\-parameter descriptions, see the **SandboxMetrics** section of this topic. |


<span id="5wDJuq0a"></span>
##### SandboxMetrics


|**Parameter Name** |**Type** |**Description** |
|---|---|---|
|cpu_count |Integer |The total CPU cores of the sandbox. |
|cpu_used_pct |Float |The CPU utilization of the sandbox. |
|disk_total |Integer |The total disk size of the sandbox. |
|disk_used |Integer |The disk size used by the sandbox. |
|mem_total |Integer |The total memory of the sandbox. |
|mem_used |Integer |The memory size used by the sandbox. |
|timestamp |DataTime |The metric timestamp. |


<span id="FS0Tu0ln"></span>
#### Examples

```Python
def metrics_operation(sbx):
    res = sbx.get_metrics()
    print(res)
```



</Tab>
</Tabs>
