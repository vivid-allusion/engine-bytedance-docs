---
title: "IAM FAQs"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/IAM_FAQs"
---

* [Why do the resource lists in Direct Connect only display the IDs of associated cloud resources (such as VPCs and CENs) and not their names?](https://docs.byteplus.com/en/docs/53/78993#.5Li65LuA5LmI5LiT57q_6L-e5o6l6LWE5rqQ5YiX6KGo5Lit5Y-q5pi-56S65YWz6IGU5LqR6LWE5rqQ77yI5aaC56eB5pyJ572R57uc44CB5LqR5LyB5Lia572R77yJ55qESUTvvIzkuI3mmL7npLrlkI3np7DvvJ8=)

* [How can an IAM user use the Direct Connect feature?](https://docs.byteplus.com/en/docs/53/78993#.5a2Q55So5oi35aaC5L2V5L2_55So5LiT57q_6L-e5o6l5Yqf6IO977yf)

* [How do IAM users use tag features?](https://docs.byteplus.com/en/docs/53/78993#.5a2Q55So5oi35aaC5L2V5L2_55So5qCH562-5Yqf6IO977yf)

* [Why can't IAM users view monitoring data?](https://docs.byteplus.com/en/docs/53/78993#.5Li65LuA5LmI5a2Q55So5oi35peg5rOV5p-l55yL55uR5o6n5pWw5o2u77yf)

* [The IAM user has been granted project-scoped permissions for the Direct Connect system policy, but why can the user still not use Direct Connect normally?](https://docs.byteplus.com/en/docs/53/78993#.5bey5Li65a2Q55So5oi35o6I5LqI5LqG5LiT57q_57O757uf562W55Wl55qE6aG555uu5p2D6ZmQ77yM5Li65LuA5LmI5LuN5peg5rOV5q2j5bi45L2_55So5LiT57q_6L-e5o6l77yf)


<span id=".5Li65LuA5LmI5LiT57q_6L-e5o6l6LWE5rqQ5YiX6KGo5Lit5Y-q5pi-56S65YWz6IGU5LqR6LWE5rqQ77yI5aaC56eB5pyJ572R57uc44CB5LqR5LyB5Lia572R77yJ55qESUTvvIzkuI3mmL7npLrlkI3np7DvvJ8="></span>
## Why do the resource lists in Direct Connect only display the IDs of associated cloud resources (such as VPCs and CENs) and not their names?

This occurs because the account you are using is an IAM user, and this IAM user has not been granted global permissions for the corresponding associated cloud resources (like VPC or CEN).

If you need to view the detailed information of these related cloud resources, the root account must configure global permissions for the associated resources for this IAM user. For detailed instructions on permission configuration, see [Policy management](https://docs.byteplus.com/en/docs/6257/65058).

<span id=".5a2Q55So5oi35aaC5L2V5L2_55So5LiT57q_6L-e5o6l5Yqf6IO977yf"></span>
## How can an IAM user use the Direct Connect feature?

An IAM user cannot use Direct Connect features without the appropriate permissions. If an IAM user needs to use Direct Connect, the root account to which the IAM user belongs must authorize the IAM user.


1. Log in to the BytePlus [IAM console](https://console.byteplus.com/iam/identitymanage/user) using the root account which the IAM user belongs.

2. In the **IAM** console left\-side navigation pane, click **User**.

3. On the **User** page, click the username of the IAM user to be authorized to enter the **User detail** page.

4. Click **Authorize** to add system default policy permissions for the IAM user.

   
   |Policy name |Supported action |
   |---|---|
   |DirectConnectFullAccess |Grants full read and write access to the Direct Connect service. |
   


<span id=".5a2Q55So5oi35aaC5L2V5L2_55So5qCH562-5Yqf6IO977yf"></span>
## How do IAM users use tag features?

After an IAM user is granted Direct Connect permissions, if they need to use the tag feature, the root account must also grant them tag\-related permissions. For more information, see [Roles or policies required for DC features](https://docs.byteplus.com/en/docs/directconnect/Configuration-example-of-custom-policy#.5LiT57q_6L-e5o6l5Yqf6IO95L6d6LWW55qE6KeS6Imy5oiW562W55Wl).


1. Log in to the BytePlus [IAM console](https://console.byteplus.com/iam/identitymanage/user) using the root account to which the IAM user belongs.

2. In the **IAM** console left\-side navigation pane, click **Permission policy**.

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



4. In the left\-side navigation pane, click **User**.

5. On the **User** page, click the username of the IAM user to be authorized to enter the **User detail** page.

6. Click **Authorize**.

7. Assign the newly created custom policy permissions to the IAM user.


<span id=".5Li65LuA5LmI5a2Q55So5oi35peg5rOV5p-l55yL55uR5o6n5pWw5o2u77yf"></span>
## Why can't IAM users view monitoring data?

After an IAM user is granted Direct Connect permissions, if they need to view monitoring data, the root account must also grant them CloudMonitor\-related permissions. For more information, see [Roles or policies required for DC features](https://docs.byteplus.com/en/docs/directconnect/Configuration-example-of-custom-policy#.5LiT57q_6L-e5o6l5Yqf6IO95L6d6LWW55qE6KeS6Imy5oiW562W55Wl).


1. Log in to the BytePlus [IAM console](https://console.byteplus.com/iam/identitymanage/user) using the root account to which the IAM user belongs.

2. In the **IAM** console left\-side navigation pane, click **User**.

3. On the **User** page, click the username of the IAM user to be authorized to enter the **User detail** page.

4. Click **Authorize** and add system default CloudMonitor policy permissions to the IAM user as needed.

   
   |Policy name |Supported action |
   |---|---|
   |CloudMonitorFullAccess |Management permissions for CloudMonitor. With this policy, the IAM user can both view monitoring data and use CloudMonitor features. |
   |CloudMonitorReadOnlyAccess |Access permissions for CloudMonitor. With this policy, the IAM user can view monitoring data only. |
   


<span id=".5bey5Li65a2Q55So5oi35o6I5LqI5LqG5LiT57q_57O757uf562W55Wl55qE6aG555uu5p2D6ZmQ77yM5Li65LuA5LmI5LuN5peg5rOV5q2j5bi45L2_55So5LiT57q_6L-e5o6l77yf"></span>
## The IAM user has been granted project\-scoped permissions for the Direct Connect system policy, but why can the user still not use Direct Connect normally?

Currently, within the Direct Connect service, only DC Connection and Direct Connect Gateway support the Project Management capability. Virtual Interface does not support this yet. If an IAM identity is granted only **Project permissions** for the DirectConnectFullAccess or DirectConnectReadOnlyAccess policy, the IAM identity will not be able to view or use the full Direct Connect functionality.

To properly use Direct Connect resources, a custom policy within the policy permission scope need to be created and granted the IAM user. For specific actions, see [Instructions for IAM users on using Direct Connect policies and permissions configuration](https://docs.byteplus.com/en/docs/directconnect/Configuration-example-of-custom-policy#.5a2Q55So5oi35L2_55So5LiT57q_6L-e5o6l562W55Wl5Y-K5p2D6ZmQ6YWN572u6K-05piO).
