---
title: "IAM FAQs"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Identity-and-Access-Management-FAQs"
---

* [Why does the VPN gateway resource list show only the IDs of associated cloud resources (such as Virtual Private Cloud, Elastic Compute Service) but not their names?](https://docs.byteplus.com/en/docs/52/5087#.5Li65LuA5LmIVlBO572R5YWz6LWE5rqQ5YiX6KGo5Lit5Y-q5pi-56S65YWz6IGU5LqR6LWE5rqQ77yI5aaC56eB5pyJ572R57uc44CB5LqR5pyN5Yqh5Zmo77yJ55qESUTvvIzkuI3mmL7npLrlkI3np7DvvJ8=)

* [How do IAM users use the VPN Connect feature?](https://docs.byteplus.com/en/docs/52/5087#.5a2Q55So5oi35aaC5L2V5L2_55SoVlBO6L-e5o6l5Yqf6IO977yf)

* [How do IAM users use tag features?](https://docs.byteplus.com/en/docs/52/5087#.5a2Q55So5oi35aaC5L2V5L2_55So5qCH562-5Yqf6IO977yf)

* [Why can't IAM users view monitoring data?](https://docs.byteplus.com/en/docs/52/5087#.5Li65LuA5LmI5a2Q55So5oi35peg5rOV5p-l55yL55uR5o6n5pWw5o2u77yf)

* [Why can't VPN gateway routes and SSL client certificates be migrated between projects?](https://docs.byteplus.com/en/docs/52/5087#.5Li65LuA5LmIVlBO572R5YWz6Lev55Sx44CBU1NM5a6i5oi356uv6K-B5Lmm5peg5rOV6L-B56e76aG555uu77yf)


<span id=".5Li65LuA5LmIVlBO572R5YWz6LWE5rqQ5YiX6KGo5Lit5Y-q5pi-56S65YWz6IGU5LqR6LWE5rqQ77yI5aaC56eB5pyJ572R57uc44CB5LqR5pyN5Yqh5Zmo77yJ55qESUTvvIzkuI3mmL7npLrlkI3np7DvvJ8="></span>
## Why does the VPN gateway resource list show only the IDs of associated cloud resources (such as Virtual Private Cloud, Elastic Compute Service) but not their names?

This occurs because the account you are using is an IAM user, and this IAM user has not been granted global permissions for the corresponding associated resources.

If you need to view detailed information about related resources, you must use the root account to configure global permissions for the associated resources for this IAM user. For detailed configuration, see [Policy Overview](https://docs.byteplus.com/en/docs/6257/65058).

<span id=".5a2Q55So5oi35aaC5L2V5L2_55SoVlBO6L-e5o6l5Yqf6IO977yf"></span>
## How can IAM users use the VPN Connect feature?

IAM users without VPN Connect permissions cannot use the VPN Connect feature. If an IAM user needs this feature, the main account to which the IAM user belongs must authorize the relevant VPN Connect permissions (global or project permissions) for the IAM user.

<span id=".5o6I5LqI5a2Q55So5oi35YWo5bGA5p2D6ZmQ"></span>
#### Grant global permissions to an IAM user

An IAM user granted full project resource permissions for a feature is called a **global IAM user** and can manage all resources under all projects. In the VPN Connect product, a global IAM user granted all project resources for the VPN Connect feature can manage all VPN Connect resources under all projects.


1. Log in to the IAM console using the main account of the IAM user.

2. In left\-side navigation pane of the **IAM** console, click **User**.

3. On the **User** page, click the username of the IAM user to be authorized to enter the **User detail** page.

4. Click **Policy**, in **Directly Add Policy** section, click **Authorize** to add system preset policy permissions for the IAM user.

   
   |Policy name |Supported action |
   |---|---|
   |VPNFullAccess |Full read\-write access for VPN Connects. |
   


<span id=".5o6I5LqI5a2Q55So5oi35oyH5a6a6aG555uu5p2D6ZmQ"></span>
#### Grant the IAM user specified project permissions

An IAM user granted VPN Connect permissions for a specific project can only access resources within that project.


1. Log in to the IAM console using the main account.

2. In the left navigation pane, select **User Management \> User** to open the user list page.

3. Click the target IAM user's name to open the user details page.

4. Click **Authorize** to enter the Add authorization page.

5. Select one or more policies according to your requirements, and choose the projects (such as default) where the policies apply in the scope column.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Policy: defines the operation scope, resource scope, and permission conditions, such as read\-only for VPN Connect resources.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Scope of effect: defines the scope where the policy is effective, such as allowing access only to VPN resources under the default project.   </div>
   

6. Click **Submit** to complete the action.


<span id=".5a2Q55So5oi35aaC5L2V5L2_55So5qCH562-5Yqf6IO977yf"></span>
## How do IAM users use tag features?


1. Log in with the main account that the IAM user belongs to and enter Identity and Access Management (IAM).

2. In left\-side navigation pane of the **IAM** console, click **Permission policy**.

3. Click **Create policy** and create a new custom policy with reference to the example below, granting global permissions to call TagResources, UntagResources, and ListTagsForResource.

   ```Plain Text
   {
       "Statement":[
           {
               "Effect":"Allow",
               "Action":[
                   "vpc:TagResources",
                   "vpc:UntagResources",
                   "vpc:ListTagsForResources"
               ],
               "Resource":[
                   "*"
               ]
           }
       ]
   }
   ```
   

5. In the left\-side navigation pane, click **User**.

6. On the **User** page, click the username of the IAM user to be authorized to enter the **User detail** page.

7. Click **Permissions**, then under **Global Policy**, click the **Add Permissions** button.

8. Assign the newly created custom policy permissions to the IAM user.


<span id=".5Li65LuA5LmI5a2Q55So5oi35peg5rOV5p-l55yL55uR5o6n5pWw5o2u77yf"></span>
## Why can't IAM users view monitoring data?

After an IAM user is granted VPN Connect permissions, they must also be authorized by the root account to which the IAM user belongs with CloudMonitor permissions to view monitoring data.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The collection of monitoring metrics depends on Cloud Monitor, which is currently in public preview. You need to enable the Cloud Monitor trial before accessing monitoring data.</div>



1. Use the root account to which the IAM user belongs to log in to the IAM console.

2. In left\-side navigation pane of the **IAM** console, click **User**.

3. Click the username of the IAM user to be authorized to enter the User detail page.

4. Click **Authorize** and add system default CloudMonitor policy permissions to the IAM user as needed.

   
   |Policy name |Supported action |
   |---|---|
   |CloudMonitorFullAccess |Management permissions for CloudMonitor. With this policy, the IAM user can both view monitoring data and use features of the CloudMonitor. |
   |CloudMonitorReadOnlyAccess |Access permissions for CloudMonitor. With this policy, the IAM user can view monitoring data only. |
   


<span id=".5Li65LuA5LmIVlBO572R5YWz6Lev55Sx44CBU1NM5a6i5oi356uv6K-B5Lmm5peg5rOV6L-B56e76aG555uu77yf"></span>
## Why can't VPN gateway routes and SSL client certificates migrate projects?

VPN gateway routes and SSL client certificates are sub\-resources and do not support separate project migration.


* VPN gateway routes are sub\-resources of the VPN gateway. They can only be migrated together with the VPN gateway and cannot be migrated separately between projects.

* SSL client certificates are sub\-resources of the SSL server. They can only be migrated together with the SSL server and cannot be migrated separately between projects.
