---
title: "Label management"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Label_management"
---

Resource Label consists of a set of key\-value pairs. You can classify and aggregate cloud resources from different dimensions with resource labels, and they are also used in scenarios like label\-based authorization and cost allocation. This article will guide you on how to use labels in FaaS.

<span id="label-type"></span>
## Label type


* System labels: Labels that the system automatically adds to a resource when it is created are called system labels, generally starting with `sys:`. System labels can only be viewed, not edited.

* User labels: Labels that you manually add to a resource are called user labels. You can't add user labels that start with any case form of `sys:`.


<span id="application-scenarios"></span>
## Application Scenarios


* **Group Management**

   You can bind different labels to different environments (such as production and test environments). For example, bind a label key\-value pair like env:test to all functions involved in the test environment. It helps to filter out a group of labelged functions for operations during regular maintenance.

* **Label\-based Accounting**

   In team or project management, you can add labels based on groups, projects, or departments (such as CostCenter:Project) to implement grouping and manage accounts based on labels in the cost center.


<span id="precautions"></span>
## Precautions


* The FaaS resources that support the use of labels include: function.

* Labels consist of a label key (Key) and a label value (Value). When setting the label key (Key) and label value (Value), differentiate between uppercase and lowercase letters in English, and the label value (Value) can be empty.

* For the same resource, multiple labels must have unique label keys (Key), and each label key (Key) can only have one label value (Value).

* A single operation can add up to 20 labels, and a single resource can have up to 50 labels.


<span id="usage-process"></span>
## Usage Process

This article takes functions as an example to illustrate how to manage labels for cloud resources. The general usage process for the label management feature is as follows:


1. Grant permissions to IAM users based on labels: Grant IAM users access to resources with specific labels.

2. [Create function](https://docs.byteplus.com/en/docs/faas/Function_Creation_Option_Selection): Create functions using an IAM user and bind labels.

3. (Optional) [Edit labels](https://docs.byteplus.com/docs/faas/Label_management#edit-labels): When the labels bound to a function change, you can add, modify, or delete labels.


<span id="view-label-resource-information"></span>
## View label resource information

<span id="view-the-labels-bound-to-a-resource"></span>
### View the labels bound to a resource


1. Log in to the [Function Service console](https://console.byteplus.com/vefaas).

2. Select the region where your business is located in the top navigation bar.

3. On the **Function** page, find the target function and click the function name.

4. On the **Function configuration** tab, view the label information bound to the function.


<span id="search-for-resources-by-labels"></span>
### Search for resources by labels.


1. Log in to the [Function Service console](https://console.byteplus.com/vefaas).

2. Select the region where your business is located in the top navigation bar.

3. On the **Function** page, you can quickly search for functions by labels as follows.

   1. Click on the search bar above the function list and select **Label**.

   2. In the pop\-up text box below, specify the label key and label value to be searched. Support for entering multiple labels, with different labels having an **or** filter relationship.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The label value can be left unfilled or as a null value:      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Unfilled: By default, there is no restriction on the label value, it can be any value.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Null value: Search for labels where the label value is empty, i.e., labels added without entering a label value.      </div>
      

   3. Click **Confirm** to view all instances bound to the target label.


<span id="edit-labels"></span>
## Edit Labels

Edit labels for created resources including adding, modifying, or deleting them.


1. Log in to the [Function Service console](https://console.byteplus.com/vefaas).

2. Select the region where your business is located in the top navigation bar.

3. On the **Function** page, choose any of the following methods to access the Edit Labels page.

   1. Click on the modify icon in the **Labels** column where the target function is located.

   2. Click on the target function name to enter the **Function Configuration** tab, then in the **Basic Information** section, click on the modify icon for labels.

4. In the pop\-up Edit Labels dialog box, follow the on\-screen instructions to add, modify, or delete labels.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">A single operation can add up to 20 labels, and a single resource can have up to 50 labels.   </div>
   

5. Click **Confirm** to complete the operation.
