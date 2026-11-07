---
title: "Sandbox applications"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Sandbox_applications"
---

A sandbox application is the fundamental unit of a cloud sandbox, which is used for managing resource scheduling and operation. This topic mainly describes how to create, use, and manage cloud sandbox applications in the BytePlus Function Service (FaaS) console.

<span id="ljkMoCvh"></span>
## Creating sandbox applications

<span id="KJlpCTpd"></span>
### Prerequisites


* An API Gateway (APIG) instance and corresponding services (domain names) have been created to expose the application endpoint. For details, see [Creating instances](https://docs.byteplus.com/en/docs/apig/Creating_an_instance?LibVersion=markdown备份版本) and [Creating services](https://docs.byteplus.com/en/docs/apig/Creating_a_service?LibVersion=markdown备份版本).

* (Optional) The custom images you need are already uploaded to the BytePlus Container Registry (CR). For details, see [Pushing and pulling docker images](https://docs.byteplus.com/en/docs/cr/push-and-pull-images?LibVersion=markdown备份版本).

* (Optional) The BytePlus Torch Log Service (TLS) has been activated. If you need to use a custom logging project to handle function logs, ensure that the project and topics have already been created. For details about related operations, see [Managing log projects](https://docs.byteplus.com/en/docs/tls/Managing_projects) and [Managing log topics](https://docs.byteplus.com/en/docs/tls/Managing_topics).

* (Optional) The BytePlus Virtual Private Cloud (VPC) service has been activated, and a VPC, subnets, and security groups have been created in the region where the function is to be deployed. For details, see [Creating VPCs](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC?LibVersion=markdown备份版本), [Creating subnets](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet?LibVersion=markdown备份版本), and [Creating security groups](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group?LibVersion=markdown备份版本).

* (Optional) Read [Mounting TOS](https://docs.byteplus.com/en/docs/faas/Mount_TOS?LibVersion=markdown备份版本) for instructions related to Torch Object Storage (TOS).

* Optional: Read [Mounting NAS file storage](https://docs.byteplus.com/en/docs/faas/Mount_FileNAS?LibVersion=markdown备份版本) for instructions related to NAS file storage.


<span id="2mg99NBS"></span>
### Procedure


1. Log in to the [Function Service Console](https://console.byteplus.com/vefaas).

2. In the top navigation bar, select the target region.

3. In the left navigation bar, click **Cloud sandbox** \> **Sandbox app**. Then, click **Create sandbox app**.

4. On the **Create sandbox applications** page, specify parameters according to the following instructions.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Basic information** ||
   |Name |Specify a custom name for the sandbox application. The sandbox application name must be unique within the same account. The name cannot be modified after being created. |
   |Description |Enter the description of the sandbox application. It can be left empty. |
   |**For sandbox images** ||
   |Container image |Deploy sandbox applications by using container images:<br><br><br>* **Public image**: The ready\-to\-use public images provided by default.<br><br>* **Custom images**: The custom images that are already preheated. You can filter images by ID or address.<br><br><br>For the description of sandbox images, see [Sandbox images](https://docs.byteplus.com/en/docs/faas/Sandbox_images?LibVersion=markdown备份版本). |
   |Startup command<br><br> |Enter a start command for the application. If you need to specify a script file, use an absolute path and make sure that the script file has executable permissions.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If you set the <strong>Container image</strong> parameter to <strong>Public image</strong>, FaaS will provide the default start command based on the selected image. You can modify the command if necessary.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If you set the <strong>Container image</strong> parameter to <strong>Custom images</strong>: FaaS will automatically parse the configuration file of the target image to obtain the <strong>start command</strong>. You can modify it if necessary.</div><br> |
   |Listening port |Enter the port that the HTTP server listens on.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Avoid using the ports that are already occupied by FaaS<code>: 9000</code>, <code>9001</code>, <code>9990</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The enabled HTTP server needs to listen on <code>0.0.0.0:Port</code> or <code>*:Port</code>. Otherwise, a request timeout error will occur.</div><br> |
   |**Gateway routing configuration** ||
   |Domain type |The domain type of the sandbox application. Valid values:<br><br><br>* **Unified domain**: All the instances in a sandbox application share the same domain name. You can target a specific instance by including the `x-faas-instance-name` header or the `faasInstanceName` query parameter in requests.<br><br>* **Wildcard domain**: [[Beta - apply for trial](https://docs.byteplus.com/en/docs/faas/How_do_I_apply_for_beta_features?LibVersion=markdown备份版本)] Each sandbox instance can have a separate access address.<br><br><br>For description of sandbox instances, see [Sandbox instances](https://docs.byteplus.com/en/docs/faas/Sandbox_instances?LibVersion=markdown备份版本). |
   |APIG instance |Select an APIG instance. The sandbox application will use an API gateway as the traffic entrance. |
   |Gateway service |Select the service that corresponds to the APIG instance. |
   |Route name |Specify a custom route name. The route name cannot be modified after being created. |
   |Path |Set a request path through which the sandbox application can be accessed. It can be matched only by a prefix and must start with a forward slash (`/`). |
   |Route authentication |Configure route authentication for the APIG instance to ensure the route security of the sandbox application.<br><br><br>* **Disable**: Authentication is disabled by default. You can manually enable Key Auth as needed. For detailed operations, see [API Key authentication and authorization](https://docs.byteplus.com/en/docs/apig/Creating_Key_Auth_plugin).<br><br>* **Key Auth**: Use the Key Auth add\-on on APIG to implement API Key\-based authentication and authorization.<br><br>   After selecting **Key Auth**, you also need to perform **authentication configuration**, which means that you need to select the location of the Key Auth information.<br><br>   * **header**: Add Key Auth information in the request header. The default source is Authorization.<br><br>   * **querystring**: Add Key Auth information in the request parameters. The default source is token.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When you use Key Auth, the APIG instance version must be v3.1 or later. If the version does not meet your business requirements, you can submit an <a href="https://console.byteplus.com/workorder/create?step=1">APIG ticket</a> or contact your BytePlus account manager to upgrade the instance version.   </div><br>    |
   |**Environment variables** ||
   |Environment variables<br><br> |Configure custom environment variables, which can be directly read during the runtime of the function code.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you set the <strong>Container image</strong> parameter to <strong>Custom images</strong>, FaaS will automatically parse the configuration file of the target image to obtain the <strong>environment variables</strong> for the image. You can modify it if necessary.</div><br> |
   |**Advanced settings** |For details, see [Function configuration](https://docs.byteplus.com/en/docs/faas/Function_configuration?LibVersion=markdown备份版本). |
   

5. Read and select the checkbox of Function Service Terms of Service and Function Service Product Service Level Agreement, and then click **Confirm** to create the sandbox application.


<span id="IYTnwfgH"></span>
## Managing sandbox applications

After creating a sandbox application, you can view its basic information, monitoring information, and logs. You can also manage it and set queries per minute (QPM) for the API that creates sandbox instances.


1. Log in to the [Function Service Console](https://console.byteplus.com/vefaas).

2. In the top navigation bar, select the target region.

3. In the left navigation bar, click **Cloud sandbox** \> **Sandbox app**.

4. On the **Sandbox app** page, view information about the sandbox application.

   
   |Module category |Description |
   |---|---|
   |Quick deployment through templates |Display various sandbox application templates provided by veFaaS for quick deployment of sandbox applications. For more descriptions, see [Cloud sandbox template](https://docs.byteplus.com/en/docs/faas/Cloud_sandbox_template). |
   |Sandbox application information |In the sandbox application list, you can view the observability (monitoring information and logs) information of the target sandbox application, as well as other basic information such as tags, number of instances, and image addresses. |
   

5. Find a sandbox application and click the application name to go to the details page.

   * **Top of the details page**

      You can release or delete the application in the upper\-right corner of the details page.

   * **Basic information**

      
      |Feature module |Description |
      |---|---|
      |Parameter configuration |View or modify the parameters of the sandbox application. For information about parameters, see the [Creating sandbox applications](https://docs.byteplus.com/en/docs/faas/Sandbox_applications#ljkMoCvh) section of this topic. |
      |Change notice |Provides release prompts after configuration changes. After the configurations of the application are updated, the console will clearly display the differences in configuration items before and after the change. You can release the application based on the on\-screen prompts. |
      

   * **For sandbox instances**

      
      |Feature module |Description |
      |---|---|
      |Resource statistics |Displays the total number of instances and the number of running instances of the current application. |
      |Resource quotas |Displays the usage and utilization of resources. You can click **Apply for more** to apply for higher quotas in **Quota Center**.<br><br><br>* **Maximum number of instances**: Displays the number of created instances of the current application and the proportion of the created instances to the quota. Click **Settings** to adjust the maximum number of available instances and the number of warm pools for the current application. If you need to configure more instances, go to **Quota Center** and apply for more resources by using the `SandboxFunctionInstancesLimit` parameter.<br><br>* **Memory usage**: Displays the memory usage of the current application and the proportion of the memory usage to the quota for the current account. You can apply for more resources in the **Quota Center** by using the `SandboxMemory` parameter.<br><br>* **vCPU usage**: Displays the vCPU usage of the current application and the proportion of the vCPU usage to the quota for the current account. You can apply for more resources in the **Quota Center** by using the `SandboxVCPU` parameter. |
      |Instances |Display the instances of current sandbox application. If no sandbox instance is available, click **Create sandbox instances** to create one. For details, see [Creating sandbox instances](https://docs.byteplus.com/en/docs/faas/Sandbox_instances?LibVersion=markdown备份版本). |
      

   * **Update log**

      
      |Feature module |Description |
      |---|---|
      |Update details |Displays the change information of the sandbox application. Click **Change ID** to view specific changes during a specific period of time. |
      |Version rollback |Click **Roll back** in the **Actions** column that corresponds to a specific update ID. After the secondary confirmation, the application will be rolled back to the historical version. |
      

   * **Monitoring**

      You can view or configure monitoring for sandbox applications. For details, see [Monitoring and logs](https://docs.byteplus.com/en/docs/faas/Monitoring_and_logs?LibVersion=markdown备份版本).

   * **Logging**

      You can view the logs of the sandbox application. For details, see [Monitoring and logging](https://docs.byteplus.com/en/docs/faas/Monitoring_and_logs?LibVersion=markdown备份版本).


<span id="tqohOujq"></span>
## Testing sandbox applications

The following content will use an image named **sandbox\-fusion** and tagged as **Code** type as an example to demonstrate how to test a sandbox application.

<span id="2MJfnv6o"></span>
### Testing by using APIG

Execute the `curl` command locally to call the API to test the cloud sandbox application. You can specify instance requests by using `x-faas-insatnce-name`.


* Replace `https://****.apigateway-cn-beijing.volceapi.com` with the actual access address of your cloud sandbox function.

* Replace the value of `data` as needed.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you are using<code>vefaas-public/sandbox-fusion</code>, read the open\-source document <a href="https://bytedance.github.io/SandboxFusion/zh-Hans/docs/api/run-code-run-code-post/">Sandbox fusion</a> and then replace the value of the <code>data</code> parameter.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you are using a custom image, specify the value of the <code>data</code> parameter according to the actual requirements.   </div>
   

   ```Bash
   curl 'https://****.apigateway-cn-beijing.volceapi.com/run_code' \
     -H 'accept: application/json, text/plain, */*' \
     -H 'accept-language: zh-CN,zh;q=0.9' \
     -H 'content-type: application/json' \
     -H 'x-faas-instance-name: vefaas-ojxvvagw-ondm2cscas-d1eg8b1vnaumg4bf9190-sandbox' \
   --data '{
       "code": "ls",
       "language": "bash",
       "files":{}
   }'
   ```
   


<span id="pqvv2pTr"></span>
### Performing testing by using Playground


1. On the details page of the sandbox application, go to the **Basic information** tab and find the **Gateway routing configuration** section, where you can view the **access address** of the application.

2. On the **Sandbox Fusion** page, click the **Playground** tab and then click **Sandbox** in the left navigation bar.

3. In the **Code** textbox, select a programming language and enter your code, and then click **Submit** to submit the code.

   After the code is run, view the result.
