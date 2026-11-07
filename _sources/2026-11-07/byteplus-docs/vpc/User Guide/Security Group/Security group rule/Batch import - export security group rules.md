---
title: "Batch import/export security group rules"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Batch-importing-or-exporting-security-group-rules"
---

## Scenarios

You can use the bulk import feature to add a large number of security group rules at once, or reuse partial rules from existing security groups to quickly complete batch additions of security group rules.

* The procedure to batch add a lot of rules to a target security group is: [Download and complete template](https://docs.byteplus.com/en/docs/vpc/Batch-importing-or-exporting-security-group-rules#.5LiL6L295bm25aGr5YaZ5qih5p2_) \> [Batch import security group rules](https://docs.byteplus.com/en/docs/vpc/Batch-importing-or-exporting-security-group-rules#.5om56YeP5a-85YWl5a6J5YWo57uE6KeE5YiZ).

* The operational process to reuse partial rules from an existing security group to batch add rules to a target security group is: [Batch export security group rules](https://docs.byteplus.com/en/docs/vpc/Batch-importing-or-exporting-security-group-rules#.5om56YeP5a-85Ye65a6J5YWo57uE6KeE5YiZ) \> [Modify security group rules](https://docs.byteplus.com/en/docs/vpc/Managing_a_security_group_rule) \> [Batch import security group rules](https://docs.byteplus.com/en/docs/vpc/Batch-importing-or-exporting-security-group-rules#.5om56YeP5a-85YWl5a6J5YWo57uE6KeE5YiZ).

## Procedures

### Download and complete the template

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Security Group**.

3. In the top menu bar, select the target project and region.

4. In the security group list, click the name of the target security group.

5. On the **Access rules** tab, click the **Inbound rule** tab or the **Outbound rule** tab.

6. Click **Import** to enter the security group rule import page.

7. Click **Download template** to download the template locally.

8. Open the downloaded template and fill it out according to the instructions below.

   > **tip**

   * > The batch import file can be named arbitrarily—there are no specific naming requirements.

   * > The file cannot be empty or contain only the header row; otherwise, it cannot be uploaded.

   * > It is recommended to include no more than 100 security group rules in the batch import file. A maximum of 100 security group rules can be imported in a single batch operation. Any rules beyond this limit will be ignored.

   * > The import file must not contain rules that duplicate existing rules in the target security group, i.e., no rule may exactly match all parameters (except the description) of an existing rule.

   |Parameters |Parameter description |Sample value |
   |---|---|---|
   |direction |The direction of a security group rule defines whether it controls traffic entering or leaving the ECSs within the security group. Supported formats are as follows:<br><br><br>* **Chinese**: 出方向 (Outbound)/入方向 (Inbound)<br><br>* **English (Capitalized)** : Egress/Ingress<br><br>* **English (Uppercase)** : EGRESS/INGRESS |Outbound |
   |Priority |The priority of a security group rule is an integer value ranging from 1 to 100. The default value is 1, which indicates the highest priority. |1 |
   |Policy |The policy for security group rules supports Allow and Deny. When two security group rules have the same priority, the Deny policy takes precedence over the Allow policy. The supported input formats are as follows:<br><br><br>* **Chinese**: 允许(Accept)/拒绝(Deny)<br><br>* **English (Capitalized)** : Accept/Deny<br><br>* **English (Uppercase)** : ACCEPT/DENY |permit |
   |Protocol type |Supports ALL, TCP, UDP, ICMP, ICMPV6, or GRE. |TCP |
   |Port range |Limit the port range based on different protocol types. Supports the following methods:<br><br><br>* Enter a single port, such as 80.<br><br>* Enter a port range, e.g., 20\-25 or 1\-65535.<br><br><br>> **tip**<br><br><br>> When the protocol type is ALL, ICMP, or ICMPV6, only ALL is supported as input.<br> |20\-25 |
   |Source/Destination address |The source or destination address of a security group rule supports entering a CIDR block, security group ID, or prefix list ID.<br><br><br>* When the rule direction is inbound, this field is the source address.<br><br>* When the rule direction is outbound, this field is the destination address. |0.0.0.0/0 |
   |Description |Description of the security group rule.<br><br><br>* Must start with a letter, Chinese character, or number. It may include half\-width commas (,), full\-width periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).<br><br>* Length limit is 1 to 255 characters.<br><br>* If left blank, this parameter defaults to an empty string. |Rule 1 |

8. After completing, close and save the file.

### Batch import security group rules

> **tip**

* > Please refer to the instructions to [Download and complete template](https://docs.byteplus.com/en/docs/vpc/Batch-importing-or-exporting-security-group-rules#.5LiL6L295bm25aGr5YaZ5qih5p2_) in advance to prepare the security group rules file for upload. Currently, the system supports uploading security group rule files in .csv and .xlsx formats.

* > Batch imported rules are added incrementally and will not overwrite existing security group rules.

* > During import, the system validates the file format and checks for duplicates with existing rules. If validation fails, please revise the file according to the error prompts and re\-upload.

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Security Group**.

3. In the top menu bar, select the target project and region.

4. Click the name of the target security group.

5. On the **Access rules** tab, click the **Inbound rule** tab or the **Outbound rule** tab.

6. Click **Import** to enter the security group rule import page.

7. Click **Upload** to upload the prepared security group rule file.

8. After the file is verified, click **Import** to complete the actions.

### Batch export Security Group rules

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Security Group**.

3. In the top menu bar, select the target project and region.

   * **Export a single security group:**

      1. Click the name of the target security group.

      2. Select the **Access rules** tab, then click the **Inbound rule** or **Outbound rule** tab.

      3. Click **Export**, and the system will automatically export the complete set of rules for this security group (including both inbound and outbound rules) and generate a file in .csv format.

   * **Export** ** multiple security groups:**

      1. Select multiple security groups.

      2. Click **Export rule**, and the system will automatically export all rules (including inbound and outbound rules) of multiple security groups and generate a .csv file.
