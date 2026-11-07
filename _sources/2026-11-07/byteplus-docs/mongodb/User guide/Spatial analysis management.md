---
title: "Spatial analysis management"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/Spatial_analysis_management"
---

The spatial analysis feature of Document Database for MongoDB is provided by Database Workshop (DBW). This feature allows you to view the space usage of your Document Database for MongoDB instance, historical space usage trends, analysis task records, and collection\-level space details, helping you identify space hotspots and assist with scaling, cleanup, and capacity planning.

<span id="Upgs5H6c"></span>
## Access via the MongoDB console


1. Log on to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the top menu bar, select the project and region for the instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click **Login DBW** in the **Actions** column of the target instance.

5. In the **Database Workshop** dialog box, after setting the login parameters, click **Log in**. For more details, refer to [Log on to the SQL window through the Document Database for MongoDB console](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-documentdb-for-mongodb?lang=en#.6YCa6L-HLWRidy3mjqfliLblj7DnmbvlvZUtc3FsLeeql-WPow==).

6. After successful login, you will enter the **DBW console**. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

7. On the **Observation and diagnosis** page, click **Space usage**, then complete the following settings:

   1. In the upper\-right corner of the page, locate the drop\-down list and select **Document Database for MongoDB** as the target database type.

   2. In the upper\-left corner of the page, locate the drop\-down list and select the target instance.

8. After entering the **Space usage** page, you can use the spatial analysis feature. For details on usage, see [Spatial analysis management](https://docs.byteplus.com/en/docs/DBW/Spatial_analysis_management?lang=en).


<span id="fGQduTpW"></span>
## Access via the DBW console

You can directly log in to the DBW console and use the spatial analysis feature. For details on usage, see [Spatial analysis management](https://docs.byteplus.com/en/docs/DBW/Spatial_analysis_management?lang=en).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Database Workshop (DBW) is a unified cloud management platform for managing the lifecycle of multiple types of databases. DBW is a database SaaS product that integrates a graphical user interface (GUI), troubleshooting, and auditing. It provides web endpoint management capabilities such as comprehensive observation and analysis, intelligent risk checks, and autonomous operations. For more details, refer to <a href="https://docs.byteplus.com/en/docs/DBW/what-is-database-workbench">What is Database Workshop</a>.</div>
