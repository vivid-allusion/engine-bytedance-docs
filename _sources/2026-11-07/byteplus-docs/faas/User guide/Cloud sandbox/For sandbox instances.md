---
title: "For sandbox instances"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Sandbox_instances"
---

A sandbox instance is a secure and isolated container runtime environment that is implemented in the cloud sandbox based on the sandbox image. After creating a sandbox application, you can create a sandbox instance based on a sandbox image. This topic mainly introduces the methods for creating and managing sandbox instances.

<span id="cvyl4bnk"></span>
## Creating sandbox instances

<span id="nASP8Bh5"></span>
### Prerequisites

A sandbox application has been created. For details, see Creating sandbox applications.

<span id="52xOXleg"></span>
### Procedure


1. Log in to [Function Service Console](https://console.byteplus.com/vefaas).

2. On the top navigation bar, select the target region.

3. In the left navigation bar, select **Cloud Sandbox ** \> ** Sandbox Application**, locate the target sandbox application, and click the application name.

4. On the details page of that sandbox application, select the **Sandbox instances** tab and click **Create sandbox Instances**.

5. Configure the sandbox instance parameters according to the following description.

   
   |**Parameter** |**Description** |
   |---|---|
   |**For sandbox images** ||
   |Container image |Configure container images for sandbox instances:<br><br><br>* **Use the same image**: reuse the container image that was used when creating the instance application. There is no need to configure **start command** and **listening port** for instance in this case.<br><br>* **Use another image**: use another image instead of reusing the old one. You can select a **public image** or **custom image** as needed, and then configure **start command** and **listening port**. |
   |Startup command<br><br> |The start command for sandbox instances. If you need to specify a script file, use an absolute path and make sure that the script file has executable permissions. |
   |Listening port |The listening port of the HTTP Server for the sandbox instance.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Avoid using the ports that are already occupied by FaaS<code>: 9000</code>, <code>9001</code>, <code>9990</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The enabled HTTP server needs to listen on <code>0.0.0.0:Port</code> or <code>*:Port</code>. Otherwise, a request timeout error will occur.</div><br> |
   |**Instance configuration** ||
   |Instance specification |Set the number of vCPU and memory capacity for the instance. By default, the instance specification set with the sandbox application will be applied. You can also adjust it as needed according to the prompts on the page. |
   |Instance lifetime |Sandbox instance lifetime. Instances will be terminated upon reaching the end of their lifetime. |
   |**Environment variables** ||
   |Environment variables |The environment variables of each sandbox instance. If not configured, the ones from the sandbox application will be applied instead.<br><br>If a sandbox instance and the application both have an environment variable with the same key, the value set for the former instance will overwrite that for the latter. |
   |**Advanced settings** ||
   |Instance metadata |The metadata of the instance label. Example: `user:2100******`. You can use metadata `<key,value>` to filter sandbox instances.<br><br>Here are some scenarios:<br><br><br>* using it to associate sandbox instances with user sessions.<br><br>* using it to store custom user data for sandbox instances, e.g., API secret keys.<br><br>* Associate the sandbox instance with the user ID to facilitate subsequent connections to the cloud sandbox[ ](https://e2b.dev/docs/sandbox/connect). |
   |Execution timeout |Set an execution timeout as needed. If the instance does not start up within the 30 specified here,  the process will quit and return an error. |
   |TOS storage configuration |If TOS mount is enabled for a sandbox application, the subdirectories of a TOS Bucket can be mounted to instances. If not enabled, the TOS configuration of the sandbox application will be applied. |
   

6. Check the billing information, then click **Confirm** to start creating the sandbox instance.


<span id="rin7bQjP"></span>
## Viewing and managing sandbox instances

After successfully creating a sandbox instance, you can search for it by using the search box on the **Sandbox instance** tab and perform actions on it by using the options in **Actions** column.


|**Operation** |**Description** |
|---|---|
|Search box |Supports search by name, instance metadata, or image address using three Methods. When searching using instance metadata, enter a key\-value pair in the `key=value` format to find the sandbox instance. |
|View logs |View logs related to the sandbox instance. |
|Webshell |Log in to the instance Webshell and execute commands to perform operations such as viewing the environment information of the instance, and performing function debugging.<br><br>The following commands can be used to view the environment information of instances:<br><br><br>1. Get the proc id of the Sandbox service: `ps aux \| grep "sandbox"`<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you are using a custom image, you need to change <code>sandbox</code> to the main process name of your custom image application.   </div><br>   <br><br>2. View the process env: `cat /proc/${your_sandbox_proc_id}/environ \| tr '\0' '\n'`<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>${your_sandbox_proc_id}</code> with the actual Sandbox service process ID you get in previous step. For example, if the process ID is <code>15</code>, the complete command is: <code>cat /proc/15/environ \| tr '\0' '\n'</code>.   </div><br>    |
|Modify lifecycle |Modify the lifetime of the cloud sandbox instance. The instance will be terminated upon reaching the end of the lifetime. |
|Delete |Delete a sandbox instance. This action cannot be undone. |


<span id="le10EIbJ"></span>
## Accessing sandbox instances

Domain names for accessing sandbox instances can be found on the Sandbox instances tab if the corresponding sandbox application already has **Gateway routing** enabled. You can access a specific sandbox instance by using either a unified domain name or a wildcard domain name.


* When the gateway routing configuration uses a unified domain name, you can access a specified sandbox instance via the unified domain name provided by the API gateway. Two Parameter passing Methods are supported:

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">A request sent to a unified domain without either the query parameter or the header will be forwarded to a random sandbox instance.   </div>
   

   * Pass the sandbox instance name `faasInstanceName` in the Query Parameter. The instance list allows you to directly obtain the unified domain name access address with the Query Parameter appended.

   * Pass the sandbox instance name `x-faas-instance-name` in the request Header.

* If a wildcard domain is applied in gateway routing, each instance will have a unique access address.
