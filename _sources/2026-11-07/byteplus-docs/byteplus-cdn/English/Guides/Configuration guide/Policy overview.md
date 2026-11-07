---
title: "Policy overview"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-policy"
---

In BytePlus CDN, a policy is a reusable configuration template that combines settings for origin servers and other CDN features. By creating and binding policies to your domains, you can efficiently manage and apply a standardized set of configurations at scale.

This guide introduces the different policy types and provides step\-by\-step instructions for the entire policy lifecycle, from creation and configuration to binding and other management operations.

<span id="policy-types"></span>
## Policy Types

CDN provides the following policy types:


* Delivery policy: Used to configure origin servers and non\-HTTPS related CDN features.

* Encryption policy: Used to configure HTTPS\-related CDN features.

* Rules Engine policy: Used to configure rules in the Rules Engine.


In CDN, each domain can only be bound to one delivery policy and one encryption policy but can be bound to multiple Rules Engine policies.

<span id="steps"></span>
## Steps

The following steps use a delivery policy as an example. The steps for encryption policy are similar. For steps about Rules Engine policy, see [Rules Engine](https://docs.byteplus.com/en/docs/byteplus-cdn/rules-engine_en).

<span id="step-1-create-policy"></span>
### Step 1: Create Policy


1. Log in to the BytePlus CDN management console.

2. In the left navigation bar, click **Delivery Policies**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you are creating an encryption policy, click <strong>Security Center</strong> \> <strong>Encryption Policies</strong>.   </div>
   

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_ef7614463e694e5524250cf96caa44d5.png) </span>

3. On the **Delivery Policies** page, click **Create Policy**.

4. On the **Create Delivery Policy** page, enter the policy name and description. The policy name cannot be longer than 100 characters. The policy description cannot be longer than 120 characters.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_ef342b0b5ac71af45e2a62dafb395156.png) </span>

5. In the **Project** list, specify the project to which this policy belongs.

6. Under **Optional Configurations**, select the modules you need to configure, and then click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The Origins module is mandatory. It contains configurations related to the origin server.   </div>
   

For each policy, CDN will create a policy ID. You can find the policy ID in the policy list and policy details. The policy ID starts with `tpl-` and is 10 characters long. You cannot modify the policy ID.

Next, you need to configure the policy.

<span id="step-2-configure-policy"></span>
### Step 2: Configure Policy

In this step, you need to configure the origin server and other modules included in the policy.


* For more information about configuring the origin server, refer to [Origin configurations](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-origin-configurations).

* For more information about configuring other modules, refer to the respective module configuration instructions.


After configuring, click **Save**.

Next, you need to publish the policy.

<span id="step-3-publish-policy"></span>
### Step 3: Publish Policy

To bind a policy to a domain name, you must publish the policy.

To publish a policy, follow these steps:


1. On the **Delivery Policies** page, find the policy you just created in the policy list.

2. In the **Actions** column, click **Publish**.

3. On the **Confirm Operation** page that appears, click **OK**.


<span id="step-4-bind-domain-names"></span>
### Step 4: Bind Domain Names

After a policy is published, you can bind it to a domain. Once the binding is complete, the policy's configurations will take effect for the domain.

To bind a policy to one or more domain names, follow these steps:


1. On the **Delivery Policies** page, find the policy you want to bind in the policy list.

2. In the **Actions** column, click **Bind**.

3. On the **Bind Domain Names** page, select the domain names you want to bind, and then click **OK**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">There is no limit to the number of domain names that can be bound to a policy. However, in the console, you can only select up to 50 domain names at a time. If you need to bind more domain names, repeat the steps in <strong>Bind Domain Names</strong>.</div>


<span id="other-policy-operations"></span>
## Other Policy Operations

The following describes other operations you can perform on policies in the BytePlus CDN console.

<span id="view-policies"></span>
### View Policies

In the policy list, you can view general information about all policies.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_5577914a4426b9cb6bebbae79ef67f47.png) </span>

You can click the policy ID to view the detailed configurations of the policy.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e8d383e94989ce618ba452b92e7111cc.png) </span>

<span id="modify-policies"></span>
### Modify Policies

Configurations in policies are managed through versions. To modify policy configurations, you need to create a policy version. For information about policy versions and related operations, see [Policy Management](https://docs.byteplus.com/en/docs/byteplus-cdn/policy-management_en).

<span id="delete-policies"></span>
### Delete Policies

You can only delete policies that are not bound to any domains, which means the policy's **Bindings** count in the list is 0.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Once a policy is deleted, it cannot be recovered, so please proceed with caution.</div>


<span id="steps"></span>
#### Steps


1. In the policy list, find the policy you want to delete.

2. In the **Actions** column, click **Delete**.

3. In the **Confirm Operation** dialog box, click **OK**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf86c289a25e49b29c895ff27d9c48b5~tplv-goo7wpa0wc-image.image) </span>


<span id="duplicate-policies"></span>
### Duplicate Policies

To create a policy with settings similar to an existing one, you can duplicate the existing policy.

You can only duplicate published policies.

A policy created by duplication has a status of 'Draft'. Afterward, you can modify the configurations of the policy, publish it, and then bind it to domain names.

<span id="steps"></span>
#### Steps


1. In the policy list, find the policy you want to duplicate.

2. In the **Actions** column, click **Duplicate**.

3. In the **Duplicate Policy** dialog box, enter a name, description, and project for the new policy, and then click **OK**.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_d6cbce6f792a9e8718cd60db94304dec.png) </span>


<span id="search-for-policies"></span>
### Search for Policies

On the policy list page, you can search for policies by their bound domain name, policy name, or policy ID. The search options include **Fuzzy Match** and **Exact Match**. The following screenshot demonstrates how to search for all the policies bound to [www.example.com](http://www.example.com).

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_3fa2f4beda0b6a6b6d004827fd67aa41.png) </span>

<span id="export-policies"></span>
### Export Policies

You can export the policies by clicking the download button at the top right of the policy list.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e6c1beeeab8634a1391ef8832708dd00.png) </span>

The exported list is saved in as a .csv file. The file name format is `ByteplusCDN-<Policy_Type> <Account_ID>_<Export_Time>`. For example: ByteplusCDN\-Delivery\-Policy 3000000xxx_20230825190817. The content of the file matches the policy list in the console.

<span id="view-history"></span>
### View History

On the policy details page, you can view the policy's ancestry tree and operation history.

<span id="policy-ancestry"></span>
#### Policy Ancestry

In CDN, there are two ways to create a policy:


* Create a policy from scratch.

* Duplicate an existing policy.


Assume you create Policy A from scratch, then create Policy B by duplicating Policy A, and then create Policy C by duplicating Policy B. In this case, the ancestry tree of Policy C will be: Policy A \> Policy B \> Policy C.

The ancestry tree displays up to 10 ancestors.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a31780bb391e02888ba09e9a0332f0c1.png) </span>

<span id="operation-history"></span>
#### Operation History

For a policy, CDN records the following types of operations:


* Create policy.

* Publish policy.

* Bind domain name.


The operation history lists all operations performed on the policy. These operations are sorted chronologically, with the most recent at the top. The list shows up to 10 operations.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_085d52b4c1cbd2694d057a633ccfeed4.png) </span>

For a "Bind domain name" operation, the history shows the domain names that were bound to the policy before and after the operation. You can click **View Changes** to view the changes.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_9704383332851a107f16d2444b3a581d.png) </span>
