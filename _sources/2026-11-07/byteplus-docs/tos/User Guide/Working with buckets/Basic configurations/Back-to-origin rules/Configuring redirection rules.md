---
title: "Configuring redirection rules"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Create-a-redirection-back-to-origin-rule"
---

After setting up a redirect back to the source, when the requested object does not exist in the bucket, TOS supports returning the redirect address to the requester, who then obtains the object or object metadata through the redirect address. This article describes how to set up a redirect back to the source.

<span id="e4a7eac4"></span>
## Background information

The redirection back to the source function supports the following two operations:


* Use GetObject to trigger a redirect back to the source: When the requested object does not exist in the bucket, TOS returns the redirect address to the requester, who then obtains the object from the redirected address.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c10d896858754ec5af673d755cb5c7b3~tplv-goo7wpa0wc-image.image) </span>

* Use HeadObject to trigger a redirect back to the source: When the object requesting metadata does not exist in the bucket, TOS will return the redirect address to the requester, who will then obtain the object metadata through the redirected address.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c0d2879dc2fc4bccaa35bc87f5937149~tplv-goo7wpa0wc-image.image) </span>


<span id="c3d95658"></span>
## Precautions


|**Scene** |**Category** |**Precautions** |
|---|---|---|
|Using GetObject to trigger a redirection back\-to\-origin rule |Back\-to\-origin object size |Maximum support for objects requesting 300GiB. |
||Back\-to\-origin condition |By default, when GetObject returns an HTTP status code of 404, it triggers a redirect back\-to\-origin rule and pulls the file from the source site. |
|Using HeadObject to trigger a redirection back\-to\-origin rule |Back\-to\-origin limit |* Redirecting back\-to\-origin softlink object via HeadObject request is not supported.<br><br>* When requesting to redirect back\-to\-origin object metadata through HeadObject, the parameter **Whether to pull file from the origin server** is invalid, that is, pulling files from the source station and writing them to the TOS are not supported in this scenario. |
||Back\-to\-origin condition |Only when enabling the HeadObject feature when creating the origin retrieval rule, and when the HeadObject request returns an HTTP status code of 404, will the redirection back\-to\-origin rule be triggered. |


<span id="765bd204"></span>
## Procedure


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. In the left navigation pane,select **Basic configurations \> Back\-to\-Origin rules**, and on the **Back\-to\-Origin rules** page, click **Create rule**.

4. On the **Create Back\-to\-Origin Rule** page, configure the following parameters.

&nbsp;

   
   |**Parameter** |**Description** |
   |---|---|
   |Back\-to\-Origin method |Select Redirection. |
   |Back\-to\-Origin condition |Select the triggered return conditions according to the requirements, and trigger the return to the source to meet all the configured return conditions at the same time. The return conditions are described as follows:<br><br><br>* **HTTP Status Code** : Default check and only supported **HTTP Status Code** is **404**.<br><br>* **Filename prefix** : Set the file name prefix that needs to be triggered after checking.<br><br>* **Filename suffix:**  After checking, set the filename suffix that needs to be triggered.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">For example, if you check the suffix before the file name and set it to <code>test</code>and <code>object.png</code>respectively, when you access the <code>test *** object.png</code>object under the bucket does not exist and the returned HTTP status code is 404, TOS will provide the back\-to\-source address set in the rule for you to access.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After checking the prefix and suffix of the file name, you need to set the corresponding information before the condition will take effect; if not, it means that it will not match.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you want to match all the suffixes under the prefix, just check the filename prefix; or check the filename suffix without setting any information.</div><br> |
   |Specify the domain |Specifies the domain name that accesses the source site. When specified, only this domain name can access the origin server to trigger a redirect back\-to\-origin rule.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Specify up to 20 source domains.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The domain name needs to be able to access the bucket. It is recommended to fill in the custom domain name bound to the bucket.</div><br> |
   |Back\-to\-Origin type |Set the origin server type for back\-to\-origin. The fields are described as follows:<br><br><br>* Select ** back to source private bucket** if the origin server is a private bucket from TOS or another cloud provider.<br><br>* Do not select **back to source private bucket** if the origin server is a public bucket from TOS or another cloud provider. |
   |Back\-to\-Origin address |Set the back\-to\-origin address that needs to be jumped after the back\-to\-origin condition is triggered. The instructions are as follows:<br><br><br>* **Add prefix and suffix** : After triggering the back\-to\-origin rule, it will jump to the file with the specified presuffix. The file address description is as follows:<br><br>   1. Protocol: Required, optional **http** or **https**, default is **http**.<br><br>   2. Domain Name: Required, must be in domain name format, IP address is not supported.<br><br>   3. File name prefix: optional, if not, it will jump to the corresponding domain name by default.<br><br>   4. File name suffix: optional, if not, it will jump to the corresponding domain name by default.<br><br>      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e16f31b37028419b9f7d49546c17170a~tplv-goo7wpa0wc-image.image) </span><br><br>* **Redirect to fixed address** : When the back\-to\-origin rule is triggered, all jump to fixed files by default. The fixed address is described as follows:<br><br>   * Protocol: Required, optional **http** or **https**, default is **http**.<br><br>   * Return to source domain name: Required, must be in domain name format, IP address is not supported.<br><br>* **Replace filename prefix** : When the back\-to\-origin rule is triggered, jump to the file that replaces the filename prefix. The instructions are as follows:<br><br>   * Agreement: Required. Optional **http** or **https**, the default is **http**.<br><br>   * Return to source domain name: Required, must be in domain name format, IP address is not supported.<br><br>   * Replacement Prefix: Optional. When the prefix field after replacement is not filled in, it is equivalent to truncation; when the filename prefix before replacement is not filled in, it is equivalent to adding the filename prefix.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Adding only one redirect address is supported.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If you choose <strong>Redirect to fixed address</strong>, operations such as pulling files are not supported.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">After the setting is completed, you can refer to the back\-to\-origin file address below the <strong>TOS Access Address</strong> area to verify if the origin address is set correctly.</div><br> |
   |Whether to support HeadObjec |Whether to support HeadObject requests to trigger redirects back\-to\-origin rule. By default, only GetObject requests are supported to trigger redirects back\-to\-origin rule. When turned on, both GetObject and HeadObject are supported to trigger redirects back\-to\-origin rule. Off by default. |
   |Whether to carry request parameter for back\-to\-origin |Select whether to pass through the queryString carried by the request to the origin server. On by default. |
   |Whether to pull file from the origin server |After opening, TOS will first redirect to the source address, and then pull the file asynchronously in the background and save it to TOS. On by default.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning"><strong>Whether to pull file from the origin server</strong> parameter is only applicable to the scenario where the GetObject request triggers a redirect back\-to\-origin rule. In the scenario where the HeadObject request triggers a redirect back\-to\-origin rule, this parameter is invalid.</div><br> |
   |Whether to carry request parameter for file pull |When pulling the file, choose whether to pass the queryString carried by the request to the origin server. Off by default. |
   |Whether to redirect based on the origin server for async pull |When pulling files, whether to follow the origin server's 3XX redirection requests for retrieval, with a maximum of 3 redirections. It is turned off by default. |
   |HTTP Header passthrough rule |TOS allows the response headers to be passed when accessing the specified origin server. The following rules are supported:<br><br><br>* **Transparently Transmit All HTTP Headers**: Default value, pass through all parameters after selection, but the following request headers will not pass through: Host, Content\-length, Date, Authorization.<br><br>* **Transparently Transmit Specified HTTP Headers**: Specify the headers allowed to pass, up to 10 can be added.<br><br>* **Transparently Transmit No HTTP Headers** : Disable passthrough of all parameters when selected.<br><br>* **Not Transparently Transmit Specified HTTP Headers** : Specify headers that are prohibited from passing, up to 10 can be added. |
   |Add specified HTTP Header |Specify the Key and Value of the HTTP Header. When specified, the Key and Value will be added to the Header and passed to the origin server.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Specify up to 10 HTTP headers.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Headers specifying Content\-Length, Date, Range, Authorization types are not supported.</div><br> |
   |Support custom metadata |* When fetching an object from a specified origin server, you can save the response headers (SourceHeader) from the origin as custom metadata for the object. TOS automatically prefixes the metadata key with `x-tos-meta-` and appends the suffix you set (MetaDataSuffix), forming the final metadata key.<br><br>* Click **Add metadata** and configure the following:<br><br>   * Enter the origin response header (SourceHeader) in the left input box.<br><br>   * Enter the metadata key suffix (MetaDataSuffix) in the right input box.<br><br>   You can add or remove multiple mapping groups. Each rule supports up to ten mappings.<br><br>* For example, if SourceHeader is `content-language` and MetaDataSuffix is `language`, the final metadata key is `x-tos-meta-language`. |
   

5. Click **Submit**.

   After the mirror back\-to\-origin rule is created, you can view the created rule in the policy list.


<span id="21aa45da"></span>
## Related operations


* Edit back\-to\-origin rule: Click **Edit** in the target rule **Actions** column to modify back\-to\-origin rule.

* Delete back\-to\-origin rule: Click **Delete** in the target rule **Actions** column and click **Delete** in the pop\-up dialog box to delete the back\-to\-origin rule.

* Move up/down back\-to\-origin rule: Click **Up** or **Down** in the target rule **Actions** column to adjust the order of the back\-to\-origin rules.
