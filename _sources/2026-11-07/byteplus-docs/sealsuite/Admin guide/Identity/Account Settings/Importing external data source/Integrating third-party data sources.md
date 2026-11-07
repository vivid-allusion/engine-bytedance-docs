---
title: "Integrating third-party data sources"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-importing-data-from-third-party-upstream-sources-"
---

You can utilize the one\-click import feature to seamlessly integrate the organizational structure and user information from third\-party platforms (such as DingTalk, LarkSuite, WeCom, LDAP, Authing, Windows AD, Azure AD, Okta, and LarkSuite) into the SealSuite Admin Console. This allows for centralized management and prevents the need to recreate employee accounts in SealSuite repeatedly. You can also import organizational and user information from SealSuite to a third\-party platform, simplifying administrative tasks and saving time.

<span id="ba861e3a"></span>
# Use case

The directory synchronization feature in SealSuite comprises two main components: Upstream synchronization and downstream synchronization.


* **Upstream Synchronization**: The upstream synchronization feature allows you to automatically transfer data from a source system (upstream) to the SealSuite Admin Console. This feature facilitates the management and synchronization of data from various sources. It minimizes errors caused by manual data entry while ensuring consistency and real\-time updates in your data.

* **Downstream Synchronization**: The downstream synchronization feature allows you to push the organizational data in SealSuite to subsidiaries or branches. This is ideal for businesses operating with multiple subsystems. By managing a main data source within SealSuite, data can be centrally managed, which helps to decrease operational and maintenance expenses.


Using these two synchronization methods, SealSuite can help your enterprise achieve efficient data management and flow, ensuring that information is accurate and timely.

<span id="694674eb"></span>
# Procedure


1. Log in to the SealSuite Admin Console.

2. In the left\-side navigation bar, select **Identity** \> **Account Setup**.

3. On the **Account Setup** page, click the **Directory Sync** tab.

4. Click **Add Data Source** in the upper right corner.

   If you are configuring directory synchronization for the first time, please click **Start**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f0ceb50d6c064a78ab42c45a5d718cde~tplv-goo7wpa0wc-image.image) </span>


In the **Select data source** dialog box, click the **Upstream Synchronization** or **Downstream Synchronization** tab.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e358b9afc92a4b7aba396cc91615ba07~tplv-goo7wpa0wc-image.image) </span>

6. On the **Upstream Synchronization/Downstream Synchronization** tab, select the specified data source and click **Create**.

7. For detailed operational instructions on different directory synchronization, please refer to the respective documentation to complete the configuration.


* **Upstream Synchronization Configuration**

   * [Importing organizational data from Lark](https://docs.byteplus.com/docs/sealsuite/docs-import-organizational-data-from-lark)

   * [LDAP organizational architecture import configuration tutorial](https://docs.byteplus.com/docs/sealsuite/docs-ldap-organizational-architecture-import-configuration-tutorial)

   * [Google LDAP organizational structure import and third-party login configuration tutorial](https://docs.byteplus.com/docs/sealsuite/Google_LDAP_organizational_structure_import_and_third-party_login_configuration_tutorial)

   * [Azure AD organizational import and third-party login configuration tutorial](https://docs.byteplus.com/docs/sealsuite/docs-azure-ad-organizational-import-and-third-party-login-configuration-tutorial)

* **Downstream Synchronization Configuration**

8. After completing the data source configuration, you can return to the **Directory Synchronization** page to enable or edit the created data source.

   * Enable synchronization for one or more data sources of the same type simultaneously.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can enable synchronization manually, automatically, or in real\-time, but it can only be applied to one data source at a time. If multiple data sources of a certain type have already been synchronized, such as WindowsAD 1 and WindowsAD 2, then other types of data sources, such as LDAP, cannot be synchronized simultaneously.      </div>
      

   * If there is a requirement for managing multiple data sources, you can quickly distinguish and manage them by editing the data source name.


<span id="68577458"></span>
# Follow\-up actions

[Managing upstream third-party data source synchronization rules](https://docs.byteplus.com/docs/sealsuite/docs-managing-upstream-third-party-data-source-synchronization-rules)
