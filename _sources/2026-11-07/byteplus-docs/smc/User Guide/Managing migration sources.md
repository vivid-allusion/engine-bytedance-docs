---
title: "Managing migration sources"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Managing-Migration-Sources"
---

After importing a migration source, you can manage it on the migration source list page.

<span id="PajIVQTP"></span>
## Prerequisites

The migration source has been imported. For details, see [Importing migration sources](https://docs.byteplus.com/en/docs/smc/Import_Migration_Sources).

<span id="ECu1vFWh"></span>
## View migration source details

After the import, you can view basic information, attributes, and disk details of the migration source to confirm whether the target instance specified in the migration task supports the migration source data.


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left directory tree under any region, select "Server Migration Center \> Migration Source".

3. Select the "Import migration source" tab.

4. On the list page, you can view basic information such as the target migration source name/ID, status, and precheck status. You can also click the task name of the target migration source in the "Last migration task name/ID" column to view migration task details.

5. You can click the name of the target migration source to navigate to the migration source details page. On the details page, you can view migration source basic information (for example, migration source name, Agent version), attributes (for example, operating system, boot mode, architecture), volumes (for example, system volume capacity, number of data volumes), and other details.


<span id="IGdfWAXj"></span>
## Change migration source basic information

After importing a migration source, you can change its name in the console to distinguish between different migration sources.


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left directory tree under any region, select "Server Migration Center \> Migration Source".

3. Select the "Import migration source" tab.

4. Click the name of the target migration source to navigate to the migration source details page.

5. Click the edit button on the right of "Migration source name".

6. Enter the new name in the pop\-up window and click the "Confirm" button to complete the modification.


<span id="uvrss3u9"></span>
## Delete migration source

You can delete the migration source that is no longer used.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Only migration sources in <strong>Offline</strong>, <strong>Online</strong>, or <strong>Abnormal</strong> status can be deleted.</div>


* <div data-tips="true" data-tips-type="default">A migration source associated with migration tasks cannot be deleted. Please <a href="https://docs.byteplus.com/en/docs/smc/Managing-Migration-Jobs#m9Jk5vRY">delete the associated migration task first</a>.</div>


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left directory tree under any region, select "Server Migration Center \> Migration Source".

3. Select the "Import migration source" tab.

4. Click the "Delete" button in the Actions column of the target migration source.

5. In the pop\-up window, click "Confirm" to complete the operation.
