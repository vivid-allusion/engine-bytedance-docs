---
title: "Integrated Workbench"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Integrated-Workbench"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This function is supported by version 4.4.0 or above. This function is a paid function. If you want to use it, you need to contact your Customer Success Manager for consultation.</div>


<span id="一、概述"></span>
# 1. Overview

In the scenario where the enterprise system functions are more complete, there are many systems, such as CDP, CSM, recommender system, operation system, etc. Enterprises hope to connect the capabilities of DataTester with their own systems to reduce multiple jumps between systems. The integration workbench provides different integration templates to support customers in integrating DataTester's capabilities into customer\-owned systems through a process\-guided approach, effectively solving such problems.

<span id="二、功能介绍"></span>
# 2. Function introduction

<span id="_2-1集成工作台"></span>
## 2.1 Integrated Workbench

Menu to "Open Capabilities \> Integrated Workbench"

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/85eeda4da7ac487499350e7432267879~tplv-goo7wpa0wc-image.image) </span>

<span id="新建定制"></span>
### New **Customization**

Click **New Customization**, fill in the information and select the integrated template type, and click Save

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5fe5833106b6443e88179cddb2d6b5b0~tplv-goo7wpa0wc-image.image) </span>

Next, we went to the custom editing page.

<span id="页面配置能力"></span>
### Page configuration capability

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa560482911d44d78ce156b4b26c4b0a~tplv-goo7wpa0wc-image.image) </span>

When clicking on the configurable blue area, the configuration panel is displayed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c97471c6a774692bcff80042cdc5693~tplv-goo7wpa0wc-image.image) </span>

If you think it is cumbersome to switch the configuration area each time, you can directly click the title at the top of the configuration panel to switch to the root node. Some configurations will only exist at the root node.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d89bd028a268459d8d7704dda9b2bacc~tplv-goo7wpa0wc-image.image) </span>

**The supported configuration pages are**


* list of experiments

* experimental report


The supported configuration items are as follows:


|Page |Parameter value |Description |
|---|---|---|
|list of experiments |isSkipCreateExperimentModal |Skip the experiment creation mode pop\-up |
||defaultNewExperimentMode |default jump experiment |
||hiddenExperimentModes |Hidden experimental mode |
||headerModule.hidden |Hidden Header Module |
||headerModule.title |title |
||headerModule.barHidden |Help information hiding |
||headerModule.createHidden |Create button hide |
||tableModule.filterHidden |Filter module hide |
||tableModule.operationHiddenKeys |Table operation hidden item |
|experimental report |hiddenAsyncTask |Hide asynchronous query task |
||hiddenFlightToFeature |Hidden Experiments Curing to Features |
||hiddenMetricSwitch |Hide switching between global and detailed metrics views |
||hiddenCustomFilterBox |Hide custom filter templates |
||initTabKey |Initialized lab reports tab |
||hiddenTabKeys |Lab report tab hidden keys |


<span id="_2-2-主题色定制"></span>
## 2.2 Theme color customization

Click the "Theme Configuration" button on the right side of the top guide to display the theme color configuration panel.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/864479b9d72a4d76860eea4b6140b30e~tplv-goo7wpa0wc-image.image) </span>

**The theme color configurations supported in this issue are**


* main color

* Text color

* border color


<span id="_2-3-表单搭建能力"></span>
## 2.3 Form building capabilities

When entering the experimental creation page, "Enter the experimental creation and construction" is suspended at the top, and you can enter the form construction page;

Note: Currently only supports **programming experiments**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/769a81b70f4c425fb8326e80c415b86d~tplv-goo7wpa0wc-image.image) </span>

initialization page

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4225424cccdb4b7a9f0cf67df1863397~tplv-goo7wpa0wc-image.image) </span>


1. Top navigation: Action bar, providing save, preview, close/open form configuration capabilities, retracement/restore, and the ability to view the linkage diagram between components

2. Library: Provide the most basic forms to build atomic components

3. Material Tree: The sequential structure of the components that currently make up the experimental creation page

4. Property configuration: configure the display style of each component, support functions and teaching and research, linkage capabilities

5. Canvas: real\-time display, current form build product


<span id="步骤"></span>
### **Steps**


1. Click on the component in the material library and display it in the middle panel. At present, the most basic programming experiment configuration will be preset;

2. Configure the properties of the component, you can hide the component, you can click the component tree on the left to open the corresponding configuration panel;


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a04173ff2c714649842b4beada0e5d12~tplv-goo7wpa0wc-image.image) </span>

Different components correspond to different configuration capabilities.

The following are some basic configurations, with different components having their own specific supported configuration capabilities:


|Property |Default value |Description |
|---|---|---|
|key |without |Corresponding to the key in the experimental creation interface |
|title |without |Corresponding to the left display label |
|default value |without |component initial value |
|editable |true |Can it be edited? |
|hide |false |Whether to display the component, unlike deleting the component, the component's value is stored in the form |
|validation rule |{} |Provides basic and custom validation capabilities for component values |
|linkage rule |without |Provide linkage capability configuration between various components, currently only supports linkage of component values |



3. Verification and configuration of components


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a012fee96d804584b2e3a2f4da667d27~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb0305bceb964fe3a1bb4df4daf36a7c~tplv-goo7wpa0wc-image.image) </span>

JSON schema

Custom function, return true pass, string error message

<span id="联动逻辑规则"></span>
### **Linkage logic rule**

Currently only active mode is supported

You need to understand the value composition of each component to avoid the problem of not finding the value

$Self.value: Refers to the component value of the current component $target [\*] .value: Refers to the component value of the target component, its subscript can be any number (these numbers are the component order selected in the selection box, increasing from 0) such as $target [0] .value

```json
For example, when the experimental type changes, the mutual exclusion layer is cleared
Select the experimental type component, create one at the linkage rule, select the mutual exclusion layer component as the target component, and set the linkage type to value
Linkage value：{ 
     ...$target[0].value, 
     layer: '', 
   }
```


Example:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/58f6ab96e7574c96897b9335143a62e9~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a2f12edf332f4eea98c51363a5ab0515~tplv-goo7wpa0wc-image.image) </span>

<span id="预览配置项"></span>
### **Preview configuration item**

Enter through the "Preview" button in the operation bar.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a0d155094b0244d9a8761e1ced4f6f66~tplv-goo7wpa0wc-image.image) </span>

<span id="创建-编辑-详情编程实验"></span>
### **Create/edit/detail programming experiments**

Precondition: The "On" switch in the operation bar is turned on.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3e83f15e51f4f6bbd9bca6fb36339bf~tplv-goo7wpa0wc-image.image) </span>

<span id="三、功能应用-接入引导"></span>
# 3. Functional application & access guidance

<span id="_3-1功能应用"></span>
## 3.1 Functional application

After the integration is successful, you can view the integrated DataTester page on your own page.

<span id="_3-2接入引导"></span>
## 3.2 Access guidance

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/674d45fc9b3e4debaa7d4ad42211dc3a~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2650925bdd6541db92228fe50e088d13~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec43588b3da146bb8fa3ba4d397d4d54~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/74f8fa0a385e4c2991797fe14f09d76b~tplv-goo7wpa0wc-image.image) </span>

<span id="四、权限管理"></span>
# 4. Permission management

Support the control of integrated workbench operation permissions for different roles in "Global Settings \- Rights Management", which can control the permissions that can only be viewed, edited and viewed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b28ad4fccd84e58bf3a332893af15ce~tplv-goo7wpa0wc-image.image) </span>
