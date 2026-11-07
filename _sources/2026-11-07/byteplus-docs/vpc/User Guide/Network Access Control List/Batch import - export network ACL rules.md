---
title: "Batch import/export network ACL rules"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Batch_import_or_export_network_ACL_rules"
---

You can refer to this topic to quickly complete the batch configuration of network ACL rules.

## Action notes

* A maximum of 100 network ACL rules can be imported at a time. Any rules beyond 100 will not be imported.

* Batch\-imported network ACL rules are added incrementally and will not overwrite existing network ACL rules. You can use this feature with confidence.

## Procedures

**Batch import new network ACL rules**

**1. Download and fill in the template**

   1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

   2. In the left\-side navigation pane, select **Network ACL**.

   3. In the top menu bar, select the target project and region.

   4. In the Network ACL list, click the name of the target Network ACL.

   5. On the **Inbound rule** or **Outbound rule** tab, click **Import**.

   6. Click **Download template** to download the template locally.

   7. Open the downloaded template and fill it out according to the instructions below.

      > **tip**

      * > The batch import file can be named arbitrarily—there are no specific naming requirements.

      * > The file cannot be empty or contain only the header row; otherwise, it cannot be uploaded.

      |Parameters |Parameter description |Sample value |
      |---|---|---|
      |Policy |The policy for network ACL rules supports Allow and Deny. The supported input formats are as follows:<br><br><br>* **Chinese**: 允许(Accept)/拒绝(Deny)<br><br>* **English (Capitalized)** : Accept/Deny<br><br>* **English (Uppercase)** : ACCEPT/DENY |Allow |
      |Agreement |Supports ALL, TCP, UDP, ICMP, ICMPV6, or GRE. |TCP |
      |Source address/destination address |Enter the source IP address for inbound traffic or the destination IP address for outbound traffic. |0.0.0.0/0 |
      |Destination port |Enter the port number of the destination address for the outbound/inbound rule.<br><br>Limit the port range based on different protocol types. Supports the following methods:<br><br><br>* Enter a single port, such as 80.<br><br>* Enter a port range, such as 20\-25.<br><br>* Enter all ports:<br><br>   * For TCP or UDP protocol, enter 1\-65535.<br><br>   * For ALL, ICMP, or ICMPV6 protocol, enter ALL.<br><br><br>> **tip**<br><br><br>> When the protocol type is ALL, ICMP, or ICMPV6, only ALL is supported as input.<br> |80 |
      |Description |Description of the network ACL rule.<br><br><br>* Must start with a letter, Chinese character, or number. It may include half\-width commas (,), full\-width periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).<br><br>* Length limit is 1 to 255 characters.<br><br>* If left blank, this parameter defaults to an empty string. |Rule 1 |

   8. After completing, close and save the file.

**2. Batch import network ACL rules**

> **tip**

> Refer to the "Download and fill in the template" section above to prepare the network ACL rule file to be uploaded in advance. Currently, network ACL rule files in .csv and .xlsx formats are supported for upload.

> During import, the file format and potential conflicts with existing network ACL rules are verified. If the verification fails, modify the file according to the prompts and import it again.

   1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

   2. In the left\-side navigation pane, select **Network ACL**.

   3. In the top menu bar, select the target project and region.

   4. Click the name of the target Network ACL.

   5. On the **Inbound rule** or **Outbound rule** tab, click **Import**.

   6. Click **Upload** and upload the prepared network ACL rule file.

   7. After the file is verified, click **Import** to complete the actions.

**Reuse existing network ACL rules**

**1. Batch export network ACL rules**

Export the rules of the target network ACL.

   1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

   2. In the left\-side navigation pane, select **Network ACL**.

   3. In the top menu bar, select the target project and region.

   4. Click the name of the target Network ACL.

   5. On the **Inbound rule** or **Outbound rule** tab, click **Export**. The system will automatically export all rules of the network ACL (including both inbound and outbound rules) and generate a file in .csv format.

**2. Modify network ACL rules**

Open the network ACL rule file exported in the previous step, and add, modify, or delete network ACL rules as needed.

**3. Batch import network ACL rules**

Import the modified network ACL rule file into a new network ACL.

   1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

   2. In the left\-side navigation pane, select **Network ACL**.

   3. In the top menu bar, select the target project and region.

   4. Click the name of the target Network ACL.

   5. On the **Inbound rule** or **Outbound rule** tab, click **Import**.

   6. Click **Upload** and upload the prepared network ACL rule file.

   7. After the file is verified, click **Import** to complete the actions.
