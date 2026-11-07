---
title: "Adding/Deleting a prefix list entry"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Managing-entries-in-the-prefix-list"
---

<span id=".5re75Yqg5YmN57yA5YiX6KGo5p2h55uu"></span>
## Add a prefix list entry

<span id=".5pON5L2c6K-05piO"></span>
### Instructions


* The prefix list entries to be added must meet all configuration constraints of the network resources that reference this list.

* A single prefix list can hold a maximum of 200 entries.

* After adding prefix list entries, all resources referencing the prefix list will have the corresponding rules or entries automatically added in real time. Please proceed with caution.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedures


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Prefix List**.

3. In the top menu bar, select the target project and region.

4. Click the prefix list name.

5. On the item list tab, click **Add Entry**.

   
   |Parameters |Notes |Sample value |
   |---|---|---|
   |Configuration mode |Select the configuration method, supporting **Single** entry input and **Batch** input. |Batch |
   |Prefix List Entry |* When the configuration method is set to **Single**, input a single CIDR, such as 10.0.0.0/24.<br><br>   Click  **+Add entry** to add multiple prefix list entries sequentially.<br><br>* When the configuration method is set to **Batch** input, input multiple CIDRs under the following requirements:<br><br>   * Enter one entry per line, separated by a carriage return.<br><br>   * Separate the address/CIDR block and its remark within an entry using a "\|" symbol. The remark must be between 0 and 255 characters in length.<br><br>   * Add up to 50 entries in a single operation.<br><br>   * Duplicate CIDR blocks are not allowed. A single IP address will be automatically converted to a /32 prefix for validation purposes. |10.0.0.1/32 \| Example 1<br><br>10.0.0.2/32 \| Example 2<br><br>10.0.0.3/32 \| Example 3<br><br>10.0.0.4 \| Example 3 |
   

6. Click **Add** to complete the action.


<span id=".5Yig6Zmk5YmN57yA5YiX6KGo5p2h55uu"></span>
## Delete a prefix list entry

After deleting prefix list entries, all network resources referencing this list will have the corresponding rules or entries automatically removed. Please proceed with caution.


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Prefix List**.

3. In the top menu bar, select the target project and region.

4. Click the prefix list name.

5. In the entry list tab, click **Delete**on the right side of the target entry.

6. After selecting **I have confirmed that deleting the above entry has no business impact**. Click **Delete** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[ModifyPrefixList](https://docs.byteplus.com/en/docs/vpc/ModifyPrefixList)
