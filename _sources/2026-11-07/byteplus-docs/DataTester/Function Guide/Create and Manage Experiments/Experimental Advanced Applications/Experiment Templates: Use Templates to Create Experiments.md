---
title: "Experiment Templates: Use Templates to Create Experiments"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Experiment-Templates-Use-Templates-to-Create-Experiments"
---

DataTester provides you with the experimental template function. The experimental template can quickly set some form items that must be filled in when the experiment is created, or force the values in the form items to be solidified. This will make it easier for the entire group to control the form during construction experiments, and improve the clarity of understanding of the form items. This article introduces the operation guide of the experimental template function.

<span id="f3e08b10"></span>
# Precautions

Only role users with permissions related to the experimental template can use the experimental template feature.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b4ba3693f0f49ee9cb4740004c4eb89~tplv-goo7wpa0wc-image.image) </span>


* View/use experimental templates: You can view the list of experimental templates and use templates.

* Add /configure experiment templates: You can create and manage experiment templates.


<span id="4c8948ec"></span>
# Create and manage experimental templates

<span id="72f7a42f"></span>
## Create an experiment template


1. Log in and enter the DataTester console, click **Open Capabilities** \> **Experiment Templates** in the left navigation bar, enter the Experiment Templates page, and click the **New Template** button in the upper right corner to create an experiment template.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e78c8e9078df4f70873ac974b10865a9~tplv-goo7wpa0wc-image.image) </span>

2. Configure the use of template parameters on the pop\-up page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d7fc1bd007d744cf91dbc13836381047~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Configuration instructions |
   |---|---|
   |**Template Name** & **Business Background** |Customize the **template name** and **business background**. When subsequent experimenters refer to the template to create an experiment, they can identify which template should be used and whether to serve business requirements through the template name and business background. The business background can be configured as: [xxx version function iteration dedicated]. |
   |**Type of experiment** |According to business needs, choose the experimental template\-\-**programming experiment \- server side** or **programming experiment \- client side** experimental template. |
   

3. Click **Create and enter the template editor**, the page jumps to the detailed parameters page of the experimental template, and configures the detailed experimental parameters of the experimental template.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/af2af9a450cd42e1974118ab412fe93a~tplv-goo7wpa0wc-image.image) </span>

   * The experimental template parameter configuration is consistent with the experimental parameter configuration for creating a normal programming experiment, see for details [Programming Experiment](https://docs.byteplus.com/docs/DataTester/Programming-Experiment).

   * There are settings for each experimental parameter at the top right of the experimental template parameter page. You can set **whether it is solidified** or **disabled** according to your needs.

      * **Whether to solidify:**  Whether to use the parameter content configured in the experimental template as the initial value of the template. When the template is referenced to create an experiment, this value will be filled directly.

      * **Whether to disable:**  If the parameter is turned on and disabled, the parameters cannot be changed when the reference template is created, which can prevent some key parameter configuration results from being changed.

4. After completing the experimental template parameter configuration, click **Save Configuration** in the upper right corner to complete the experimental template creation. The page returns to the experimental template page, and you can view the created experimental template.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6788edd9665941c2884f9162d6eaf8d9~tplv-goo7wpa0wc-image.image) </span>


<span id="12340a74"></span>
## Edit/modify the experimental template

You can edit, copy, and delete the created experimental template on the experimental template page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a06fd46b3d5545b9ac6ff081aca56128~tplv-goo7wpa0wc-image.image) </span>


* The mouse is suspended on the experimental template. You can click on the **template configuration** to jump directly to the experimental template parameter configuration page, and you can directly modify the configuration of the experimental parameters.

* The mouse hovers on the edit button in the upper right corner of the experimental template, and the **edit**, **copy**, and **delete** buttons will be displayed. You can click the corresponding buttons to operate as needed.


<span id="1f2ae3b4"></span>
# Use experiment template

After creating the experiment template, when subsequent experimenters create experiments, they can directly reference the created experiment template in the experiment list to create experiments.


1. Log in and enter the DataTester console, click **A/B Testing** \> **Experiment List** in the left navigation bar, and click the  **+ Use Templates** button in the upper left corner of the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a6abb5f9edf4faa9f1219c82349e92e~tplv-goo7wpa0wc-image.image) </span>

2. Find the experimental template you want to reference in the pop\-up page (support searching for the experimental template title or description at the top right), and click **Apply** at the back.

3. The page jumps to the experimental parameter configuration page for creating the experiment. The parameters in the page are pre\-filled according to the experimental template you choose to refer to. You can adjust and modify them according to the actual experimental needs, and then complete the experimental creation.


<span id="9b66a62a"></span>
# Applied Practice

<span id="734271a0"></span>
## **Practice 1: Lock the initial type of the experimental key to JSON to improve efficiency**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f9101661fe3f4a57af556ca566a7e703~tplv-goo7wpa0wc-image.image) </span>

<span id="24b24dc8"></span>
## **Practice 2: Solidify some default tick indicators and automatically tick them when creating experiments in templates**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cabfd569639f4744bf4c3b3fa8e70241~tplv-goo7wpa0wc-image.image) </span>
