---
title: "Accessing VCI Agent Sandbox via APIG"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Accessing_VCI_Agent_Sandbox_via_APIG"
---

APIG supports integration with VCI Agent Sandbox. It abstracts Agent Sandbox Pods under VCI instances in a container cluster into an Upstream and uses it as a routing backend for the gateway. This is suitable for scenarios where a business is deployed using Agent Sandbox and needs to dynamically route traffic by Sandbox ID through the gateway. This topic describes how to access VCI Agent Sandbox through APIG.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This topic provides data\-plane forwarding for Agent Sandbox, for example, forwarding requests to be executed to the sandbox. If control\-plane forwarding for Agent Sandbox, such as creating a sandbox, also needs to be integrated with APIG, see <a href="https://docs.byteplus.com/en/docs/apig/Creating_a_Vital_Kubernetes_Engine_type_Upstream?lang=en">Creating VKE type Upstreams</a>.</div>


<span id="9w6sMXrR"></span>
## Prerequisites


* A cluster required for VCI workloads has been created and VCI Agent Sandbox has been installed. For details, see [Using VCI in VPC-CNI clusters](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Vital-Kubernetes-Engine), [Using VCI in Flannel clusters](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Flannel-cluster), and [Installation guide](https://docs.byteplus.com/en/docs/vke/Installation_guide?lang=en#pZGIXGfo).

* An APIG instance has been created. For details, see [Creating instances](https://docs.byteplus.com/en/docs/apig/Creating_an_instance). The IP address of an APIG instance may change when the instance is upgraded or restarted and cannot be fixed at this time. If VCI Agent Sandbox has Network Policy enabled to restrict inbound and outbound traffic, we recommend that you select a smaller subnet address space when creating the APIG instance. This avoids IP address waste and excessive permission grants, and allows the subnet of the APIG instance in the Network Policy configuration. See the following reference configuration. For more information about Network Policy, see [Using a NetworkPolicy for network access control](https://docs.byteplus.com/en/docs/vke/Using-NetworkPolicies-for-network-access-control?lang=en).

   ```YAML
   apiVersion: networking.k8s.io/v1
   kind: NetworkPolicy
   metadata:
    name: allow-ingress-from-cidr
    namespace: default
   spec:
    podSelector:
        matchLabels:
            app: web # Match Pods with label app=web (the target objects to be accessed).
    policyTypes:
    - Ingress # Control inbound traffic.
    ingress:
    - from:
        - ipBlock:
            cidr: 192.**.**.**/** 
            # Restrict the source CIDR to as small a range as possible. Set it to the APIG instance subnet.
            # To exclude a range, add except:
            # except:
            # - 192.**.**.**/**
        ports:
          - protocol: TCP
            port: 49983 # envd port
          - protocol: TCP
            port: 49999 # code interpreter port
   ```
   


<span id="3WsqJpvY"></span>
## Limits

The APIG instance and VKE cluster must be in the same VPC.

<span id="pkzdrbyU"></span>
## Procedure

<span id="3v01m5zn"></span>
### Step 1: Import the container cluster where Agent Sandbox resides


1. Log in to the [APIG console](https://console.byteplus.com/veapig).

2. Select the target region in the top navigation bar.

3. In the **Instance management** drop\-down list, select the target instance, and then click **Import container cluster**. 

4. On the cluster list page, click **Import cluster**.

5. On the "Import cluster" page, configure the information as required. For details, see [Importing VKE clusters](https://docs.byteplus.com/en/docs/apig/Import_container_cluster).

   
   |Parameter |Description |
   |---|---|
   |K8S cluster |Select the specific cluster to integrate with. In this example, an existing cluster named **smart\-llm\-router** is selected.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Only clusters in the same VPC as the gateway instance can be selected.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Only clusters with status "Running" can be selected.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For Flannel clusters, the Pod CIDR block of the selected cluster must match the Pod CIDR block specified during gateway instance creation.</div><br> |
   |Route synchronization |Specify whether to enable the route synchronization feature.<br><br>After route synchronization is enabled, APIG automatically listens to changes in the container cluster's Ingress resources and applies their relevant configurations. It also converts Ingress resources into services, custom domains, routes, Upstreams, and other resources, and integrates them into the current gateway. For more information, see [Synchronizing Ingress routes](https://docs.byteplus.com/en/docs/apig/Cluster_ingress_synchronization). |
   

6. Click **Confirm** to complete the import.


<span id="og6LOazU"></span>
### Step 2: Create an Upstream of the VCI Agent Sandbox type


1. In the left navigation pane, click **Upstreams**. 

2. On the Upstream list page, click **Create Upstream**.

   3. On the "Create Upstream" page, enter the parameter information as required.

   * **Basic information**

      
      |Parameter |Description |
      |---|---|
      |Upstream name |Specify a name for the Upstream. The Upstream name must be unique within the same instance. In this example, it is set to **agent\-sandbox**. |
      

   * **Back\-end configuration**

      
      |Parameter |Description |
      |---|---|
      |Backend service |Select the backend service type that the Upstream integrates with. In this example, **VCI Agent Sandbox** is selected. |
      |Listening range |Configure the listening scope.<br><br><br>* **All Sandboxes**: Covers all Sandboxes in the selected cluster.<br><br>* **Label selected**: Enter the Key and Value of the Sandbox Label. **Using form editing** and **Using JSON format editing are supported**. |
      

4. Click **Confirm** to finish.


<span id="NJVwFQhf"></span>
### Step 3: Create a service


1. In the left navigation pane, click  ** Service list (Domain name)** . On the Service list page, click **Create Service**.

2. In the "Create Service" dialog box, configure the service parameters.

   
   |Parameter |Description |
   |---|---|
   |Instance |A service is an instance\-level resource. |
   |Service name |Enter a custom service name. The service name must be unique within the same instance. In this example, it is set to **agent\-sandbox\-service**. |
   |Notes |Enter note information. |
   

3. Click **Confirm** to complete service creation.


<span id="pSbiQfyX"></span>
### Step 4: Create a route


1. In the left navigation pane, select **Service list (Domain name)** . On the service list page, click **Add route** in the **Actions** column of the target service.

2. On the **Add route** page, configure the route information. Only the Upstream traffic distribution configuration is described here. For details, see [Creating routes](https://docs.byteplus.com/en/docs/apig/Creating_a_route?lang=en).

   
   |Parameter |Description |
   |---|---|
   |Upstream types |Select the type of Upstream to connect to. In this example, **VCI Agent Sandbox** is selected. |
   |Select upstream |Select the specific Upstream to connect to. Select the Upstream of the VCI Agent Sandbox type that you created. |
   |Weight |Configure the traffic weight for the current Upstream. Enter an integer from 1 to 1000.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The system calculates traffic distribution proportionally based on the total weight value of all configured Upstreams and the weight ratio of each individual Upstream. The displayed percentages are rounded to two decimal places.</div><br> |
   

3. Click **Confirm** to complete the route creation.


<span id="unzJ1caP"></span>
### Step 5: Obtain the default service domain name for SDK reference


1. In the left navigation pane, click **Service list (Domain name)** .

3. Click the name of the target service, and obtain the access domain name on the **Service overview** tab.

4. When referencing the SDK on the client side, add the following environment variables, replacing the domain name with the default service domain name you obtained. For details, see [SDK reference](https://docs.byteplus.com/en/docs/vke/SDK_reference?lang=en#4oWPWiWQ).

   ```Python
   os.environ["E2B_SANDBOX_URL"] = "s****.apigateway-cn-beijing.volceapi.com"
   ```
   


<span id="29odxZQq"></span>
## Validate results

Before validating the result, you need to create a template. For specific operations, see [Create a template](https://docs.byteplus.com/en/docs/vke/Getting_started?lang=en#ONuXBkTU).


1. Create a file named `sandbox_demo.py` with the following content. In this example, the input parameter value of the `run_sandbox_demo` function is `default--code-interpreter-template`, where `default` is the namespace in the VKE cluster and `code-interpreter-template` is the template name.

   ```Python
   import os
   from e2b_code_interpreter import Sandbox
   
   # BytePlus APIG environment variable configuration
   os.environ["E2B_API_KEY"] = "c03****"
   os.environ["E2B_API_URL"] = "http://suq****.apigateway-cn-beijing.volceapi.com"# Configure the control plane API gateway based on your actual setup. APIG is not a hard dependency.
   os.environ["E2B_SANDBOX_URL"] = "http://sih8****.apigateway-cn-beijing.volceapi.com"
   
   
   def run_sandbox_demo(template_name: str):
       sandbox = None
       try:
           print("Start creating a sandbox instance")
           sandbox = Sandbox.create(
               template=template_name,
           )
           print(f"Sandbox information：{sandbox.get_info()}")
   
           print("Running shell command：echo hello from sandbox")
           result = sandbox.commands.run("echo hello from sandbox")
           print("Standard output：", result.stdout.strip())
   
       except Exception as e:
           print(f"Sandbox error：{e}")
       finally:
           if sandbox is not None:
               print("Destroying sandbox resources")
               sandbox.kill()
   
   
   if __name__ == "__main__":
       run_sandbox_demo("default--code-interpreter-template")# The input parameter format here is {namespace in the VKE cluster}--{template name}
   ```
   

2. Navigate to the directory where the file is located and execute the following command:

   ```Bash
   python sandbox_demo.py
   ```
   

   The expected output is as follows:

   ```Bash
   Start creating a sandbox instance
   Sandbox information:SandboxInfo(sandbox_id='default--sbx-19****', template_id='default--code-interpreter-template', name='', 'metadata={'agents.xk8s.io/controller-first-observed-at'}
   Running shell command:echo hellofrom sandbox
   Standard output:hello from sandbox
   Destroying sandbox resources
   ```
