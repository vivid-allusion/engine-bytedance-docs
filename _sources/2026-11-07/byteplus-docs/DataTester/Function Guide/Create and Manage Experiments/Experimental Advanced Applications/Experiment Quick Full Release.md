---
title: "Experiment Quick Full Release"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Experiment-Quick-Full-Release"
---

<span id="一-概述"></span>
## 1. Overview

For independent experiments in progress, closed, and debugging, users can transfer experiments into Features and publish it online.


* Independent experiments refer to experiments that have never been associated with a feature or created from any feature. Once the experiment is transferred into a feature, in order to avoid conflicts, other features cannot be associated.


**Prerequisites:**  Programming experiments with one parameter variable (boolean, string, number, and json) are currently supported, allowing experiments to transfer into Feature.

**Permission\-related**: Users with "collaborator permissions" on experiments can transfer into Features directly from independent experiments or one of the better experimental versions.

<span id="二-应用场景"></span>
## 2. Application scenario


* A version has been verified as a winning version by AB test and needs to be **released to the general public** online.

* The experimental results have been very significant, and it is hoped that the better version **will be greyscale released** online.


<span id="三-基本原则"></span>
## 3. Basic principle

The basic principles of experimental transformation into Feature are as follows:


* The current Feature and experiment are in a 1\-to\-many relationship, allowing multiple experiments with the same mutual exclusion layer to be opened on one Feature, and not allowing one experiment to transfer to multiple Features.

* Debugging, in progress (including frozen/unfrozen), and closed experiments can be transferred into Feature, and draft box experiments cannot be transferred into Feature.

* If an experiment transfers into a feature, the experiment is running, and the feature is turned on, then the experiment hit priority is higher than the feature hit priority. The specific impact is as follows:



|User |Is it an experimental audience? |Whether to enter the experimental traffic allocation |Featured Audience |Whether to enter Feature traffic allocation |Result |
|---|---|---|---|---|---|
|user1 |Yes |Yes |Yes & No |Yes & No |Hit experiment |
|user2 |Yes |No |Yes |Yes |Hit Features |
|user3 |Yes |No |Yes |No |Inaction |
|user3 |Yes |No |No |N/A |Inaction |
|user4 |No |N/A |Yes |Yes |Hit Features |
|user4 |No |N/A |Yes |No |Inaction |
|user5 |No |N/A |No |N/A |Inaction |


<span id="四-操作入口"></span>
## 4. Operation entrance

<span id="_1-实验列表页"></span>
### 4.1. Experiment list page

On the experiment list page, choose an experiment. On the experiment details page, then click "··· \- Experiment Quick Full Release", as shown below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/efc06637277d464080a2720f75abb43d~tplv-goo7wpa0wc-image.image) </span>

Follow the steps to publish the experiment.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e642eca916574db49eaef093d93d2b3e~tplv-goo7wpa0wc-image.image) </span>

<span id="五-固化至feature页面"></span>
## 5. Add to Features page

In the above entrance, transfer the experiment to a feature, that is, enter the Create/Edit feature page. Follow\-up process, you can refer to the process of creating features.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b44b8c34b15c471989e7256c72a724a7~tplv-goo7wpa0wc-image.image) </span>
