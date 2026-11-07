---
title: "Configuring data protection rules for sync tasks"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configuring-data-protection-rules-for-sync-tasks"
---

Data protection rules are designed to prevent data loss during synchronization tasks, helping to ensure the security of your organizational data and maintain business continuity.

<span id="feac7d2b"></span>
# How It Works

Data Protection Rule acts as a crucial safeguard to prevent accidental mass data loss during user synchronization.

In a typical scenario, a network issue or a misconfigured identity provider could cause a sync task to incorrectly flag many active employees as departed. Without protection, SealSuite would proceed to de\-provision their accounts, potentially revoking access to critical services like Wi\-Fi and VPN for a significant portion of your workforce.

The Data Protection Rule prevents this by allowing you to set a "pause threshold". If a sync task attempts to mark more users as "departed" than your configured threshold allows—either by a percentage or a raw count—the task is automatically paused. This gives you a critical window to investigate the source of the error before any irreversible changes are made, ensuring business continuity and data integrity.

Due to the high impact of accidental de\-provisioning, we strongly recommend enabling this feature.

<span id="c51f5e0d"></span>
# How to Configure the Rule


1. Log in to the Admin Console.

2. From the left navigation bar, go to **Identity** \> **Account Setup**.

3. Click the **Directory Sync** tab.

4. From the Data source list, click the name of the data source you want to edit.

5. On the details page, go to the **Advanced settings** tab and click **Edit** in the Data Protection Rule section.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5cee84047db2411fb1e01b8da5e21fc9~tplv-goo7wpa0wc-image.image) </span>

6. Enable the **Termination data protection trigger event** toggle and set the following thresholds. If a sync task exceeds either of these thresholds, it will be automatically paused.

   * **Turnover Rate:**  A percentage (0% \- 100%). If the percentage of users marked as departed in a single sync exceeds this value, the task will be paused. Default: `10%`.

   * **Number of resignations:**  A specific number of users (5 \- 999,999). If the number of users marked as departed in a single sync exceeds this value, the task will be paused. Default: `100`.


**Recommendation:** 


* For organizations with **fewer than 100 people**, we recommend using the **Turnover Rate** threshold.

* For organizations with **more than 100 people**, we recommend using the **Number of resignations** threshold.

7. Click **Save** in the top\-right corner to apply your changes.
