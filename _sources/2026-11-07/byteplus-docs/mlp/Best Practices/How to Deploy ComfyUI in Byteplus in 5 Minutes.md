---
title: "How to Deploy ComfyUI in Byteplus in 5 Minutes"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/How_to_Deploy_ComfyUI_in_Volcano_Engine_in_5_Minutes"
---

<span id="前言"></span>
# Introduction

Machine learning cloud platforms provide users with powerful AI algorithm development tools, integrating cloud\-native tools and computing power (GPU, CPU cloud servers) to accelerate the development and deployment process. This case aims to demonstrate how to quickly deploy ComfyUI using MLP to achieve efficient image generation and processing.

<span id="快速体验"></span>
# Quick Experience

<span id="demo"></span>
## DEMO


* Source code referenced in this practice: [GitHub - ComfyUI_examples](https://github.com/comfyanonymous/ComfyUI_examples/tree/master/sdturbo)


<span id="预期结果"></span>
## Expected Result

After filling in all parameters and the Prompt, click Queue Prompt to get the image output.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b81d444d547d04b855c5604d75765421.png) </span>

<span id="快速部署实践"></span>
# Quick Deployment Practice

<span id="前置依赖"></span>
## Prerequisites

This solution takes ComfyUI as an example. Before starting operations, confirm you have completed the following preparations:


* Confirm you have completed the configuration in [Quick Start](https://docs.byteplus.com/en/docs/mlp/Quick_Start).

* Confirm the computing power status of the current available queue. It is recommended that the queue has any GPU resources; CPU image generation may take a lot of time

* Ensure there is a public network type load balancer instance in the availability zone where the computing power is located. If not, go to the [Load Balancer Console](https://console.byteplus.com/clb/region:clb+cn-hongkong/LoadBalancer?) to create one (online service dependency)


<span id="方式一：开发机部署"></span>
## Method 1: Deployment on Development Machine

<span id="step1：创建开发机"></span>
### Step 1: Create Development Machine

Access the development machine [Console](https://console.byteplus.com/ml-platform/devinstance/create), create a development machine and deploy resources. Key configurations are as follows:


1. Resource specification: configure the following resource specifications.

   * CPU instance: 8C/64G/20GB cloud disk.

   * GPU card quantity: at least 1 card; best practice is to use one ml.gni3.

2. Image: select the image URL and enter `vemlp-demo-cn-shanghai.cr.volces.com/demo/comfyui:v0.2.3`

3. Access port: turn on at least one of SSH/WebIDE; this practice selects WebIDE. And add a custom port \- listening port 8188; ensure the security group has opened up 8188.

4. After confirming creation, automatically jump to the development machine details page. Because the pulled image is large, the first development machine creation time is estimated to be 10 minutes.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9f4b271ab06643c7935cf4ebfe7a1948~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec313500569a448cba84ed3dc86d0c45~tplv-goo7wpa0wc-image.image) </span>

<span id="step2：部署-comfyui-并下载样例模型"></span>
### Step2: deploy ComfyUI and download the sample model

Execute the following commands in the development machine; when downloading the model, execute the corresponding intranet download command according to the Region where the development machine is located. Among them, the intranet single\-stream download speed of the model is approximately 50MB/s, and it is expected to take about 2 minutes. Note that the service is started on 0.0.0.0:8188.

```bash
cd ~/code/ComfyUI/models/checkpoints
# East China 2 (Shanghai): Run the following command to download
wget vemlp-demo-cn-shanghai.tos-cn-shanghai.ivolces.com/models/sd_xl_turbo_1.0_fp16.safetensors
# North China 2 (Beijing): Run the following command to download
wget vemlp-demo-cn-beijing.tos-cn-beijing.ivolces.com/models/sd_xl_turbo_1.0_fp16.safetensors
python ~/code/ComfyUI/main.py --listen 0.0.0.0
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ede45665e048df2220cf297c2a4daafe.png) </span>

<span id="step3：访问-comfyui-服务"></span>
### Step3: Access the ComfyUI service

In the Terminal, Command+click http://0.0.0.0:8188, or obtain the access address from the development machine details page \- Access Configuration and open it in a browser to enter the ComfyUI service interface.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4f5533bd484b45abafe78ece6c0ffabb.png) </span>

<span id="step4：导入样例-workflow-并生图"></span>
### Step4: Import the sample Workflow and generate images


1. First, save the sample picture.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8dd2c8b511400eb8f00e8f1aed2a76ed.png) </span>

2. On the ComfyUI interface, load the sample picture (or drag the file into the interface) to import the Workflow.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1393bd83beb945da894432369ad0e807.png) </span>

3. Click Queue Prompt in the top\-right corner; the first inference may need to wait for approximately 1 minute.

4. After deployment is completed, log output is visible in the development machine, and image output is visible on ComfyUI.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_59f1924331aa2f49e6f3569ea0a0dac3.png) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a7ef386891e8b9011bb5914bd0f8c955.png) </span>

<span id="方式二：在线服务部署"></span>
## Method 2: Online Service Deployment

<span id="step1：创建在线服务"></span>
### Step 1: Create an online service

Enter the online service [console](https://console.volcengine.com/ml-platform/region:ml-platform+cn-beijing/serviceNew/create), create an inference service and deploy resources. Key configurations are as follows:


1. Image: Select the image URL and enter `vemlp-demo-cn-shanghai.cr.volces.com/demo/comfyui:v0.2.3`

2. Entry command: You need to execute the corresponding internal network model download command according to the Region where the online service is located.


```bash
cd ~/code/ComfyUI/models/checkpoints
# East China 2 (Shanghai): Run the following command to download
wget vemlp-demo-cn-shanghai.tos-cn-shanghai.ivolces.com/models/sd_xl_turbo_1.0_fp16.safetensors
# North China 2 (Beijing): Run the following command to download
wget vemlp-demo-cn-beijing.tos-cn-beijing.ivolces.com/models/sd_xl_turbo_1.0_fp16.safetensors
python ~/code/ComfyUI/main.py --listen 0.0.0.0
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In production business, it is recommended to pull the model by mounting shared storage vePFS/SFCS to ensure expansion efficiency.</div>



3. Subnet and security group: In the security configuration, ensure that port 8188 is opened.

4. Port: Add a custom port, set the listening port to 8188, and the calling port can be selected arbitrarily.

5. Load balancer: The load balancer created in  **「Prerequisites」** 


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23824945089744a1928b0a63e4aafdcf~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/81bb5e66b2af4805b089954925d64700~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/297a50cdf7f74b068cf6fd939bae1f2e~tplv-goo7wpa0wc-image.image) </span>

After completing the above configurations, you can view in the 【Service Details Page \- Logs】 that the single\-stream download speed of the model over the internal network is approximately 50MB/s, and it is expected to take about 2 minutes. Note that the service starts at 0.0.0.0:8188.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b582ae18f89a4273a570210b7916ea6e~tplv-goo7wpa0wc-image.image) </span>

<span id="step2：访问-comfyui-服务"></span>
### Step 2: Access the ComfyUI service

Go to the created online service's [Details Page \- Call Guide], obtain the public network access address, and open it in a browser.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a7c1a1753f9e48f0b9b1dd5015bc7947~tplv-goo7wpa0wc-image.image) </span>

<span id="step3：导入样例-workflow-并生图"></span>
### Step3: Import the sample Workflow and generate an image


1. First, save the sample picture.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8dd2c8b511400eb8f00e8f1aed2a76ed.png) </span>

2. Load the sample picture on the ComfyUI interface (or drag the file into the interface) to import the Workflow.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1393bd83beb945da894432369ad0e807.png) </span>

3. Click Queue Prompt in the top\-right corner; the first inference may take about 1 minute.

4. After deployment is completed, log output is visible in the development machine, and image output is visible on ComfyUI.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8b1de9b4b35d066cdbff16d4ea05ee99.png) </span>
