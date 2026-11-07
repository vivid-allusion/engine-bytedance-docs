---
title: "Managing the ACL"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Managing-access-control-policy-groups"
---

This topic introduces how to manage policy groups.

<span id=".5Yib5bu6562W55Wl57uE"></span>
## Create policy group


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. In the left\-side navigation pane, select **Access control**.

4. Click Create access control policy group.

5. Configure relevant parameters based on the table below.

   
   |Parameter |Explanation |Example |
   |---|---|---|
   |Policy group name |Enter the name of the policy group. |Acl\-01 |
   |Affiliated Project |Select the project to which the access control list belongs. [Learn more](https://docs.byteplus.com/en/docs/clb/Project-management) |default |
   |IP entry |Consists of IP address/IP range + remarks, each line contains one entry in the format "x.x.x.x\|remarks" or "x.x.x.0/x\|remarks".<br><br><br>* Supports adding both IPv4 and IPv6 entries simultaneously.<br><br>* IP addresses/IP ranges cannot be `0.0.0.0, 0.0.0.0/x` or `::/x`.<br><br>* IP address ranges must be in standard format, where the IP address matches the mask. For example, 192.168.0.0/16 is correct, but 192.168.1.0/16 is incorrect.<br><br>* Remarks are optional and cannot exceed 128 characters. |192.168.1.0/24 |
   |Tags |A tag consists of a key\-value pair and is used for categorizing and searching resources<br><br>Click the Add icon, input the Tag key and Tag value, and add a tag to the policy group. |* Tag key: acl\-key<br><br>* Tag value: acl\-test |
   

6. Click **Create** to complete the action.


<span id=".566h55CGSVDmnaHnm64="></span>
## Manage IP Entries

You can add or delete up to 50 IP entries at a time. Adding or deleting IP entries takes effect immediately. Proceed with caution.


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. In the left\-side navigation pane, select **Access control**.

4. Click Manage IP entries on the right of the target policy group.

   * **Add IP entry**

      1. Click Add IP Entry to add a new IP entry.

      2. Click **Add** to complete the action.

   * **Delete IP entry**

      1. Click Delete on the right side of the IP entry list to delete a single IP entry.

      2. Click **Delete** to complete the action.


<span id=".5Yig6Zmk562W55Wl57uE"></span>
## Delete policy group

Policy groups associated with listeners cannot be deleted.


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. In the left\-side navigation pane, select **Access control**.

4. Click Delete on the right side of the target ACL.

5. Click **Delete** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [CreateAcl](https://docs.byteplus.com/en/docs/clb/CreateAcl)

* [DeleteAcl](https://docs.byteplus.com/en/docs/clb/DeleteAcl)

* [DescribeAcls](https://docs.byteplus.com/en/docs/clb/DescribeAcls)

* [DescribeAclAttributes](https://docs.byteplus.com/en/docs/clb/DescribeAclAttributes)

* [AddAclEntries](https://docs.byteplus.com/en/docs/clb/AddAclEntries)

* [RemoveAclEntries](https://docs.byteplus.com/en/docs/clb/RemoveAclEntries)
