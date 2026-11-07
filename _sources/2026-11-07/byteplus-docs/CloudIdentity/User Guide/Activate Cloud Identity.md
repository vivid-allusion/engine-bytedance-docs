---
title: "Activate Cloud Identity"
product: "BytePlus Cloud Identity"
product_code: "CloudIdentity"
source: "https://docs.byteplus.com/en/docs/CloudIdentity/Activate-Cloud-Identity"
---

<span id="activate-cloud-identity"></span>
# Activate Cloud Identity

<span id="scenarios"></span>
## Scenarios

Cloud Identity is a free service. After activating it, you can use it by creating an instance. This topic describes how to activate Cloud Identity.

<span id="prerequisites"></span>
## Prerequisites


1. You have completed your account profile. [Go compltete.](https://console.byteplus.com/user/accountProfile/?hiddenNavbar=true)

2. You have activated the Organization service. [Otherwise, you must activate the Organization service.](https://console.byteplus.com/organization/serviceOpen/)

3. You are an organization master account, such as the root user or an authorized IAM user.


<span id="procedure"></span>
## Procedure


1. Log in to the BytePlus console and go to the [Cloud Identity](https://console.byteplus.com/cloudidentity/region:ap-southeast-1/multiAccountAccess/) page.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_8ee18f609501b0b56bfe14f8a3076e87.png) </span>


2. Click Activate to create a Cloud Identity instance in the region that you selected. Only the Asia Pacific (Johor) region is supported.


<span id="what-to-do-next"></span>
## What to do next

After creating a Cloud Identity instance, you can configure the identity source by referring to [User synchronization settings](http://docs.byteplus.com/en/docs/CloudIdentity/Overview-of-SCIM-based-user-synchronization).

<span id="faqs"></span>
## FAQs

<span id="why-does-my-organization-member-account-have-a-new-service-linked-role-after-activation"></span>
#### Why does my organization member account have a new service\-linked role after activation?

Cloud Identity serves as a trusted service within your organization's multi\-account management framework, requiring delegated access to your organization's account structure. Activating Cloud Identity represents your consent to activate the trusted service, which empowers the organization to automatically create the service\-linked role ServiceRoleForCloudIdentity in member accounts, facilitating batch SSO authorization operations.
