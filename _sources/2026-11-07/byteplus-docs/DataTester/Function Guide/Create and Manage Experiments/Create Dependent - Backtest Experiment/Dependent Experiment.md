---
title: "Dependent Experiment"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Dependent-Experiment"
---

A dependent experiment refers to splitting traffic to open a new experiment (child experiment) among users who hit an experimental group in an existing experiment (parent experiment). This article introduces the application scenarios and operation points of DataTester's dependent experiment.

<span id="应用场景"></span>
# Application scenario

**Core scenario:** 

It is necessary to continue to delineate users for the exploration of new experiments based on the "enrollment population" of an already started experiment. The features are as follows:


* The parent experiment cannot be closed to identify the base user of the child experiment.

* Multiple child\-experiments can be opened, multiplexing the traffic of the selected parent experimental group.

* The dependent experiment is a different function, that is, all users of the child experiment inherit the configuration (function) of the parent experiment, and use the child experiment to see the superposition effect.

* The data of the parent experiment cannot be seen, and the conclusion has no reference significance due to the strategic influence of the quilt experiment.

* On top of a running experiment, we want to simultaneously verify the combined effect of a second function/strategy.


**Business Scenario:** 


* For news apps, the parent experiment is whether to open an "entertainment" channel to users. Subsequent to the product iteration process, child\-experiments will be launched on this basis, and different functional layouts and styles will be provided for users in the experimental version of the "entertainment" channel that has been opened to observe the user's usage time and retention.

* For e\-commerce platforms, shopping carts are designed with three button styles (A1, A2, A3), and checkout page CTA buttons are designed with three styles (B1, B2, B3). Product managers hope that each style of shopping cart and checkout page CTA corresponds one by one. For example, users who see A1 can only see B1 after entering the checkout page, and so on. At this time, you can open the parent experiment A in the shopping cart, and open the child experiment B on the CTA button of the settlement page, and the traffic of the experimental version will be inherited one by one.


<span id="创建父子实验"></span>
# Notes and Prerequisites

<span id="14e6a2af"></span>
## **Prerequisite**

Access client side SDK or server level SDK, see below [Data Access Overview](https://docs.byteplus.com/docs/DataTester/Data-Access-Overview).

<span id="基本原则"></span>
## Basic principle


* The child experiment life cycle must be included in the parent experiment life cycle, that is, there are running child experiments, and the parent experiment cannot be shut down.

* The parent experiment and the child experiment have a 1\-pair N relationship, and the child experiment, the parent experiment and the child experiment cannot be located on the same mutual exclusion group.

* The parent\-child experimental model can be different.


<span id="创建限制"></span>
## Creation limit


* Currently, only "programming experiments" in the running state are supported as parent experiments.

* The type of dependent experiment should be the same, the client\-side child experiment can only inherit the client\-side parent experiment, and the service terminal experiment can only inherit the server\-level parent experiment.

* Grandchild experiment is not supported: The parent\-child relationship currently only supports two levels, does not support multi\-level, and does not support ring formation.

* Permission restrictions: Non\-experimental collaborators cannot open child\-experiments based on that experiment.


<span id="d67ac420"></span>
# Create a dependent experiment

<span id="常规父子实验"></span>
## Routine parent\-child experiment

<span id="_1-创建入口"></span>
### Step 1 Create an entry

The collaborator of the parent experiment, click the target parent experiment in the "Experiment List" to enter the details page, click "More", and select "Start Dependent Experiment" from the drop\-down list. As follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/121d1d1982e247ebb3f1530e25247e4c~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-填写基本信息"></span>
### 2. Fill in the basic information

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a8bf596fbdfa475ea656d15a7f03f5ea~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-设置生效策略"></span>
### 3. Set the effective policy

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e25dfc039331404a8825b6230f0a533c~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-配置实验版本"></span>
### 4. Configure the experimental version

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9926049d4dfa43ff9a855de87025e91e~tplv-goo7wpa0wc-image.image) </span>

**Associated Parent Version:** 


* The experimental version of each child experiment can be associated with multiple specific versions of the parent experiment, or choose to "not inherit the experimental version".

* The experimental version of the parent experiment refers to the implementation mechanism of the filter audience filter condition, and filters the traffic entering the child experiment.


**If the group cannot enter the group, it means checking "Traffic changes will not affect the assigned incoming users, but will only take effect for users who have not yet entered the group".** 

**In the parent\-child experiment, whether to check "enter the group but not the group" has the following effects on the flow of the child experiment:** 


|**Serial number** |**Parent experiment "in group and not out of group".**  |**Child experiment "in group and not out of group".**  |**Product logic and behavior** |
|---|---|---|---|
|1 |Yes |Yes |Both parent and child experiments record the status of users entering the group. Once they enter the group, no matter how the traffic changes in the future, the user will not be out of the group. |
|2 |Yes |No |The parent experiment records the user's entry status, but the child experiment does not. The incoming traffic of the child experiment must hit the parent experiment. When the traffic of the child experiment changes, the incoming users of the child experiment may be out of the group. |
|3 |No |Yes |The parent experiment does not record the status of the user entering the group, and the child experiment records the status of the user entering the group. Once a child experiment user is in the group, the child experiment will remain in the group state even if the parent experiment is out of the group. |
|4 |No |No |The parent and child experiments do not record the status of users entering the group. The traffic change of the parent experiment and the user leaving the group caused by the filtering conditions will also affect the child experiment. |


<span id="_5-添加实验指标"></span>
### 5. Add experimental metrics

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0fa9ddf9d6224b7b838523945afcec6e~tplv-goo7wpa0wc-image.image) </span>

<span id="_6-查找父-子实验"></span>
## Find Parent/Child Experiment

Parent/child experiments can be found on the Experiment Reports page, Report Overview, as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/206d81408cb64e0cb638af81fdc1b63d~tplv-goo7wpa0wc-image.image) </span>

<span id="实验血缘族谱"></span>
## Experimental lineage

The parent\-child experiments will influence each other, and the corresponding experimental results will also be correlated to a certain extent.


* From the perspective of child\-experiments: The parent experiment as a filter condition will affect the incoming flow of child\-experiments.

* From the perspective of the parent experiment: the parent experiment is relatively passive, and its traffic will be polluted by the child experiment that is opened later.


Therefore, providing a family tree diagram of the experimental bloodline can provide a more comprehensive reminder of the child experiments of your current parent experiment, so as to facilitate your scientific decision\-making.

After the flow configuration type of dependent association experiment, the family tree of each experiment is displayed, and the current experiment and its parent experiment, brother experiment, child experiment and the solidified features of each experiment are displayed to show the experimental\-level inheritance relationship. As follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/39eeb3421a7042149a03249fe821072d~tplv-goo7wpa0wc-image.image) </span>
