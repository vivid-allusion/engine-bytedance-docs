---
title: "Access control"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Access-control"
---

This topic describes how to configure IP\-based access control for listeners in the BytePlus Application Load Balancer (ALB) console.

In an ALB instance, you can configure IP access control for each listener to achieve the following functions:

* Allow requests only from specific IP addresses.

* Deny requests from specific IP addresses.

You manage a specific set of IP addresses through an access control policy group, and then associate that policy group with a listener as either an allowlist or a denylist to implement access control for that listener.

## Procedures

### Step 1: Create access control policy group

1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the target project and region.

3. In the left\-side navigation pane, select **Access control**.

4. Click **Create access control policy group.**

5. To configure the related parameters, see the table below.

   |Parameter |Explanation |Example |
   |---|---|---|
   |Name |Enter the name of the policy group. The name must meet the following requirements:<br><br><br>* Must start with an English letter or a Chinese character.<br><br>* Can only contain Chinese characters, letters, numbers, periods (.), underscores (_), and hyphens (\-).<br><br>* Length must be 1 to 128 characters. |Acl\-01 |
   |IP entry |Enter one or more IP entries. IP entry format requirements:<br><br><br>* Each entry must be on a separate line. Entries are separated by line breaks.<br><br>* The entry format can be: `x.x.x.x｜remark`, `x.x.x.0/x｜remark`, `x:x:x:x:x:x:x:x｜remark`, or `x:x:x:x:x:x:x:x/x｜remark`. The remark field is optional and cannot exceed 255 characters.<br><br>* Addresses cannot be duplicated across different lines.<br><br>* Each policy group can contain a maximum of 300 IP address entries. |192.168.1.0/24 |
   |Project |Select a project for the policy group. A Project is a resource management method provided by BytePlus. Using projects, you can group and manage your cloud resources.<br><br>If you do not select a project, the policy group will be added to the **default** project by default. |default |
   |Tags |A tag consists of a key\-value pair and is used for categorizing and searching resources [Prerequisite](https://docs.byteplus.com/en/docs/clb/Tag-Overview)<br><br>Click the Add icon, input the Tag key and Tag value, and add a tag to the policy group. |* Tag key: acl\-key<br><br>* Tag value: acl\-test |

6. Click **Save** to complete the action.

### Step 2: Configure access control for listener

1. In the left navigation pane, select **Instance**.

2. On the **Instance management** page, find the instance that requires listener access control configuration on the ALB instance list.

3. In the **Actions** column, click **Listener**.

4. In the **Listener information** tab, find the listener to configure.

5. In the **Name/ID** column, click the listener name.

6. In the **Listener details** tab, click **Edit** icon next to **Access control**.

7. On the **Configure access control** page, configure the parameters as described below.

   |Parameter |**Description** |
   |---|---|
   |Status |Determines whether access control is enabled for the listener. Default: Disabled. |
   |Control mode |Specify the method of access control. The options for this field are as follows:<br><br><br>* Allowlist: Indicates that only requests from IP addresses within the policy group are allowed. If the specified policy group does not contain any IP addresses, it means all requests are denied access to the listener.<br><br>* Denylist: Indicates that requests from IP addresses within the policy group are denied. If the specified policy group does not contain any IP addresses, it means all requests are allowed access to the listener. |
   |Policy group |Specify the policy group. You can specify up to 5 policy groups. |

8. Click **Save** to complete the action.
