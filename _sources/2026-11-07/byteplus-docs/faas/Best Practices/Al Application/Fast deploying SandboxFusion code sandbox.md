---
title: "Fast deploying SandboxFusion code sandbox"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Fast_deploying_SandboxFusion_code_sandbox"
---

This article introduces the use of BytePlus Function Service (veFaaS) to fast deploy code sandbox service based on the open\-source SandboxFusion project, to meet the needs of running code in the sandbox.

<span id="TVlpOcHB"></span>
## Background information

SandboxFusion is a code sandbox service based on the HTTP protocol that supports running 23 programming languages. By leveraging namespace resource isolation and cgroup resource management technologies, it achieves lightweight security isolation and flexible deployment features that adapt to a variety of devices, meeting multi\-scenario requirements from edge nodes to cloud servers.

<span id="RMhvBDAr"></span>
## Prerequisites

Relevant products with BytePlus activated


* [Function Service (veFaaS)](https://console.byteplus.com/vefaas)

* [API Gateway (APIG)](https://console.byteplus.com/veapig)


<span id="OQ4bicTM"></span>
## Procedure


1. Log in to [Function Service Console](https://console.byteplus.com/vefaas).

2. On the top navigation bar, select the target region.

3. In the left navigation bar, select **Cloud Sandbox **  \> **Sandbox Application**, and click **Create Sandbox Application**.

4. On the **Create Sandbox Application** page, configure the parameters. When deploying SandboxFusion, pay special attention to the following parameters. Other parameters can remain at their default values. For detailed parameter descriptions, refer to [Sandbox Application](https://docs.byteplus.com/en/docs/faas/Sandbox_applications).

   
   |**Parameter** |**Description** |
   |---|---|
   |**Basic information** ||
   |Name |Specify a custom name for the sandbox application. The sandbox application name must be unique within the same account. The name cannot be modified after being created. |
   |**For sandbox images** ||
   |Container image |Select **public image**, and use `sandbox-fusion` to search for the target image in the **image address** search box on the right. Select the image version as needed.<br><br><br>* Python language image: Image tag is `vefaas-latest`.<br><br>* Multi\-language image: Image tag is `vefaas-python`. |
   |Startup command |Keep the default configuration `bash /root/sandbox/scripts/run.sh`. |
   |Listening port |Keep the default setting as 8000. |
   |**Gateway routing configuration** ||
   |Domain type |The domain type of the sandbox application. Valid values:<br><br><br>* **Unified domain**: All the instances in a sandbox application share the same domain name. You can target a specific instance by including the `x-faas-instance-name` header or the `faasInstanceName` query parameter in requests.<br><br>* **Wildcard domain**: [[beta · apply for trial](https://docs.byteplus.com/en/docs/faas/How_do_I_apply_for_beta_features?LibVersion=markdown备份版本)] Each sandbox instance can have a separate access address.<br><br><br>For description of sandbox instances, see [Sandbox instances](https://docs.byteplus.com/en/docs/faas/Sandbox_instances?LibVersion=markdown备份版本). |
   |APIG instance |Select an APIG instance. The sandbox application will use an APIG instance as the traffic entrance. |
   |Gateway service |Select the service that corresponds to the APIG instance. |
   |Route name |Specify a custom route name. The route name cannot be modified after being created. |
   |Path |Set a request path through which the sandbox application can be accessed. Only prefix matching is supported, and the path must start with `/`. |
   

5. After successful creation, click **Release** in the upper right corner of the Sandbox Application page to complete the deployment of the SandboxFusion sandbox service.


<span id="6FX8ARV9"></span>
## Verification results

After release, you can use the public address of SandboxFusion to verify the deployment of the application.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Log in to the created application, and on <strong>Basic Information \> Gateway Route Configuration \> Configuration Information \> Public Network</strong>, you can obtain the public access address of the application.</div>


<span id="bERxduW4"></span>
### Call the SandboxFusion service via API

Use the Curl command to call the API. The sample code for using the SandboxFusion service is as follows.

```Bash
curl 'https://****.apigateway-cn-beijing.volceapi.com/run_code' \
  -H 'accept: application/json, text/plain, */*' \
  -H 'accept-language: zh-CN,zh;q=0.9' \
  -H 'content-type: application/json' \
--data '{
    "code": "ls",
    "language": "bash",
    "files":{}
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Replace <code>https://****.apigateway-cn-beijing.volceapi.com</code> with the <strong>public access address</strong> of the SandboxFusion service.</div>


* <div data-tips="true" data-tips-type="default">Replace the values in the <code>data</code>field based on your business requirements. For related parameter prescriptions and examples, refer to the open\-source document <a href="https://bytedance.github.io/SandboxFusion/zh-Hans/docs/api/run-code-run-code-post/">Sandbox Fusion</a>.</div>



<span id="n8j2W3c2"></span>
### Access the SandboxFusion service via browser


1. Enter the **public access address** in the browser and access it.

2. Click the **Playground **  tab and select **Sandbox**.

3. In the Code textbox, select a programming language and enter your code, and then click Submit to submit the code.

4. After the execution is completed, view the result output.


<span id="XjDLg5uY"></span>
### Request SandboxFusion service via veFaaS function.


1. On the top navigation bar in the Function Service Console, select China (Beijing) region, and create the event function of the Python Runtime. For detailed description, refer to [Event function](https://docs.byteplus.com/en/docs/faas/Creating_event_functions).

2. After the function is created successfully, add the **public network access address** to the code under the **Code** tab on the function details page.

3. Save code updates and release functions. For details, refer to [Releasing functions](https://docs.byteplus.com/en/docs/faas/Release_function).

4. Conduct an online test. For detailed operations, refer to [Test function](https://docs.byteplus.com/en/docs/faas/Function_testing).

   The sample request parameters are as follows:

   ```Python
   "data": {
       "code": "print(\"Hello, SandboxFusion!\")",
       "language": "python"
   },
   ```
   

   The sample codes are shown below. For calling parameters of run_code interfaces in different languages, refer to [Run Code](https://bytedance.github.io/SandboxFusion/docs/api/run-code-run-code-post/).

   ```Python
   import json
   import http.client
   import re
   
   def handler(event, context):
       print("received new request\n")
   
       conn = http.client.HTTPSConnection("******.apigateway-cn-beijing.volceapi.com")
       headers = {
           'Content-Type': 'application/json',
           'Accept': 'application/json'
       }
   
       # Obtain request data
       reqBody = event["body"]
       reqData = json.loads(reqBody)
       code_str = reqData.get("code")
       language = reqData.get("language")
   
       # Default code
       if not code_str:
           code_str = "def reverse_string(s):\n    return s[::-1]\ninput_string = \"Hello, World!\"\nreversed_string = reverse_string(input_string)\nprint(\"the reversed string:\", reversed_string)"
       # Default language
       if not language:
           language = "python"
   
       # Call the sandbox run_code API to run the code
       payload = json.dumps({
           "compile_timeout": 30,
           "run_timeout": 30,
           "code": code_str,
           "language": language,
           "files": {}
       })
       conn.request("POST", "/run_code", payload, headers)
       res = conn.getresponse()
       data = res.read()
       response = data.decode("utf-8")
   
       # Extract result
       run_result = json.loads(response).get("run_result")
   
       # Response result
       result = {
           'statusCode': 200,
           'headers': {
               'Content-Type': 'application/json'
           },
           'body': json.dumps({
               'message': {
                   "result": run_result,
                   "language": language,
                   "code": code_str
               }
           })
       }
       return result
   ```
   


&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;
