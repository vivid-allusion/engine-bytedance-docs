---
title: "Quick start guide"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Quick_start_guide"
---

ArkClaw supports workspace activation with multiple authentication methods, to meet enterprise requirements for account management, security, and compliance. Enterprises can choose the most appropriate authentication method based on existing account systems or demands for quick trial, and deliver convenient Single Sign\-On (SSO) experience to employees.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The <strong>Getting Started</strong> topic walks administrators through the full workflow to activate ArkClaw. Once the steps are completed, you can start using ArkClaw without referring to the separate section on <strong>administrator activation of ArkClaw</strong>.</div>



* <div data-tips="true" data-tips-type="warning">For employee instructions, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Applying_for_ArkClaw_instances"><strong>Employee use of ArkClaw</strong></a><strong>.</strong></div>


* <div data-tips="true" data-tips-type="warning">For details about the advanced settings for the administrator, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Space_information"><strong>ArkClaw management by the administrator</strong></a>.</div>



<span id="QO6IY2Ze"></span>
## Space activation methods

ArkClaw Enterprise supports multiple space activation methods. To quickly find a suitable activation method, see the following suggestions.


* If your enterprise wants a **quick trial or immediate activation** without integrating with the existing account system for the time being, **Platform\-hosted** is recommended.

* If your enterprise **already heavily uses office collaboration tools** (Feishu, Lark,  Microsoft Teams, Slack), we recommend selecting the corresponding authentication method to reduce the burden on employees of remembering multiple sets of account credentials and to unify permission management.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If your enterprise has a <strong>self\-built unified account center</strong> (for example, based on OAuth 2.0, OIDC, or SAML), we recommend that you adopt <strong>other standard protocols</strong> for flexible integration after space activation.</div>



|**Authentication** |**Is pre\-configuration required** |**Applicable scenario** |**Activation instruction** |
|---|---|---|---|
|[Feishu](https://docs.byteplus.com/en/docs/ArkClaw/Feishu_authentication) |Yes |Enterprise internal teams are managed via Feishu. |* Configure a dedicated Feishu SSO application and grant required permissions before space activation.<br><br>* After the administrator activates the space, employees can log in via one\-click Feishu authorization for seamless integration with the existing organizational structure. |
|[Lark method](https://docs.byteplus.com/en/docs/ArkClaw/Lark_authentication) |Yes |The enterprise already uses Lark to manage teams internally. |* Before activating the space, a dedicated Lark SSO application must be configured and granted the necessary permissions.<br><br>* After the administrator activates the space, employees can log in with one\-click authorization via Lark, seamlessly integrating with the existing organizational structure. |
|[Slack method](https://docs.byteplus.com/en/docs/ArkClaw/Slack_authentication) |Yes |The enterprise already uses Slack to manage teams internally. |* Before activating the space, a dedicated Slack SSO application must be configured and granted the necessary permissions.<br><br>* After the administrator activates the space, employees can log in with one\-click authorization via Slack, seamlessly integrating with the existing organizational structure. |
|[Microsoft Teams](https://docs.byteplus.com/en/docs/ArkClaw/Microsoft_Teams_authentication) |Yes |Enterprise internal teams are managed via Microsoft Teams. |* Configure a dedicated Microsoft Teams SSO application and grant required permissions before space activation.<br><br>* After the administrator activates the space, employees can log in via one\-click Microsoft Teams authorization for seamless integration with the existing organizational structure. |
|Other standard protocols<br><br><br>* [OAuth 2.0 protocol](https://docs.byteplus.com/en/docs/ArkClaw/OAuth)<br><br>* [OIDC protocol](https://docs.byteplus.com/en/docs/ArkClaw/OIDC_protocol)<br><br>* [SAML protocol](https://docs.byteplus.com/en/docs/ArkClaw/SAML_protocol) |No (quick activation) |Enterprises with a self\-built Identity Provider (IdP) or other standard SSO services. |No pre\-configuration is required. After space activation, complete the authentication configuration based on the adopted OAuth 2.0, OIDC, or SAML protocol. |


<span id="rH30UfdE"></span>
## Activate multiple spaces

ArkClaw supports activating independent ArkClaw spaces under different projects to facilitate unified multi\-project management. Resources (such as seats and Coding Plan packages) and billing (renewal and configuration changes) of each space are fully isolated and operate independently. In the ArkClaw console, administrators can directly activate and configure an ArkClaw space for any project that does not yet have one.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning"><strong>Limit on number of spaces</strong>:</div>


   * <div data-tips="true" data-tips-type="warning">By default, only 1 ArkClaw space can be activated within <strong>a single region</strong> or <strong>a single project</strong>. To activate multiple spaces within the same region (this support is in beta), contact your customer manager.</div>


* <div data-tips="true" data-tips-type="warning"><strong>Space permission assigment</strong>: To assign different management permissions to multiple spaces for differentiated permission control, you can attach permission policies to IAM users and limit the resource scope to which those permissions apply. For details, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Authorizing_an_IAM_user_to_use_ArkClaw_Enterprise#5qQx0Wfg">Authorizing IAM users to access ArkClaw</a>.</div>


* <div data-tips="true" data-tips-type="warning"><strong>Security and instance isolation</strong>: If the security management service is enabled, Claw instances will, by default, enable the Claw Sentry plugin to provide security protection. Individual spaces are independently managed. The security management module governs Claw instances only within the current space and loses its effect after you switch to another space.</div>


* <div data-tips="true" data-tips-type="warning"><strong>Space deletion</strong>: You cannot delete an activated space yourself. To delete it, submit a ticket or contact technical support for assistance.</div>


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. Click the resource scope button in the top menu bar to view other projects.

3. Select a project for which no ArkClaw space has been created. On the ArkClaw space activation page, configure the space. For detailed settings and steps, see the topic corresponding to the selected authentication method (for example, [Feishu authentication](https://docs.byteplus.com/en/docs/ArkClaw/Feishu_authentication?lang=en#2orpKEw3)).
