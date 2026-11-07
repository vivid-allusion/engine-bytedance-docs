---
title: "FAQ"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/intelligent-cache-faq"
---

<span id="9aa90f16"></span>
# What is the purpose of virtual warehouse local disk?

The primary function of virtual warehouse local disk is to accelerate the read performance of remote data in an architecture where storage and computation are separated. By default, ByteHouse Cloud Data Warehouse (CDW) uses a write\-through approach, writing data directly to remote persistent distributed storage. Subsequent SQL read operations trigger data retrieval, returning the data to the local disk.

If you want to manually trigger cache extraction and loading, refer to [Preload ](https://docs.byteplus.com/docs/bytehouse/docs-query-acceleration-preload).

<span id="b069d0c6"></span>
# How is the local disk space divided?

Files stored in local disk mainly include data blocks, metadata, unique index files, temporary BSP disk files, temporary files for foreground insert operations and background data merging, and more. Data blocks account for approximately 70% to 80%, while indexes and temporary files account for around 10%.

If you need detailed information about proportions or require targeted adjustments, you can submit a ticket or contact the ByteHouse team.

<span id="e294547b"></span>
# If the error 'Cannot reserve 1 MB, not enough space' occurs, how should this be handled?

When the SQL exception displays the `Cannot reserve xx MB, not enough space` error message, it is typically caused by insufficient reserved local temporary file space. Possible reasons for this issue include an increase or higher frequency of insert operations on the frontend, a larger number of rows being batched, more frequent data merges on the backend, or merging files that are too large.

Additionally, ByteHouse CDW allows you to configure separate compute groups for reading and writing. If you set the read and write virtual warehouses to be the same virtual warehouse, this issue is more likely to occur.

You can resolve this in the following ways:


* If you have not yet purchased virtual warehouse local disk, the default general\-purpose 1:4 virtual warehouse comes with 200 GB of complimentary space. You can expand the cache space by purchasing local disk. The above methods can expand the space for temporary files and avoid the above error. For details on purchasing and operation, please refer to [Use virtual warehouse local disk](https://docs.byteplus.com/docs/bytehouse/intelligent-cache).

* If you have already purchased local disk, you may expand local disk as appropriate. Log in to the ByteHouse CDW console, click **Virtual warehouse** at the top of the page, locate the virtual warehouse you are using, click **Edit**, and adjust the size of the local disk.
