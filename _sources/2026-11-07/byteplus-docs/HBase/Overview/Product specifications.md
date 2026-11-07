---
title: "Product specifications"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Product_specifications"
---

This topic describes the instance specifications and storage types of Table Storage for HBase.

<span id=".6K6h566X6KeE5qC8"></span>
## Instance specifications

Instance specifications include the specifications for Master and Region Server nodes, as shown in the following table:


|Specification code |CPU |Memory |Supported node types |
|---|---|---|---|
|hbase.x1.large |4C |8 GiB |Thrift Server |
|hbase.x1.2xlarge |8C |16 GiB |Thrift Server |
|hbase.x1.4xlarge |16C |32 GiB |* Master<br><br>* Region Server |
|hbase.x2.4xlarge |16C |64 GiB |* Master<br><br>* Region Server |
|hbase.x1.8xlarge |32C |64 GiB |Region Server |


<div data-tips="true" data-tips-type="tip">Description</div>


<div data-tips="true" data-tips-type="tip"> If the available specifications cannot meet your service requirements, <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> to contact technical support.</div>


<span id="GLVjSLjA"></span>
## Storage type

HBase provides three storage types, as detailed in the following table:


|Storage type |Description |Storage range |
|---|---|---|
|HDD file storage |HDD disks are more affordable than SSD disks, making them suitable for scenarios that require large data storage and high cost\-effectiveness. |100GiB~20,000GiB |
|SSD file storage |SSD disks offer fast read/write speeds and low latency, making them ideal for scenarios that require frequent read/write operations and high performance. |100GiB~20,000GiB |
|Capacity storage |Capacity storage can be used as a cold data storage medium to store infrequently used data, reducing storage costs. |800GiB~1,000,000GiB |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the current storage range does not meet your business needs, you can <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> to contact technical support for a limit increase.</div>
