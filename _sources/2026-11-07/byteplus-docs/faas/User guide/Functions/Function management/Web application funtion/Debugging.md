---
title: "Debugging"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Debugging"
---

You can perform remote debugging on web applications that use the native runtime by using debugging instances. A cloud\-end debugging instance with a custom lifetime is provided for temporary testing. This solution saves the trouble of repeated modification, release, and verification in the testing procedure.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Considerations


* Only the web applications built on **Native runtime** can be debugged by creating debugging instances. Only the API Gateway (APIG) trigger can be used to simulate traffic tests when using debugging instances. For how to create web applications built on **Native runtime**, see [Creating web applications](https://docs.byteplus.com/en/docs/faas/Creating_Web_applications).

* After a debugging instance is created, it will not be updated along with the later releases of the web application.

* A function can only have one debugging instance. The newly created instance will replace the old one.

* Debugging instances are billed as reserved instances.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Creating debugging containers

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Only applicable to the web applications built on <strong>Native runtime</strong>.</div>



1. Log in to [Function Service Console](https://console.byteplus.com/vefaas).

2. In the top navigation bar, select the region where your business is located.

3. In the left navigation bar, click **Function**. On the page that appears, click the name of the target function to go to the details page of the function.

4. On the **Development and debugging** tab, click **Create debugging container** in the **Debugging container** section.

5. In the **Create debugging container** panel, specify the related parameters and then click **Create**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Create the debugging instance based on the configuration of the latest version for the function. After you create the debugging instance, you can view the debugging instance in the <strong>Instances section on the Resource management</strong> tab.   </div>
   

&nbsp;

   
   |**Configuration** |**Description** |
   |---|---|
   |Container type |The following debugging methods are supported.<br><br><br>* WebIDE debugging: Create a debugging instance based on the latest version of the function and start a web integrated development environment (WebIDE) with the default configuration. You can develop functions using WebIDE within the lifetime of the container. After development is complete, you can update and deploy functions using the veFaaS Code Deployer add\-on that was added to WebIDE. For details, see [Using the veFaaS Code Deployer add-on to manage functions](https://docs.byteplus.com/en/docs/faas/Manage_functions_using_veFaaS_Code_Deployer_plugin).<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Only the functions running based on code packages, rather than images, can be debugged through WebIDE.</div><br><br><br><br>* Webshell debugging: Create a debugging instance based on the latest version of the function. You can log in to the debugging instance through webshell. |
   |Debugging duration |The debugging duration of the debugging instance. |
   |Startup command |This parameter is available only for webshell debugging. The start command of the debugging instance, which is the start command configured for the function in the latest version by default. |
   |Debugging port |This parameter is available only for webshell debugging. The default port number of the debugging instance is 9090. Two ports are supported at most (DebugPort0 and DebugPort1).<br><br><br>* Port numbers can range from 1024 to 65535.<br><br>* The port number cannot conflict with the listening port number of the web application. |
   


&nbsp;

<span id=".5p-l55yLIERlYnVnIOWunuS-iw=="></span>
## Viewing debugging instances

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Only applicable to the web applications built on <strong>Native runtime</strong>.</div>


After the debugging instance is created, click the instance name to go to the **Resource Management** tab. You can view the debugging instance information in the Instances section.


* The name of a debugging instance starts with `debug` and allows you to view the basic information about the instance, such as the availability zone (AZ), status, and start time.

* You cannot migrate debugging instances.

* You can perform the following operations on debugging instances:

   * View instance logs: Click **Log** to view the standard output logs of the target debugging instance.

   * Webshell login: Click **Webshell** to log in to the target debugging instance and run command line interface (CLI) commands on the instance.

   * Delete a debugging instance: Click **Delete**. After a secondary confirmation, you can delete the debugging instance.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">After you delete the debugging instance, the current debugging environment cannot be restored. Proceed with caution.      </div>
      

<span id=".5L2_55SoIERlYnVnIOWunuS-i-i_m-ihjOWHveaVsOa1i-ivlQ=="></span>
## Testing functions

Web applications built on **Native runtime** allow you to create debugging instances. After a debugging instance is created, it can be used for function testing.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default"><strong>Non\-web applications</strong> cannot use debugging instances for function testing. They are tested online only.</div>



1. Log in to [Function Service Console](https://console.byteplus.com/vefaas).

2. In the top navigation bar, select the region where your business is located.

3. In the left navigation bar, click **Function**. Select the name of the target function on the page to go to the details page of the function.

4. Go to **Development and debugging \> Function test**, and select Online instance or Debug instance as needed.



|**Configuration** |**Description** |
|---|---|
|Trigger type |Select the type of trigger for function testing.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When you test a function by using a debugging instance, only the <strong>APIG</strong> trigger is supported.</div><br> |
|Request instance type |Supports two types, i.e., Online instance and Debug instance.<br><br><br>* **Online instance**: You do not need to create a debugging instance. Instead, you can test functions online with simulated events.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Ensure the functions are deployed successfully before you start testing with <strong>Online instance</strong>.   </div><br>   <br><br>* **Debug instance**: It is only effective with Native runtime and can only be tested through **API Gateway** triggers. A cloud\-end debugging instance with a custom lifetime is provided for temporary testing. This solution saves the trouble of repeated modification, release, and verification in the testing procedure. |



3. Click **Test now** to start function testing. You can view the test results at the top of the **Function test** panel.
