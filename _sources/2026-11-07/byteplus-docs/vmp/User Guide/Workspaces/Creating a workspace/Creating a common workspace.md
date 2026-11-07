---
title: "Creating a common workspace"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Creating-workspaces"
---

The common workspace is a cloud\-based standard workspace provided by Vital Managed Service for Prometheus (VMP). The common workspace offers logically isolated Prometheus capabilities. This topic describes the procedure and considerations for creating a common workspace.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

VMP has been activated.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target region.

3. Click **Workspace** in the left navigation bar to go to the workspace list page.

4. Click **Create**, and click the **Common workspace** tab to configure the common workspace.

   
   |**Parameter** |**Descriptions** |
   |---|---|
   |Project |The project to which the workspace belongs. |
   |Region |Specify the region of the workspace.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In private networks, cloud services and the VMP service in the same region are interconnected by default. It is recommended to deploy the VMP service and monitoring objects in the same region.</div><br> |
   |Workspace name |Specify a name for the workspace. The data of workspaces with different names is isolated. |
   |Enable custom authentication (optional) |By default, the common workspace supports authentication through  **AK/SK** for data writing and query. You can also manually enable and configure custom authentication based on your business requirements.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The common workspace provides dual\-mode <strong>AK/SK</strong> authentication capability by default:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Use the standard signature method of  <strong>AK/SK</strong> to complete identity verification by carrying signature information in the request header.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Use the  <strong>AK</strong> as the username and the <strong>SK</strong> as the password to complete basic authentication. This meets the access requirements of third\-party tools.</div><br><br><br>* **Enable custom authentication**: After you enable this option, workspaces support **custom authentication** and BytePlus ** AK/SK** authentication. Custom authentication is categorized into the following two types: ** Basic Auth** and ** Bearer Token**.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Basic Auth</strong> and <strong>Bearer Token</strong> cannot be both enabled.   </div><br>   <br><br>   * **Basic Auth**: A basic authentication method that supports authentication**** through custom usernames and passwords, which achieves data writing and query.<br><br>   * **Bearer Token**: A token\-based authentication method that supports authentication through tokens, which achieves data writing and query.<br><br>* **Disable custom authentication** (default): After you disable custom authentication, you can use the default  **AK/SK** method to perform authentication. |
   |Basic Auth (optional) |You need to specify the following parameters only if **Enable custom authentication** is enabled, and **Basic Auth** is used for authentication.<br><br><br>* **User name**: Specify a username used for Basic Auth authentication.<br><br>* **Password**: Specify a password used for Basic Auth authentication.<br><br>   * **Confirm password**: Enter the password used for basic authentication again and ensure the two passwords are identical. |
   |Bearer Token (optional) |You need to specify this parameter only if **Enable custom authentication** is enabled and **Bearer Token** is used for authentication.<br><br>You can click **auto generation** to obtain a **Token** or manually enter a **Token**. This token is used to validate requests and restrict the scope of operations.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The bearer token will be stored by the system through reversible encryption to ensure token data security. To prevent risks caused by the manually configured token, such as weak passwords and repeated use, we recommend that you use the <strong>automatic generation</strong> feature of the   to obtain the token.</div><br> |
   |Public network access |Set whether to allow access to the workspace over the public network.<br><br><br>* **Enable**: The workspace can be accessed over the public network. After the workspace is created, both public and private network access addresses are generated.<br><br>* **Disable**: The workspace cannot be accessed over the public network. After the workspace is created, only a private network access address is generated.<br><br><br>If you enable public access, you need to configure the HTTPS certificate public key.<br><br><br>* **Public key**: Enter the Base64\-encoded certificate public key in the field. |
   |Delete protection |Enable or disable the deletion protection feature for the workspace.<br><br><br>* <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a23fe514b7cf317a3f7ce6fdc2d3a51b.png) </span>Enables the deletion protection feature for the workspace. After the feature is enabled, the workspace cannot be deleted, which prevents accidental deletion. If you want to delete the workspace later, you need to disable this feature in the **Basic information** section on the details page of the workspace.<br><br>* <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0b1e4b6b24897ecfec6af06c69491d3d.png) </span>Disables the deletion protection feature for the workspace, which allows the workspace to be deleted. |
   |Tags |Enter the label of the workspace to identify the key\-value pair of the workspace. Combined with the selector, the tag can be used to quickly filter the target workspace.<br><br>Click **Add tag**, and enter the **label key** and **label value** as prompted. |
   |Workspace instance type |Specify the type of workspace. Currently, only **Standard Edition** is supported. |
   |Billing method |Select the billing type as needed. Available options include "Charge Based on Write Volume" and "Bill by reported volume". For details on different billing types, see [Pay-as-you-go](https://docs.volcengine.com/docs/6731/447498).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After a workspace is created, its billing type can be changed only once. For more details, see <a href="https://docs.volcengine.com/docs/6731/2488939">Changing the workspace billing type</a>.</div><br> |
   |Data storage duration |Select a data storage duration based on your business requirements.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The data storage precision in the workspace varies based on the data storage duration. The data storage precision decreases as time passes after the data is written. Precision decreases by the following rules:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When data storage duration ≤ 90 days, the storage precision remains the <strong>original precision</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When 90 days < data storage duration ≤ 180 days, the storage precision is <strong>5 minutes</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When 180 days < data storage duration ≤ 1 year, the storage precision is <strong>1 hour</strong>.</div><br><br><br><br><div data-tips="true" data-tips-type="warning">For example, if you create a workspace with a storage duration of 1 year and continuously write data into the workspace, the workspace will contain data with different precision at the same time. The storage precision of data with a storage duration of 1 to 90 days remains the original precision. The storage precision of data with a storage duration of 90 to 180 days is 5 minutes. The storage precision of data with a storage duration of 180 days to 1 year is 1 hour.</div><br> |
   

5. After you confirm that the configurations are correct, select **I have read and agreed to Vital Managed Service for Prometheus Dedicated Service Terms & Vital Managed Service for Prometheus Product Service Level Agreement**.

6. Click **Create Now**, and wait for the system to create the workspace.


<span id="iKXbjLBU"></span>
## Verifying results

<span id="FhruDkvF"></span>
### View workspace status

After the workspace is created, you can view the workspace in the workspace list. When the workspace is in the **Normal** state, it indicates that the workspace is created and works as expected.

<span id="uDUAkJdn"></span>
### Obtain workspace addresses

Click the workspace name to go to the details page of the workspace, and view and obtain the addresses of the workspace. For details, see [Obtaining workspace addresses](https://docs.byteplus.com/en/docs/vmp/Obtaining-the-Remote-Write-URL-and-Query-URL).
