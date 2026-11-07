---
title: "Password-free dashboard sharing"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Password-free_dashboard_sharing"
---

The log service supports password\-free dashboard sharing with other users. Recipients can access the dashboard via a password\-free link without configuring login permissions. This article introduces how to create a password\-free link and access the dashboard through it.

<span id="93f73774"></span>
## Prerequisites

A dashboard has been created.

<span id="be03b8b4"></span>
## 1 Create a password\-free link


1. Log in to the [Torch Log Service console](https://console.byteplus.com/tls/).

2. On the top navigation bar, select the region where the log service is located.

3. In the left navigation pane, select **Common Features** \> **Dashboard**.

4. In the dashboard list, click the target dashboard.

5. In the target dashboard, click the share icon.

6. In the **Common sharing link** panel, click C**reate new link**.

7. Set the following parameters, then click **OK**.

   
   |Parameter |Description |
   |---|---|
   |Name |Set the name of the password\-free link. |
   |cut\-off time |Set the valid time range for the password\-free link.<br><br><br>* **long\-term effective**: the password\-free link remains valid indefinitely.<br><br>* **Specify a deadline**: the password\-free link expires after the deadline and can no longer access the corresponding dashboard. |
   |access restrictions |Specify the users who can access this password\-free link.<br><br><br>* **Unlimited**: Users with this link can access it.<br><br>* **Specify a  BytePlus account**: Enter the specified BytePlus account ID; only this user can access the password\-free link. |
   |Time range |Set the search time range for the dashboard and charts.<br><br><br>* **Default time range for each chart**: use the chart's default query time range.<br><br>* **Custom time**: the query time range for custom charts. |
   |Filters and variables |After using filters and variables on the dashboard, shared dashboards or charts retain this information and support dynamic adjustment of charts based on selected filters and variables. |
   

8. Copy the password\-free link.


<span id="749a4d8d"></span>
## 2 Access the dashboard via the password\-free link

After sharing the password\-free link you created with other users, they can directly access and view the corresponding dashboard through that link.

<span id="13738e4d"></span>
## IAM user operation permissions

To ensure data security and precise management, you can authorize IAM users to specify their resource scope when operating password\-free links. The minimum operation permission policy for password\-free links is explained as follows:

<span id="929f61a0"></span>
### Create a password\-free link

After granting, IAM users can only create password\-free links in the specified dashboard.

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "tls:CreateDashboardShare"
            ],
            "Resource": [
                "trn:tls:{$region}:{{accountId}}:project/{{projectId}}/dashboard/{{dashbordID}}"
            ]
        }
    ]
}
```


<span id="ed4c6500"></span>
### Edit password\-free link

After granting, IAM users can only edit the specified password\-free link.

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "tls:ModifyDashboardShare"
            ],
            "Resource": [
                "trn:tls:{$region}:{{accountId}}:project/{{projectId}}/dashboard/{{dashbordID}}"，
                "trn:tls:{$region}:{{accountId}}:project/{{projectId}}/dashboard/{{dashbordID}}/share/{{ticketID}}"
            ]
        }
    ]
}
```


<span id="d0b21e9d"></span>
### Delete password\-free link

After granting, IAM users can only delete the specified password\-free link.

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "tls:DeleteDashboardShare"
            ],
            "Resource": [
                "trn:tls:{$region}:{{accountId}}:project/{{projectId}}/dashboard/{{dashbordID}}"，
                "trn:tls:{$region}:{{accountId}}:project/{{projectId}}/dashboard/{{dashbordID}}/share/{{ticketID}}"
            ]
        }
    ]
}
```


<span id="43b4c1bb"></span>
### Query password\-free link list

After granting, IAM users can only view the list of password\-free links in the specified dashboard.

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "tls:DescribeDashboardShares"
            ],
            "Resource": [
                "trn:tls:{$region}:{{accountId}}:project/{{projectId}}/dashboard/{{dashbordID}}"
            ]
        }
    ]
}
```


<span id="af081fbf"></span>
### Change the availability status of the password\-free link

After granting, IAM users can only change the availability status of the specified password\-free link.

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "tls:ModifyDashboardShareAvailable"
            ],
            "Resource": [
                "trn:tls:{$region}:{{accountId}}:project/{{projectId}}/dashboard/{{dashbordID}}"，
                "trn:tls:{$region}:{{accountId}}:project/{{projectId}}/dashboard/{{dashbordID}}/share/{{ticketID}}"
            ]
        }
    ]
}
```


<span id="9978d978"></span>
## Related actions


* Delete password\-free link

   You can find the target link in the **normal sharing link** panel and click **Delete** to remove the password\-free link.

   After deletion, you will no longer be able to access the corresponding dashboard through this link.

* Edit password\-free link

   You can find the target link in the **normal sharing link** panel and click **Edit** to modify the password\-free link settings.
