---
title: "Managing sub-account permissions based on project resource"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/subaccounts"
---

IAM (Identity and Access Management) is a permission management system provided by BytePlus MediaLive to manage IAM users and resource access.

This article introduces how to use IAM users (also known as sub\-accounts) to set project permissions on the console to implement project\-specific permission control for sub\-accounts.

<span id="6803a245"></span>
## Concepts


* **Main account**: A registered BytePlus account.

* **Sub\-account**: A user created based on the main account.

* **User group**: A group of sub\-accounts. You can set permissions for user groups which will be applied to users in the group.

* **Policy**: A set of permissions. MediaLive allows customer managed policies, and each product also provides a system managed policy that meets the needs of its specific business.


<span id="ca576607"></span>
## Policy type

Policy is a group of permissions. You can bind a policy to a sub\-account to grant corresponding authorization.

<span id="5c685a50"></span>
### System managed policy

MediaLive currently provides two system managed policies, **LIVEFullAccess** and **LIVEReadOnlyAccess**, for you to bind sub\-accounts.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e0c4db5b1f6247aaa2d54b8a3cf3f63d~tplv-goo7wpa0wc-image.image) </span>

**LIVEFullAccess**: Provides full access to MediaLive.

**LIVEReadOnlyAccess**: Provides read only access to MediaLive.

<span id="23688bb1"></span>
### Customer managed policy

MediaLive supports custom policies.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/63be25bf92c84485b7ca13e99cd3e1fe~tplv-goo7wpa0wc-image.image) </span>

<span id="430927eb"></span>
## Procedure

<span id="77fedd79"></span>
### Create a project


1. Log in to the [BytePlus IAM console](https://console.byteplus.com/iam/identitymanage/user) through the main account.

2. In the left navigation pane, click **Project \> Create Project.** 

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/353601fff598406986cf0a434caa338b~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the **Project name** and click **OK**.


<span id="bf7e29a6"></span>
### Create an IAM user and set up permissions


1. Log in to the [BytePlus IAM console](https://console.byteplus.com/iam/identitymanage/user) through the main account.

2. In the left navigation pane, click **User management** \> **User**.

3. Click **Create New User**. Fill in the \*\*Username \*\*and configure **Login settings** on the **Basic information settings** of **Create User** page.

   * **Programmatic access**: Assign Access Keys to users for access through APl requests.

   * **Console access**: Assign passwords to users for access through the console.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf3557d0d9db41359faaedf117d14d83~tplv-goo7wpa0wc-image.image) </span>

4. Click **Next**. Select permission policy and project on the **Permission settings** of **Create User** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7404f4e01bf1429f91d1d90098c4a99d~tplv-goo7wpa0wc-image.image) </span>

5. Click **Next**. Review your settings carefully, then click **Submit**.


<span id="44ff87de"></span>
## What's next

<span id="310872fd"></span>
### Using project in MediaLive


* When adding a domain name, select the project to which the domain name space belongs. See [Adding a domain name](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-domain).

* When adding an HTTPS certificate, select the project to which the certificate belongs, see [Managing SSL certificates](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-managing-certificates).

* When creating an SDK app, select the project to which the app belongs, see [SDK management](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management).

* When creating a relay group, select the project to which the relay group belongs, see [Configuring a relay task](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-relay).

* Use projects to filter query data in usage statistics and statistical analysis, see [Querying usage data](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-usage-statistics) and [Querying analytic data](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-statistical-analysis).


<span id="a41dfec3"></span>
### Access console through IAM user function


1. Go to the [BytePlus](https://console.byteplus.com/auth/login) login page.

2. Click **IAM user** and go to **IAM user sign in** page.

3. Fill in **Main account username**, **Sub\-account username** and **Password**, then click **Sign in**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/647ae2d2199c42c58b32b3aa10887167~tplv-goo7wpa0wc-image.image) </span>

4. In the **Products** list, click **BytePlus MediaLive** to access the console.


<span id="6b7816f3"></span>
### Get Access key of IAM user and make a request


1. Log in to the [BytePlus IAM console](https://console.byteplus.com/iam/identitymanage/user) through the main account.

2. In the left navigation pane, click **User management** \> **User** to show the user list, and click a username in the list.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c56042e5df044c789b3137215d79bcb5~tplv-goo7wpa0wc-image.image) </span>

3. Go to the **User detail** page, switch to the **Access Key** tab to view the access key of the current IAM user.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e3b7f97ccbca44478bf881b4901034bd~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the key list, you can disable the Access Key in use or enable it again.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Access Key ID and Secret Access Key are the keys for you to access the MediaLive API. They have all the permissions of the IAM user. Each IAM user can create a maximum of two Access Key ID and Secret Access Key.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Please keep the key properly and change it regularly, and delete the key that is no longer in use as soon as possible. Once the key is deleted, it will become invalid and cannot be restored. Please operate with caution.   </div>
   

4. Use the IAM user access key to call the SDK. The sample code is as follows (using `CreateDomainV2` as an example).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Initialize the LiveService instance using the key of the IAM user. The access key is used for authentication and authorization to access MediaLive services.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Call the <code>CreateDomainV2</code> method in the sample code to initiate a request for adding a domain name to MediaLive. The method passes the parameters required for creating a new domain name into MediaLive.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The instance uses the IAM user AKSK to generate a signature and adds the signature to the request. This ensures the authentication and integrity of the request to prevent unauthorized access and data tampering.   </div>
   

   ```Java
   package com.byteplus.live.demo;
   
   import com.byteplus.model.live.v20230101.*;
   import com.byteplus.service.live.v20230101.LiveService;
   import java.util.ArrayList;
   import java.util.List;
   
   public class CreateDomainV2Demo {
   
     public static void main(String[] args) {
       // It's strongly advised against storing BYTEPLUS_ACCESSKEY and BYTEPLUS_SECRETKEY in the project code, or the AccessKey might leak, endangering the security of all resources under your account.
       // This example authenticates API access by reading BYTEPLUS_ACCESSKEY and BYTEPLUS_SECRETKEY from environment variables. Before running the code example, configure BYTEPLUS_ACCESSKEY and BYTEPLUS_SECRETKEY environment variables.
       LiveService service = LiveService.getInstance();
   
       service.setAccessKey(System.getenv("BYTEPLUS_ACCESSKEY"));
   
       service.setSecretKey(System.getenv("BYTEPLUS_SECRETKEY"));
   
       CreateDomainV2Body body = new CreateDomainV2Body();
   
       // An array of domain names.
       // note:
       // A domain name space can contain up to 10 domain names.
       List<CreateDomainV2BodyDomainsItem> Domains = new ArrayList<>();
   
       CreateDomainV2BodyDomainsItem Domains1 =
         new CreateDomainV2BodyDomainsItem();
   
       // The accelerated region. Valid values include:
       // <li> oversea: Outside the Chinese mainland. </li>
       // <li> cn: The Chinese mainland. </li>
       // <li> global: Global. </li>
       Domains1.setRegion("cn");
       Domains.add(Domains1);
       body.setDomains(Domains);
   
       try {
         CreateDomainV2Res resp = service.CreateDomainV2(body);
         System.out.println(resp);
       } catch (Exception e) {
         e.printStackTrace();
       }
     }
   }
   ```
