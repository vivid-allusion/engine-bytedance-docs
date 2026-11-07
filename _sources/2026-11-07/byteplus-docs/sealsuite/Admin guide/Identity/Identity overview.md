---
title: "Identity overview"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-what-is-iam-"
---

The **Identity** module of SealSuite is a central user repository designed to provide a unified and trusted identity for your organization. This module allows you to manage the entire user lifecycle, from onboarding to departure, by building a comprehensive user directory, synchronizing with other identity providers, and enforcing account security policies.

<span id="15ad71a7"></span>
# Function introduction

To construct an enterprise user directory, it is crucial to establish a central user repository for better visibility and audit purposes. The **Identity** module of SealSuite is designed to provide a unified, trusted identity for the SealSuite platform and to serve as an identity provider for other company business systems. It also manages the entire user lifecycle, including onboarding, offboarding, transfers, and adjustments.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a16e405f98324be2abcac8dc2df3ec2e~tplv-goo7wpa0wc-image.image) </span>

The main functions of Identity Management include:


* **Manage user directory**: In SealSuite, you can construct a comprehensive user directory for your enterprise. This includes creating, updating, querying, and deleting subsidiaries, departments, members, and roles. This function allows for the manual creation of the user directory or enables the import of an existing identity provider, such as Azure AD or Okta, from a third\-party source.

* **Identity source upstream and downstream synchronization**: SealSuite can serve as either an identity provider or a downstream identity consumer to enhance office security, depending on the specific needs of an enterprise's identity platform. When acting as an upstream identity provider, SealSuite can manage user access to enterprise office applications and business systems based on the LDAP protocol. As a downstream identity consumer, SealSuite can integrate with mainstream identity providers (such as Windows AD, OpenLDAP, and Google LDAP) and IM applications (such as Lark, WeCom, DingTalk, and WeLink). It inherits the existing account structure and integrates with other SealSuite modules to enable centralized, identity\-based policy management.

* **Account Security**: SealSuite develops its own MFA to prevent brute force attacks and offers additional features to enhance security for both the platform and its clients.


<span id="97f624c8"></span>
# Related information


* For guidance on building enterprise user directories and entering user information, please refer to [Managing departments](https://docs.byteplus.com/docs/sealsuite/docs-managing-departments) and [Managing users](https://docs.byteplus.com/docs/sealsuite/docs-managing-members).

   If you've already set up an enterprise user directory on a third\-party platform like Google LDAP or Lark, you can easily import it into the SealSuite Admin Console. For instructions, please refer to [Integrating third-party data sources](https://docs.byteplus.com/docs/sealsuite/docs-importing-data-from-third-party-upstream-sources-)and [Managing upstream third-party data source synchronization rules](https://docs.byteplus.com/docs/sealsuite/docs-managing-upstream-third-party-data-source-synchronization-rules).

* SealSuite provides a User Roles function, allowing you to grant different roles to employees based on the functions or business needs. For specific operations regarding User Roles, please refer to [Managing roles](https://docs.byteplus.com/docs/sealsuite/docs-managing-roles).

* You can modify the authentication method and login policy for user accounts in the Account Settings of the Admin Console. You can link your SealSuite account with third\-party login services in the Account Settings. For instructions, please refer to [Setting up account systems and identity authentication](https://docs.byteplus.com/docs/sealsuite/docs-managing-account-settings).
