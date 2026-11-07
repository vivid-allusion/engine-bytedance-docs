---
title: "LogCollector collection rule management"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/logcollector_collection_rule_management"
---

This topic describes how to manage LogCollector collection rules in the Torch Log Service (TLS) console, including modifying a collection rule, modifying the host groups associated with a collection rule, and deleting a collection rule.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information on how to create a LogCollector collection rule, refer to <a href="https://docs.byteplus.com/docs/tls/single_line_full_text_mode">Collect logs in Single\-line full\-text mode</a>.</div>


<span id=".5p-l55yL6YeH6ZuG6YWN572u5L-h5oGv"></span>
## View collection rule information

After a collection rule is created, you can view its basic information in the console.


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS resides.

3. In the left\-side navigation pane, choose **Common Functions** \> **Log Collection**.

4. In the **LogCollector** page, click the name of the collection rule that you want to view.

   On the upper\-right corner of the page, enter the name or ID of a log topic or the name or ID of a collection rule in the search box to search for collection rules.

5. View the information about the collection rule.

   On the page, the basic information about the collection rule, the configurations of the collection rule, and the host groups associated with collection rule are displayed.

   * **Basic information**: The name and ID of the collection rule, the name and ID of the associated log topic, and the creation time of the collection rule are displayed.

   * **Collection rule**: The detailed information about the collection rule, including the collection paths, collection mode, and advanced settings such as filters are displayed.

   * **Host group information**: The name and ID of each host group, the number of hosts in each host group, and the number of hosts in each heartbeat status are displayed. If some hosts in a host group are in the abnormal heartbeat status, get the IP addresses of the hosts and troubleshoot the issue. For more information on how to get the IP address of a host, refer to [View heartbeat statuses of hosts](https://docs.byteplus.com/docs/tls/View_a_host_group#%E6%9F%A5%E7%9C%8B%E5%BF%83%E8%B7%B3%E7%8A%B6%E6%80%81). For more information on troubleshooting methods, refer to [Host group heartbeat issues on a host](https://docs.byteplus.com/docs/tls/host_group_heartbeat_issues_on_a_host).


<span id=".5L-u5pS56YeH6ZuG6KeE5YiZ"></span>
## Modify a collection rule

After a collection rule is created and issued to LogCollector, LogCollector parses and collects logs from the specified paths and store logs in TLS according to the rule. If the log path, log type, and other configurations change, you must promptly modify the collection rule in the TLS console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The project and topic associated with the collection rule cannot be changed.</div>



1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS resides.

3. In the left\-side navigation pane, choose **Common Functions** \> **Log Collection**.

4. In the **LogCollector** page, click the name of the collection rule that you want to modify.

   On the upper\-right corner of the page, enter the name or ID of a log topic or the name or ID of a collection rule in the search box to search for collection rules.

5. On the upper\-right corner of the page, Click **Edit collection rule** to reset the collection path, collection mode, and other configurations.

6. Click **OK**.


<span id="5253bb5a"></span>
## Import collection rules

TLS supports batch import of collection rules for the specified topics.


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS resides.

3. In the left\-side navigation pane, choose **Common Functions** \> **Log Collection**.

4. On the **LogCollector** tab, click **Import Collection Rules**.

5. In the **collection rule import task** panel, complete the following configuration and click **Next step: Execute the task** .

   
   |Parameter |Description |
   |---|---|
   |Source region |Select the region where the collection rule to be imported is located. |
   |Source project |Select the project where the collection rule to be imported is located. |
   |Source acquisition rule |Select the collection rule to be imported, and import up to 100 collection configurations at a time. |
   |acquisition rule configuration |Set the relevant rule for the new collection rules.<br><br><br>* **New acquisition rule name** : Set the name of the new collection rule.<br><br>* **Target topic** : Bind the imported collection rule to the specified topic.<br><br>* **rule configuration** : Bind host group and set collection path for new collection rule.<br><br>   Importing collection paths and host groups for source collection rules is not supported. |
   

6. After confirming that the topic import task is complete, click **Finish** .


<span id=".5L-u5pS55a-55bqU5py65Zmo57uE"></span>
## Modify the host groups associated with a collection rule

A collection rule must be associated with a host group. After a collection rule is associated with a host group, TLS issues the collection rule to the hosts in the host group, then LogCollector on each host collects log data according to the collection rule. When creating a collection rule, you must specify a host group. If the servers that are used for your project or application are changed, modify the host group associated with the collection rule to change the log sources.


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS resides.

3. In the left\-side navigation pane, choose **Common Functions** \> **Log Collection**.

4. In the **LogCollector** pane, click the name of the collection rule that you want to modify.

   On the upper\-right corner of the page, enter the name or ID of a log topic or the name or ID of a collection rule in the search box to search for collection rules.

5. Click **Modify host group** on the upper\-right corner of the page to set a new host group.

6. Click **Submit**.


<span id=".5Yig6Zmk6YeH6ZuG6YWN572u"></span>
## Delete collection rules

If you no longer need to collect log data according to a collection rule, delete the collection rule.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After you delete a deleted collection rule, it cannot be restored. Proceed with caution.</div>


* <div data-tips="true" data-tips-type="tip">After a collection rule is deleted, LogCollector on the hosts in the host groups associated with the collection rule stops collecting and reporting log data based on the collection rule, but the data already collected is retained until it expires.</div>


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS resides.

3. In the left\-side navigation pane, choose **Common Functions** \> **Log Collection**.

4. In the **LogCollector** pane, find the collection rule you want to delete and click **Delete** in the **Action** column.

5. In the dialog box that appears, confirm the information about the collection rule and click **OK**.
