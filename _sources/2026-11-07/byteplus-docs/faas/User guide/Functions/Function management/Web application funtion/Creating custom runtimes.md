---
title: "Creating custom runtimes"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Create_a_custom_runtime"
---

veFaaS allows you to use a custom image to create a runtime that meets your business requirements for code execution environment and startup method. This topic describes how to create a custom runtime.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">[<a href="https://docs.byteplus.com/en/docs/faas/How_do_I_apply_for_beta_features?LibVersion=markdown备份版本">Beta \- apply for trial</a>] This feature is in beta. Contact your account manager to apply for a trial.</div>


<span id="5abjQ24m"></span>
## Prerequisites

A custom runtime image has been created and pushed to an image registry. For details, see [Pulling and pushing images](https://docs.byteplus.com/en/docs/cr/push-and-pull-images-in-an-enterprise-instance).

<span id="OFLWXUNy"></span>
## Limits


* The container image must be pushed to an image registry that is deployed in the same region as the function.

* After the function is created, you must wait for the image synchronization to complete before releasing the function.


<span id="QC9ujGlm"></span>
## Procedure


1. Log in to the [Function Service Console](https://console.byteplus.com/vefaas).

2. In the top navigation bar, select the target region.

3. In the left navigation pane, click **Function \> Function management**. On the Function page, click **Create function \> Web app function \> Create Web app function.** 

4. In the **Function code** section, click **Create custom runtime** for the **Runtime** parameter.

5. Specify the parameters of the custom runtime.

   
   |Parameter |Description |
   |---|---|
   |Custom Runtime Name |Enter the name of the custom runtime. |
   |Container image |Select a custom runtime image you have created. You can filter the target image by image instance, namespace, and OCI artifact repository. |
   

6. Click **Confirm** to complete the operation.


<span id="vesSt67l"></span>
## What to do next

After the runtime is created, you can update or delete the created custom runtime. In the **Function code** section, select the created custom runtime from the Runtime drop\-down list to perform the corresponding operations.


* Update: Click **Update** to update the name or image of the custom runtime. Click **Confirm** to complete the operation.

* Delete: Click **Delete** and then confirm the deletion to delete the custom runtime.
