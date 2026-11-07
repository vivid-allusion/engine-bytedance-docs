---
title: "Configure SAML authentication to implement single sign-on"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Configure_SAML_authentication_to_implement_single_sign-on"
---

By using SAML authentication, you can integrate Elasticsearch and OpenSearch instances into the enterprise identity system, enabling users to access through single sign\-on. This topic describes how to configure SAML authentication to implement single sign\-on.

<span id="Cn8wQPFb"></span>
## Background

Single sign\-on (SSO) is a unified identity authentication mechanism that allows users to access multiple trusted applications with a single authentication, avoiding repeated logins. SAML (Security Assertion Markup Language) 2.0 is an XML\-based open standard widely used in enterprise single sign\-on scenarios. It enables secure authentication and authorization by exchanging identity information between an Identity Provider (IdP) and a Service Provider (SP).

After enabling SAML authentication for Elasticsearch and OpenSearch instances, these instances act as service providers (SP) and delegate user authentication to the identity provider (IdP). Once the user completes authentication, the IdP returns a SAML assertion containing user identity and role information to Elasticsearch and OpenSearch instances. They use the assertion to complete user login and permission control, enabling SAML 2.0\-based single sign\-on.

<span id="TTlZtLZd"></span>
## Prerequisites

An Elasticsearch or OpenSearch instance has been created. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/cloudsearch/creating-instance).

<span id="7fDbng5G"></span>
## Precautions


* Only OpenSearch 2.9, 3.3, and Elasticsearch 7 instances support SAML authentication.

* Turning on, editing, or turning off SAML authentication restarts the instance; operate during low\-traffic times.


<span id="1uJXqgfM"></span>
## Turn on SAML authentication


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. On the **Instances** page, click the target instance name.

4. Select **Basic information** in the left navigation bar, then click **Enable password\-free access** to the right of **SAML authentication** in the **Access authentication** section.

5. In the Enable SAML Authentication panel, configure the following parameters, then click **OK**.

   
   |Parameter |Description |
   |---|---|
   |Access method |Select **Public network access** or **Private network access**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default"><strong>Public network access</strong> is visible only when Kibana/Dashboards public network access is enabled. For detailed steps, see <a href="https://docs.byteplus.com/en/docs/cloudsearch/enabling-public-access-tool">Configure Kibana/Dashboards public network access</a>.</div><br> |
   |sp.entity_id |The unique identifier of the SP. |
   |sp.acs |The callback address where the SP receives the SAML response. |
   |idp.entity_id |The unique identifier for the IdP, which must match **idp.metadata** `idp.entity_id`. |
   |idp.metadata |IdP's SAML 2.0 metadata in XML format. |
   |idp.roles_key (optional) |Specifies the SAML attribute for the user role. The instance determines the current visitor's role based on this attribute from the SAML authentication information. |
   |idp.subject_key (optional) |Specifies the SAML attribute corresponding to the user subject. The instance determines the current visitor's subject information from the SAML authentication details based on this attribute. |
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After configuration, each node will restart one by one, and the instance will enter the <strong>Updating</strong> state. Please wait patiently. When the instance returns to the <strong>Running</strong> state, SAML authentication is enabled successfully.   </div>
   

<span id="zSGuy8gr"></span>
## Subsequent operations

<span id="UU5nQ1Bf"></span>
### Access the instance via SAML protocol

After turning on SAML authentication, when users access the Elasticsearch or OpenSearch instance via the SAML protocol, identity and role information are returned by the IdP. `subject_key` and `roles_key` specify the user identity field and role field returned by the IdP. For example, the IdP returns the following information:

```JSON
{
  "subject_key": "xxx@volcengine.com",
  "roles_key": "my_role"
}
```


Here, `subject_key` represents the login username, and `roles_key` represents the user's roles. The instance grants corresponding permissions to users based on the returned role information.

Please ensure roles returned by IdP are created in the instance and configured with proper permissions; otherwise, users may not access related resources properly after logging in. The following example shows how to create a read\-only role for the `logs-*` index via Dev Tools:

```HTTP
PUT _opendistro/_security/api/roles/my_role
{
  "cluster_permissions": [],
  "index_permissions": [
    {
      "index_patterns": ["logs-*"],
      "allowed_actions": ["read"]
    }
  ],
  "tenant_permissions": []
}

PUT _opendistro/_security/api/rolesmapping/my_role
{
  "backend_roles": ["my_role"]
}
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The above example creates a read\-only role. For additional permissions, create roles by calling the API. For detailed steps, refer to the <a href="https://opendistro.github.io/for-elasticsearch-docs/docs/security/access-control/api/">API Reference</a>.</div>


<span id="Zy71Vb3L"></span>
### Modify SAML authentication configuration

After turning on SAML authentication, you may modify its configuration as needed.


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. On the **Instances** page, click the target instance name.

4. Select **Basic information** in the left navigation bar, then click **Edit** on the right side of **SAML authentication** in the **Access authentication** section.

5. On the edit SAML authentication panel, modify the IdP information as needed, then click **OK**. For detailed parameter descriptions, see [Enable SAML authentication](https://docs.byteplus.com/en/docs/6465/2588656#1uJXqgfM).


<span id="0FpR26UY"></span>
### Disable SAML authentication

When you no longer need single sign\-on via SAML authentication, you can turn off SAML authentication.


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. On the **Instances** page, click the target instance name.

4. Select **Basic information** in the left navigation bar, then click **Disable** on the right side of **SAML authentication** in the **Access authentication** section.

5. In the popup dialog, click **OK**.
