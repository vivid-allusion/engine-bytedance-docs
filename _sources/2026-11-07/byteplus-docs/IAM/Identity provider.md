---
title: "Identity provider"
product: "BytePlus IAM"
product_code: "IAM"
section: "Document"
source: "https://docs.byteplus.com/en/docs/IAM/identity-provider"
---

An identity provider (IdP) is a user authentication service provider responsible for collecting and storing user identity data such as usernames and passwords. In access control (IAM), it is an entity that contains metadata from external identity providers and provides identity management services. Through identity provider management, Byteplus is able to establish trust between Byteplus and identity providers that support SAML 2.0, allowing members within the customer organization to access Byteplus resources.

<span id="6ZW8PQOb"></span>
## New Identity Provider

Before you can use a user or role SSO, you need to create an identity provider.

<span id="b2ZOV8zx"></span>
### Preliminary steps

Before creating an identity provider, you need to obtain an XML\-formatted IdP metadata document from the enterprise IdP, which contains the address of the IdP login, the signature certificate, and other information.

<span id="eqt5FiRx"></span>
### Operation steps

When creating an identity provider, you can


1. Click the **New Identity Provider** button in Access Control Identity Management Identity Provider.

2. On the New Identity Provider page, select:

   1. Identity provider type (currently supports SAML types, others to come).

   2. SSO type, which represents the user SSO login or role SSO login that you want to do with the identity provider you are currently creating. The number of identity providers for user SSO types is limited to 1, and the number of identity providers for role SSO types is limited to 100. If you choose User SSO, you need to set up User SSO Login:

      1. **Turn on User SSO**: After the switch is turned on, the user can log in to the user SSO through the IdP. If the switch is turned on, the following switch needs to be configured.

      2. **Turn on SSO**: after disabling other console login \*\*switch is turned on, the user can only log in through the IdP user SSO, can not log in through the console password or bound mobile phone number, Douyin account and other third\-party login.

   3. Identity Provider Name: Please provide the identity provider name that is unique under your current account.

   4. Notes: Additional notes from your identity provider, optional.

   5. Metadata file: Please upload the IdP metadata document in XML format that you obtained at IdP. The document size is limited to 30KB.

3. Click Submit to complete the creation.


<span id="pL135dXp"></span>
### Sequential steps

Once you have completed the identity provider creation, you can proceed to create roles with a trusted identity type of identity provider (see [Role Management](https://docs.byteplus.com/en/docs/IAM/role-management)) for role SSO or continue to configure user SSO.

<span id="Iqy2zVzK"></span>
## Manage Identity Providers

In the Identity Management \- Identity Providers list, you can see all the IdP information you created.

Click **Delete** and click **OK** in the pop\-up window to delete the created identity provider. Deleting an identity provider may render the SSO associated with that identity provider unavailable, so proceed with caution.

Click on the identity provider name to view the details of a single identity provider. In the details page, you can modify the current IdP remarks, or you can re\-upload the IdP metadata file. For user SSO type identity providers, you can re\-configure the login settings switch.
