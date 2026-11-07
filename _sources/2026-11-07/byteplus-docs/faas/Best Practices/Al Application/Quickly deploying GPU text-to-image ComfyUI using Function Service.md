---
title: "Quickly deploying GPU text-to-image ComfyUI using Function Service"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Quickly_deploying_GPU_text-to-image_ComfyUI_using_Function_Service"
---

This article mainly describes how to run a ComfyUI text\-to\-image workflow in Function Service (FaaS).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">[<a href="https://docs.byteplus.com/en/docs/faas/How_do_I_apply_for_beta_features"><strong>Beta·Apply for trial</strong></a>]: The <strong>public images</strong>, <strong>Serverless GPU resources</strong> related to the Function Service ComfyUI text\-to\-image are currently in beta. If you need to use them, submit an application.</div>


<span id="n2vzYdXF"></span>
## Background information

[ComfyUI](https://www.comfy.org/) is an open\-source, node\-based, generative AI application program. FaaS provides ComfyUI public images to meet the demands of the application scenario of image and text generation.

The "**AI\-generated images\-ComfyUI**" public images provided by FaaS includes a GUI Workflow Demo that can be launched with one click.


* Start the GUI using [comfy-cli](https://github.com/Comfy-Org/comfy-cli).

* The default model [v1-5-pruned-emaonly-fp16.safetensors](https://huggingface.co/Comfy-Org/stable-diffusion-v1-5-archive/blob/main/v1-5-pruned-emaonly-fp16.safetensors) is mounted. If you need to mount your own model document, refer to [Mounting NAS file storage](https://docs.byteplus.com/en/docs/faas/Mount_FileNAS), and [Mounting TOS Torch Object Storage](https://docs.byteplus.com/en/docs/faas/Mount_TOS).

* A Custom node library containing [WAS Node Suite](https://github.com/WASasquatch/was-node-suite-comfyui).


This article shows to you how to run a ComfyUI text\-to\-image workflow in Function Service (FaaS). It mainly includes the following three steps:


1. Run the ComfyUI GUI workflow on FaaS.

2. Run the ComfyUI API workflow on FaaS.

3. Deploy ComfyUI API at scale on FaaS.


<span id="VH1ifKFC"></span>
## Prerequisites


* The [API Gateway](https://console.byteplus.com/veapig) product is activated.

* An API Gateway instance of the Serverless gateway type has been created. For detailed operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).


<span id="vKDQqE2O"></span>
## Part One: Run the ComfyUI GUI workflow

<span id="ioeaVEyz"></span>
### Step one: Create a GPU Web application


1. Create a GPU Web application.

   Log in to the [Function Service Console](https://console.byteplus.com/vefaas) and create a function of **Web application** type. Some parameter configurations are shown as below. For detailed operation instructions, refer to [Creating Web applications](https://docs.byteplus.com/en/docs/faas/Creating_Web_applications).

   
   |Parameter |Description |
   |---|---|
   |Function creation method |This article runs and calls the ComfyUI workflow through GUI and HTTP API, so select **create Web application**. |
   |Runtime |Select **Native** Runtime. |
   |Deployment method |Select **Container image** \> **Public image** \> **AI\-generated image\-ComfyUI**. |
   |Start command |It is recommended to maintain the default start command in the console: `/opt/application/run.sh`. This start command starts ComfyUI in the GUI form and listens on port 8000. |
   |Computation mode |Select **GPU acceleration**, and configure **GPU card type** according to actual resources and demands. |
   

2. Deploying ComfyUI application.

   1. After successfully creating a function, click **Release** in the upper\-right corner on the function details page. Then configure the lower limit and upper limit of the number of instances and the deployment method according to the practical demands of businesses. Finish the deployment of ComfyUI application. For detailed operations, refer to [Releasing functions](https://docs.byteplus.com/en/docs/faas/Release_function).

   2. The initial function release takes approximately one minute. Function Service will try cold\-starting instances and ensure that images can normally operate. Click the **Log** under the **Operation** column on the right side of instances to view detailed information.

3. Obtain the GUI link.

   1. Refer to [Creating API Gateway Triggers](https://docs.byteplus.com/en/docs/faas/Creating_a_API_Gateway_trigger), and obtain the GUI link for creating API Gateway Trigger of functions. For detailed operations, refer to [Creating API Gateway Triggers](https://docs.byteplus.com/en/docs/faas/Creating_a_API_Gateway_trigger).

   2. After successfully creating an API Gateway Trigger, you can obtain access address.

   3. Click the public network access address to view the GUI interface of ComfyUI in the browser.

4. Obtain the API Workflow through ComfyUI GUI.

   In the upper\-left corner of the GUI interface of ComfyUI, select **Workflow** \> **Export (API)** , then you can export the current workflow as the Workflow of API mode and download it locally. Later, you can convert the API Workflow into an API interface that can be directly called.


<span id="iNsuc7u9"></span>
## Part Two: Run ComfyUI API Workflow

After completing the operations in **Part One**, you know how to run ComfyUI GUI and export a currently developed API Workflow JSON file through ComfyUI GUI. You can convert the API Workflow file into an API that can be directly called, instead of directly exposing GUI to end users.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The "<strong>AI\-generated images\-ComfyUI</strong>" public images provided by FaaS includes an API Workflow Demo that can be launched with one click:</div>



* <div data-tips="true" data-tips-type="default"><code>api.py</code>: This is a Web Server based on FastAPI, and can create a <code>/predict</code> POST interface. It is used to execute the inference request of ComfyUI API Workflow.</div>


* <div data-tips="true" data-tips-type="default"><code>default_workflow_api.json</code>: This is a text\-to\-image API Workflow JSON file used for demos.</div>


* <div data-tips="true" data-tips-type="default"><code>run_api.sh</code>: This is a startup script for the API Workflow.</div>



<span id="dQ61X6Xi"></span>
### ComfyUI API Workflow principle

This section simply introduces how to convert the GUI application of ComfyUI into an API application that executes a designated Workflow through sample codes.

Before running the ComfyUI API Workflow in FaaS, you need to make several modifications:


1. Start a headless ComfyUI process in the background when launching the application.

   This can be realized through `comfy launch --background` of `comfy-cli`.

2. Compile a Web Server to create `/predict` interface, and execute the corresponding API Workflow.

   This can be realized through `comfy run --workflow`.


The following sample codes are only for reference. A simple Web service (`api.py`) that runs the ComfyUI API Workflow can be realized through FastAPI:


* Start ComfyUI first before starting the Web service through the `startup` event of FastAPI.

* Read the API Workflow file in the `/predict` interface. Modify the key parameters in the workflow according to requests and save them as a temporary file. Then use `comfy run --workflow` to synchronously execute the temporary file.

* Finally, read the generated images in the `output` directory and directly return.


```Python
from fastapi import FastAPI
import json
import subprocess
import uuid
from pathlib import Path
from fastapi import Response
from pydantic import BaseModel

class Predict(BaseModel):
    positive: str
    nagative: str = 'text, watermark'
    seed: int = 156680208700286

app = FastAPI()

@app.on_event("startup")
def startup_event():
    cmd = "comfy launch --background"
    subprocess.run(cmd, shell=True, check=True)

@app.get("/hello")
def hello():
    return {"Hello": "World"}
    
@app.post("/predict")
def infer(predict: Predict):
    workflow_data = json.loads(
        (Path(__file__).parent / "default_workflow_api.json").read_text()
    )

    # update workflow
    workflow_data["3"]["inputs"]["seed"] = predict.seed
    workflow_data["6"]["inputs"]["text"] = predict.positive
    workflow_data["7"]["inputs"]["text"] = predict.nagative

    # give the output image a unique id per client request
    client_id = uuid.uuid4().hex
    workflow_data["9"]["inputs"]["filename_prefix"] = client_id

    # save this updated workflow to a new file
    tmp_workflow_path = f"/tmp/{client_id}.json"
    json.dump(workflow_data, Path(tmp_workflow_path).open("w"))

    # comfy run
    cmd = f"comfy run --workflow {tmp_workflow_path} --wait --timeout 1200"
    subprocess.run(cmd, shell=True, check=True)

    # completed workflows write output images to this directory
    output_dir = "/root/comfy/ComfyUI/output"

    for f in Path(output_dir).iterdir():
        if f.name.startswith(client_id):
            img_bytes = f.read_bytes()
            return Response(img_bytes, media_type="image/jpeg")
```


<span id="FUBU0KRo"></span>
### Test API Workflow invocation


1. Change the startup script of GUI application into `run_api.sh` and then re\-deploy applications (release functions), then you can change GUI\-mode startup into API\-mode startup.

2. After redeployment, you can confirm that ComfyUI is started in the Background and listens to port 8188 through newly\-started instance logs. Because the listening port set by the function is 8000, so end users cannot access ComfyUI directly through the domain generated by APIG Trigger. They can only call the `/predict` interface created through the above steps.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_511ec1e2c2144acb025914a49a248ca4.png) </span>

3. Use Postman to test the API Workflow invocation.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a0b2c990a081d5667448bbb9f27799b1.png) </span>

4. View the specific log information of executing API Workflow and outputting results through instance logs.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ac25aa984514b88351fc02df20ed5f2c.png) </span>


<span id="BHlrjIsj"></span>
## Part Three: Deploy ComfyUI API on a large scale in FaaS

After **Part One** and **Part Two**, you know how to run ComfyUI GUI, export API Workflow file, and convert the API Workflow into an interface that can be directly called, and other methods, this section will deploy ComfyUI API on a large scale through the diverse concurrency management and Autoscale capability provided by FaaS.

This section mainly introduces how to deploy ComfyUI API on a large scale through the diverse concurrency management capability and Autoscale capability provided by FaaS.

<span id="7sb30PuR"></span>
### FaaS concurrency management and automatic scaling

Any code running in FaaS can utilize Serverless concurrency management and automatic scaling capabilities provided by the product.


* Enable a function instance to process multiple concurrent requests through setting **multiple concurrency per instance**. If the number of concurrent requests processed by one instance exceeds the set upper limit, then a new instance will be started.

* Through **turning off** multiple concurrency per instance (clearing the check box before **Enable** under the **Multiple concurrency per instance** parameter), a function instance only processes one concurrent request at one time, so the number of instances at one moment equals to the number of concurrent requests.

* Set the **maximum number of instances** to limit how many instances can start. This also limits the maximum concurrency that the current function can handle (maximum instances x maximum concurrent requests per instance).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">During development, set the <strong>maximum number of instances Max</strong> to 1 to avoid unnecessary charges.   </div>
   

* Set the **minimum number of instances** to keep some instances always running.


<span id="UVlfxV5x"></span>
### FaaS synchronous mode and asynchronous mode


* In synchronous mode, a request is always blocked until the business logic is fully executed. If concurrent requests exceed the service capacity (maximum number of instances × maximum concurrent requests per instance), an HTTP status code 429 (Too Many Requests) error is returned.

* In asynchronous mode, there will be an immediate response after submitting the request. If concurrent requests exceed the service capacity, FaaS ensures all requests execute normally through an internal "request queue".


<span id="AUrubC0d"></span>
### Conduct load testing using Locust

<span id="Fn03KaJ7"></span>
#### Locust load testing environment configuration

In the demonstration scenario, it is recommended to **turn off** the **multiple concurrent requests per instance** of ComfyUI API function (thus, a function instance can only process one request at one moment), and set the maximum number of instances to five. Thus, the maximum capacity of the function at one moment is five concurrent inputs.

The following text will use Python load testing library Locust to simulate network traffic sent to the ComfyUI application. Install Locust and Locust plugins through the command `pip install locust locust-plugins`. The sample codes are shown below. Create and write the `locustfile.py` file under the load testing directory:

```Python
# locustfile.py
from locust import HttpUser, task

class TestPredict(HttpUser):
    @task
    def hello_world(self):
        self.client.post(
            "/predict",
            json={
                "positive": "1cat",
                "negative": "text, watermark"
            }
        )
```


Run the `locust -i 100` command in the directory containing the `locustfile.py` file to open the GUI webpage of Locust, where you can specify the number of concurrent users you want to simulate. Each "virtual" user will submit a POST request to ComfyUI APIG Endpoint at `/predict`.

<span id="aUqFOi7D"></span>
#### Scenario 1: Synchronous mode, 100 requests, concurrency 5


1. Assume that you set the Number of users parameter (virtual users, i.e., concurrency) to 5 and enter the APIG domain to test the request handling status of the application under the maximum capacity limit.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8e16b449196ab7aa20783f2498c7a5d7.png) </span>

2. You can see from the test results that since the load is within the capacity limit of the application, all the requests can be processed normally.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8be93abd4b1d93e39c516f8f4577a93c.png) </span>


<span id="JNwKX2Rs"></span>
#### Scenario 2: Synchronous mode, 100 requests, concurrency 10


1. Set the Number of users (concurrency) to 10 and run the test.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3d92c6a840b740978fa177f4bd511e5e.png) </span>

2. You can see from the test results that the concurrency of 10 exceeds the maximum capacity limit of the service, so many requests will fail.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9982f1b41937d2e0d49e025549d82cc7.png) </span>

   On the Failures tab, you can see that many requests are returned with 429 error code.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8260ece9018e0eafbf0a856404f27508.png) </span>


<span id="OP7d1ZK7"></span>
#### Scenario 3: Asynchronous mode, 100 requests, concurrency 10

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If you need to verify or use the concurrency load testing under the asynchronous mode, you need to create a function and turn on the <strong>asynchronous task</strong>. After successfully creating the function, the configurations of the asynchronous task cannot be modified.</div>



1. When creating the function, turn on the **asynchronous task**. Keep the remaining configurations consistent with the contents in **Part One** in the above text.

2. After creating the asynchronous task function, continue to execute the operations in **Part Two** and **Part Three** in this article, to complete the preparation before load testing.

3. Same, use the concurrency of 10 to conduct load testing. You can see from the results that on the asynchronous task tab, requests are waiting to be processed in the queue.

   ComfyUI application can only process up to five requests at the same time, but FaaS asynchronous mode can help you to queue requests and process them one by one. After a period, all 100 requests have been processed completely.

4. This is the execution status of 100 requests when the verified concurrency is 10 in the Locust. The results show that 100 requests all succeed in asynchronous mode.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8ef757c6b13d8a9f88f233ceac9c8b0f.png) </span>

5. When you view the execution history of asynchronous tasks, you can see that the cold start requests will take about 16 seconds to complete execution, but the subsequent requests will repeatedly use the instances started, thus this will take about only one second.
