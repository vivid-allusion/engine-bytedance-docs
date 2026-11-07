---
title: "Approval and Workflows"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Approval-and-Workflows"
---

<span id="32aa4839"></span>
# Overview

In order to pursue stable iteration, do not want some radical strategy of experimental opening or rolling out 100% affect the product, the general Feature release of these online operations, is the need for approval and Review mechanism; and some rapid iteration of business, emergency bugfix, you want to be able to quickly go online, do not want more process blocking. Combining the demands of different business security and flexibility, we support different businesses to configure different workflows, including approval as a part of the workflow.


* **Scenario 1: Experimental Solidification of Important Features**

   A short video APP plans to introduce live broadcast function, first open the experiment for a period of time after the results of remarkable conclusions, plans to solidify the experiment as Feature release roll out 100%. However, the live broadcast function is a large function iteration, which needs to be operated cautiously, so it is hoped that the experimental solidification of such important functions needs to be approved by the business line administrator, and then gradually gated release after approval.

* **Scenario 2: Feature release of emergency bugfix**

   The login function of an APP has a flash back phenomenon. After inspection, it is found that there is a small bug. After being fixed, it is verified in the testing environment. If you want to quickly release the full amount of this Feature and quickly reduce the user experience problem, you need to release it quickly. Do not want more processes such as approval.


<span id="7ae166e7"></span>
# Terminology

Workflow: The operation process of different businesses composed of different links, such as experimental opening, experimental solidification Feature, and Feature, are all different workflows. Examples are as follows:


* Experiment opening: ① New experiment \- \> ② Approval \- \> ③ Successful opening

* Experimental Solidification Features: ① Generated Features \- \> ② Set Release Plan \- \> ③ Approval


<span id="99a50a86"></span>
# Use workflow

<span id="64dd8789"></span>
## **1. Workflow management**


* Function entrance: [Global Settings] \- [Workflow Management] \- [Process Settings]


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6611e909f525484290bdae4912b62bbd~tplv-goo7wpa0wc-image.image) </span>


* The current default is the following four workflows.

   * Feature Release Process

   * experiment start process

   * Experiment Transfer to Feature Flow/Experiment Quick Full Release

   * Features Open/Close Process

* What steps are included in the workflow, which are uniformly configured by the administrator of the application

   * You can click Edit to choose to open or close certain links. The links opened by default cannot be closed.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5c6f0ee9df9454abe519cd2183a3b18~tplv-goo7wpa0wc-image.image) </span>


<span id="25475d47"></span>
## **2. Workflow takes effect**

After the app administrator has configured the workflow, the operations under the app will be executed according to the corresponding settings. For example, if the release of a Feature is set with ① setting the release plan \- \> ② approval, the release of the Feature will be carried out according to the process of ① setting the release plan \- \> ② approval. After the process is completed, the Feature release will take effect online.

<span id="41f32665"></span>
## **3. Approval**

**Approval settings**


* In the workflow management, turn on the approval switch, which adds an approval link to the process.

* Click on the approval steps to set the approval plan.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5559a843b1e54727b84fcd8586422903~tplv-goo7wpa0wc-image.image) </span>

   * Approval level: The current default level 1 approval

   * Add default approval members: You can add by role or person. After adding, the process of this type of task requires approval from these approval members by default

   * Pass mechanism: Currently, the default is 1 person passes and passes.

   * Rejection mechanism: After the current default rejection, the approval needs to be restarted.


**Approval task management**


* The task of initiating approval can be viewed uniformly in System Management \> \> Approval Management

* Personnel with approval authority can approve the approval task


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dbdb09d936794892b9775cd6b7ad10a3~tplv-goo7wpa0wc-image.image) </span>
