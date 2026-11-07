---
title: "Log in to TOS Browser"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Log-in-to-tos-browser"
---

This article uses macOS as an example to explain the steps for logging in to the TOS Browser tool.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

[Install TOS Browser](https://docs.byteplus.com/docs/tos/Install-tos-browser)

<span id=".5L2_55SoLWFrLeeZu-W9lS10b3MtYnJvd3Nlcg=="></span>
## Log in to TOS Browser using AK or STS temporary credentials


1. After installation, double\-click the TOS Browser icon to open the login interface.

2. On the **AK log in** tab, set the login parameters, then click **Log In**. The parameters are described below:

   
   |**Parameter** |**Required** |**Note** |
   |---|---|---|
   |Endpoint |Yes |Select the Endpoint to log in to, explained as follows:<br><br><br>* **Public cloud** (Default): Access using the domain name exposed by TOS external services. When selecting **Public cloud** login, **HTTPS encryption** is checked by default.<br><br>* **Custom**: Log in using a custom domain name. For TOS supported access domain names, see [Regions and endpoints](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint). |
   |HTTPS encryption |No |When accessing through the public cloud, **HTTPS encryption** is selected by default to secure data transmission. |
   |Access Key ID |Yes |Enter the AccessKey ID for the account. |
   |Secret Access Key |Yes |Enter the Secret Access Key information of the account.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For detailed steps to view AKSK information, refer to <a href="https://docs.byteplus.com/docs/byteplus-platform/docs-managing-an-accesskey">View AKSK information</a>.</div><br> |
   |STS Token |No |Enter STS Token information.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When logging in to TOS Browser using only an STS temporary key, set the <strong>STS Token</strong>. For details about the STS temporary key, see <a href="https://docs.byteplus.com/docs/tos/Accessing-tos-with-temporary-credentials-of-security-token-service">Using STS temporary AK/SK+Token to access BytePlus TOS</a>.</div><br> |
   |Access path |No |Enter the access path to quickly open the corresponding file path after entering. The format is `tos://bucket/folder/`, explained as follows:<br><br><br>* If the current AK has permissions for all Buckets, the access path is optional.<br><br>* If the current AK only has permissions for a specific Bucket or a path under a Bucket, the access path is required. |
   |Remarks |No |This is for setting a login nickname to facilitate account management, explained as follows:<br><br><br>* Supports up to 30 characters.<br><br>* Cannot start with a hyphen (\-).<br><br>* If left blank, it defaults to `-`. |
   |Automatically log in |No |Once checked, TOS Browser will log in automatically on subsequent uses. |
   |Remember the key |No |When checked, TOS Browser will save your key information.<br><br><div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div><br><br><br><div data-tips="true" data-tips-type="danger">Do not select this option on temporary\-use computers to avoid risks like key leakage.</div><br> |
   | Historical session |No |TOS Browser records access paths, public cloud Endpoint, custom Endpoint, AccessKey ID, and other historical session information. Click **Historical sessions** to view historical session information in the dialog box, detailed as follows:<br><br><br>* History sessions save up to 100 AK records, with a maximum of 500 access path records per AK.<br><br>* Click **Use**, and the browser will redirect to the login page and automatically fill in the corresponding information.<br><br>   If you modify user information on the login page and log in, the session history will update accordingly.<br><br>* Click the edit button under the **Remarks** list to modify the note information.<br><br>* Click **Delete**, and after clicking **Delete** in the popup dialog, you can delete the corresponding session history. |
   


<span id="820e4eb9"></span>
## Log in to TOS Browser using a shared link

Before logging in to TOS Browser using a shared link, you need to obtain the shared link in advance.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">After logging in to TOS Browser using a shared link, you have read\-only permission for the corresponding file or folder.</div>


* <div data-tips="true" data-tips-type="warning">Login information from shared links cannot be saved in history sessions.</div>


* <div data-tips="true" data-tips-type="warning">You can create shared links via the console. For details, see <a href="https://docs.byteplus.com/docs/tos/Sharing-files">Sharing files</a>.</div>


1. After installing TOS Browser, double\-click the TOS Browser icon to open the login screen.

2. On the TOS Browser login screen, click **Share Link log in**.

3. Enter the **shared link** and click **Log in**.

   After logging into TOS Browser with a shared link, select multiple files and click **Download** to batch download files. You can also click Download All to download all files.


<span id="70c60f3e"></span>
## Log in to TOS Browser using an authorization code

You need to obtain an authorization code in advance to log in to TOS Browser using it.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Authorization codes grant users read and write permissions for specified files or folders as needed. Compared with shared links, they offer more flexible and precise permission control. For detailed instructions, refer to <a href="https://docs.byteplus.com/docs/tos/Create-authorization-code">Create authorization code</a>.</div>


* <div data-tips="true" data-tips-type="tip">Authorization code login information cannot be saved in session history.</div>


1. After installing TOS Browser, double\-click the TOS Browser icon to open the login page.

2. On the TOS Browser login page, click **Auth code log in**.

3. Enter the authorization code and click **Log in**.


<span id="dn1A9WHy"></span>
## Switch session and language


<Tabs>
<Tab zoneid="yPxB5IKG" title="Switch session">
<TabTitle>Switch session</TabTitle>

You may refer to the following steps to switch to the corresponding session while using.


1. Click the item in the upper right of the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_aa5cfee9c7a29530d08874bfb27fbcaa.png) </span> icon.

2. Click **Switch session** in the pop\-up dialog box.

3. In the **Switch session** dialog box, click **Switch** in the operation column of the target session to switch to the corresponding session.


</Tab>
<Tab zoneid="KFCl8inE" title="Switch language">
<TabTitle>Switch language</TabTitle>

TOS Browser supports both Chinese and English, allowing you to switch languages as needed. The procedure for switching languages is as follows:


1. After installing TOS Browser, double\-click the TOS Browser icon to open the login interface.

2. On the upper right corner of the TOS Browser login page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_17a1fcfd59b2d7fc2b61a8dddedc9d90.png) </span> icon.

3. In the **Settings** dialog box, click **System settings**.

4. Select **Language**, Click **Save**.

5. In the **Prompt** dialog box, click **Restart immediately**. After restarting, you can use the selected language.


</Tab>
</Tabs>


<span id="COQxcuf6"></span>
## Use HTTP proxy

When the server is in an internal network environment and external network access must go through a unified gateway, you need to use an HTTP proxy to access object storage TOS. The procedure for using an HTTP proxy in TOS Browser is as follows:


1. After completing the installation of TOS Browser, double\-click the TOS Browser icon to open the login interface.

2. At the top right corner of the TOS Browser login page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_27344616dd8cf19693bafd0230bcf4f6.png) </span> icon.

3. In the **Settings** dialog box, click **System settings**.

4. Set the **Proxy configuration** to **Custom proxy**, enter the **Proxy address** and ** Proxy port**, then click **Save**.

5. In the **Prompt** dialog box, click **Restart immediately ** to apply the proxy configuration.
