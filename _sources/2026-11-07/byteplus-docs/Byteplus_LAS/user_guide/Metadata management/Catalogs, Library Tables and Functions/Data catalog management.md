---
title: "Data catalog management"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Data_Catalog_Management"
---

## **What is a Data Catalog (Catalog)**

The AI Data Lake Service (LAS) metadata management adopts a three\-layer entity structure: Catalog/Database/Table. Each tenant has one default Catalog (hive), and you can also create other Catalogs. Under each Catalog, there can be multiple Databases, and each Database can contain multiple Tables.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee150cc3466c404fbc5e49698440cd16~tplv-goo7wpa0wc-image.image)

## **Applicable Scenarios**

Mainly applicable to scenarios requiring metadata isolation, such as different clusters, business units, or organizational teams. By binding different Catalogs, metadata in different Catalogs is mutually invisible.

## **Basic Operations**

### **Query Data Catalog (Catalog)**

1. Log in to the LAS Console.

2. Select **Catalog**.

3. On the Catalog page, click the name of the catalog you wish to query to enter the details page and view details.

### **Edit Data Catalog (Catalog)**

> **说明**

* > Users can only edit data catalogs for which they have permission; currently, modifying the catalog name is not supported.

* > The data storage path only supports TOS paths.

* > After changing the storage path of a Catalog, if the storage path of the default DB is empty or not a TOS path, the storage path of the default DB will be updated to: "Catalog path/default.db".

1. Log in to the LAS Console.

2. From the menu, select: **Catalog**.

3. Select the data catalog you wish to edit, then click **Edit** in the upper right corner.

4. Modify the storage path or notes in the popup window.

### Create Data Catalog (Catalog)

1. Log in to the LAS Console.

2. From the menu, select: **Catalog**.

3. Click “ **＋** ” above the data catalog, and in the **Create Data Catalog** popup window, fill in the catalog name, storage location, and notes. After filling in the information, click **Confirm** to complete the creation of the data catalog.

### Delete Data Catalog (Catalog)

1. Log in to the LAS Console.

2. From the menu, select: **Catalog**.

3. Select the data catalog to be deleted, click **Delete** in the upper right corner to complete the deletion of the Catalog.

> **说明**

* > Users can only delete data catalogs for which they have permission.

* > Deleting a Catalog follows the order of deleting child nodes first, then parent nodes. That is, delete the DB first, then delete the Catalog. Similarly, when deleting a DB, delete the Tables under the DB first, then delete the DB.

* > Deleting Table/DB/Catalog follows the order of deleting metadata first, then deleting the file directory corresponding to the storage location. The actions of deleting metadata and deleting files do not guarantee transactional consistency. That is, metadata may be deleted successfully while the file directory still exists. In other words, there may be cases where the Catalog/DB/Table cannot be found, but the corresponding file directory remains.

* > When deleting a data directory, the files will also be deleted. However, the current file deletion does not support a recycle bin function; once deleted, recovery is not possible. To enable recovery of accidentally deleted data, multi\-version control must be enabled in TOS. For detailed instructions, please refer to: [Version Control](https://www.volcengine.com/docs/6349/145534).

* > When deleting a Catalog, the DBs are deleted first. If an error occurs while deleting a particular DB, the DBs that have already been deleted will not be rolled back. Users can refresh the page and continue deleting DBs that have not yet been deleted.
