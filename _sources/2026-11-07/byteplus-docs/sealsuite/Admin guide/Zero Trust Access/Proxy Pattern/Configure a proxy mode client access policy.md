---
title: "Configure a proxy mode client access policy"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configure-proxy-mode-client-access-policy"
---

A client access policy defines the proxy gateway clusters available to employees or devices, and controls whether employees can manually select a cluster in the SealSuite client. During automatic cluster selection, the client also selects a cluster only from the policy\-defined scope.

By default, the client uses **Auto\-assign (Auto)** , also known as automatic cluster selection. An administrator can also enable **Allow manual cluster selection** to let employees select access clusters themselves.

* **Auto\-assign**: SealSuite measures the latency of each proxy gateway cluster within the selectable scope, and prioritizes a low\-latency access path for end users.

* **Manual selection**: The client displays the list of allowed clusters and lets users manually switch between them.

For example, an enterprise deploys three clusters in Beijing, Shanghai, and Guangzhou. To allow the R&D department to access only through the Beijing or Shanghai cluster, set its selectable cluster scope to these two clusters. To also let employees switch clusters themselves, enable manual selection.

## Prerequisites

Make sure you have referred to [Access proxy gateways](https://docs.byteplus.com/en/docs/sealsuite/access-proxy-gateway) and successfully created a **gateway cluster** and added associated nodes on the **Zero Trust Access** \> **Gateway Config** \> **Proxy Gateway** page.

## Configuration steps

1. Log in to the SealSuite Admin Console.

2. In the left navigation pane, choose **Zero Trust Access** \> **Proxy Policy**.

3. At the top of the page, switch to the **Client Access Policy** tab.

4. Click **Add Access Policy** on the right side of the page.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/2026-09-24/proxy-en-review/client-access-ready.png)

5. On the **Add Access Policy** page, complete the following configuration, and then click **Confirm** to save it.

   * **General**

      * **Policy name**: Enter a custom, easy\-to\-identify policy name, such as "R&D dedicated line access policy". The name can contain up to 150 characters.

      * **Priority**: Specifies the priority of the current policy. The value ranges from 0 to 100. A larger value indicates a higher priority. The system matches policies in descending priority order and stops matching after a hit. If two policies with the same priority are hit, the policy modified most recently takes precedence.

   * **Access Configuration**

      * **Optional Cluster Scope**: Defines the candidate clusters for automatic selection. **All Clusters** is selected by default. To restrict the scope, select **Partial Clusters**, and then search for or select the allowed clusters. You can select multiple clusters.

      * **Allow manual cluster selection**: Disabled by default, so the client selects a cluster automatically. Enable this option to display the allowed clusters in the client and let employees switch between them.

         > **tip**

         > If the cluster manually selected by a user becomes unavailable as a whole, the SealSuite client automatically falls back to **Auto\-assign** mode to keep business access uninterrupted.

      * **Network Location (optional)**

         Defines the trigger condition for the policy, so that the policy is matched only in specified network environments. The "network location" data comes from the **network region** resource repository maintained globally by the system. To add network region resources, see [Network region management](https://docs.byteplus.com/en/docs/sealsuite/network-zone-management).

         * **Any**: Does not restrict the network location. The current policy takes effect in any network environment.

         * **Specific**: Select one or more defined network regions, such as "Beijing headquarters office area". The policy is triggered only when the system detects that the current network environment of the endpoint, such as IP or Wi\-Fi, matches the characteristics of the selected regions.

         * **Unknown**: If the current network environment of the endpoint does not match the characteristics of any network region defined in the SealSuite Admin Console, it is identified as an "unknown network region". This usually indicates that the employee is using an uncontrolled public or home network. Select this option to define access rules specifically for external network environments.

   * **Conditions**

      * **Scope**: Select the scope of the policy.

         * **User**: Add employees by **department**, **role**, or specific **member**.

         * **Device**: Add devices by device attribute or group.

      * **Exclude object**: After this option is enabled, specific users or devices can be removed from the preceding effective scope for more granular control.

## Client behavior

When employees connect in **Network** \> **Proxy Mode** in the SealSuite client, clusters are selected as follows.

|Policy configuration |Client behavior |
|---|---|
|No client access policy is configured. |* Automatic cluster selection scope: all clusters.<br><br>* Manual selection: Users cannot manually select a cluster. |
|A policy is configured, and manual selection is disabled. |* Automatic cluster selection scope: all or some clusters specified by the policy.<br><br>* Manual selection: Users cannot manually select a cluster. |
|A policy is configured, and manual selection is enabled. |* Automatic cluster selection scope: all or some clusters specified by the policy.<br><br>* Manual selection: The client displays the list of allowed clusters, and employees can manually select a cluster. |

After **Allow manual cluster selection** is enabled, employees can view the cluster list in the client and manually switch clusters.
