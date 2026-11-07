---
title: "Releases"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Releases"
---

This article introduces each release of BytePlus Flink, including new features, enhancements, important issue resolutions, and corresponding documentation, to help you understand the release dynamics of Flink.

<span id="96db02bf"></span>
## January 2025


|**Module Name** |**Function Name** |**Function Description** |**Function Type** |
|---|---|---|---|
|Task Development |Variable Management |The new version of task development supports modules such as variable management, configuration templates, and connector management, making support more convenient |New Feature |
||Network Parameters |The product has built\-in network parameters activated, which do not require additional custom parameters when accessing across VPCs and the internet. |New Feature |
||Session Debugging |Supports session debugging with the cluster version of Flink 1.17. |New Feature |
||Assignment Type |Assignment Development Supports PyFlink Job Development (Only Supports Flink Versions After 1.17) |New Addition |
|Flink Connector |Flink CDC |1. Flink MongoDB CDC Data Source Supports Ignoring Delete Events.<br><br>2. Flink CDC Supports Paimon 0.8.2 Byte Enhanced Edition.<br><br>3. Flink CDC Supports Data Downstream for Paimon\-LAS. |Optimization |
||ByteHouse Connector |Upgrade the built\-in Connector version of ByteHouse Corporate Edition/Cloud Data Warehouse Edition to the latest stable version 1.27.109_patch5\-1.16 |Optimize |
|Official website integration |Project filtering |Support project filtering space at the top navigation of the product |Add |
||Project management |Support managing BytePlus Flink related resources by tags and other dimensions in project management |Add |
||Project sub\-accounting |Supports operations such as sub\-accounting by project and tag dimensions. |New addition |
|BytePlus Flink version |Flink 1.17 |BytePlus Flink 1.17 engine version continuously optimized, supports session debugging features, and includes support for stored procedure syntax and enhanced BytePlus version Paimon 0.8.2. |Beta release |
|Resource pool management |DNS settings |Supports setting DNS information via the resource pool interface to meet private domain access needs. |New addition |
|Task Operation and Maintenance |Task Restart |Beyond basic functions like stopping and starting tasks, additional support for one\-click task restart is provided to reduce the complexity of task operation and maintenance |Add |
|File Management |File Upload |Using file segmentation for uploads significantly enhances the efficiency and stability of uploading large files over 100MB |Add |
