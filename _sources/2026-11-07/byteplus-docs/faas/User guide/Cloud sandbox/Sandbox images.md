---
title: "Sandbox images"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Sandbox_images"
---

A sandbox image refers to the container image used to start a sandbox instance. You can select either custom images or ready\-to\-use public images.

<span id="HpL0xkmj"></span>
## Public images

BytePlus Function Service (FaaS) provides multiple public images for different sandbox applications. All public images have been preheated to ensure rapid image loading when creating sandbox applications, giving an out\-of\-the\-box experience.

Currently available public image types include:


* **All\-in\-One**: An all\-in\-one runtime environment image integrating various tools, designed to meet the efficient execution requirements of collaborative tasks across multiple AI Agent scenarios.

* **Code**: A dedicated image pre\-installed with mainstream compilers and code editors, providing a security\-isolated environment for code compilation, execution, and debugging.

* **Browser**: An image with a built\-in browser engine without a graphical interface and control APIs, suitable for browser\-related tasks such as web automation testing and data crawling.

* **Computer**: Standard Linux desktop/terminal, offering a complete Linux operating system environment and supporting standard Shell commands and desktop interactive operations.

* **Experiment**: Experimental sandbox environment for integrating and testing cutting\-edge or community\-driven Agent frameworks and runtimes (such as OpenCode, OpenClaw, and more), supporting rapid validation of new architectures, interaction modes, and capability orchestration mechanisms. Features may change or be unstable.

* **R2E\-Gym\-Subset**: R2E reinforcement learning environment subset, providing the core task environment of R2E (Request\-to\-Execution) for lightweight evaluation of Agent execution and feedback capabilities in specific scenarios.

* **WebArena**: Web interaction evaluation environment, built on the WebArena benchmark with real websites and task scenarios, offering a complete browser interface with GUI for assessing Agent comprehensive abilities in complex web browsing, information retrieval, and multi\-step GUI operations.

* **SWE\-bench**: [Beta \- apply for trial] A standardized testing environment specifically designed to evaluate the ability of AI models to repair software engineering code defects.


<span id="r2irzIl9"></span>
## Custom images

Custom images can be preheated to ensure sandbox applications start up within seconds.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Image preheating is an optimization technique in the container domain. It refers to pulling and caching the required container images to target nodes (such as K8s cluster worker nodes, edge nodes, and others) in advance before application deployment or container startup, thereby avoiding pulling from remote repositories during deployment. This shortens container startup time, reduces repository and network load, and improves deployment efficiency.</div>


The procedure for creating a custom image is as follows:


1. Log in to [Function Service Console](https://console.byteplus.com/vefaas).

2. On the top navigation bar, select the target region.

3. In the left navigation bar, select **Cloud Sandbox** \> **Sandbox Image**.

4. On the **Sandbox image** page, select the **Custom image** tab and click **Image preheating**.

5. On the **Image preheating** page, specify the images to be preheated. You can preheat multiple images at once.

   
   |**Parameter** |**Description** |
   |---|---|
   |Select an image source |Currently, only the images from the BytePlus Container Registry (CR) are supported. |
   |Select images |You can filter images by instance, namespace and repository to find the ones you need to preheat.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you select the filtered items on the page by ticking their checkboxes, the latest version of these images will be preheated by default. You cannot choose a specific image version in this scenario.</div><br> |
   |Preview |Select images to be preheated. You can clear all selected images at once or deselect a single one as needed. |
   

6. Click **Start preheating** to submit an image preheating task.

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Description   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the task submission fails, handle it according to the <strong>error message</strong>. If the issue persists, submit a <a href="https://console.byteplus.com/workorder/create">support ticket</a> to obtain technical support.   </div>
   

7. On the **Custom image** tab, you can view the status of preheating tasks. The status **Preheated** indicates the image has been downloaded successfully.
