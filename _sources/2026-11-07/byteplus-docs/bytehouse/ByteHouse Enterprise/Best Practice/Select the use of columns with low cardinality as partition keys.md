---
title: "Select the use of columns with low cardinality as partition keys"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/select-columns-with-low-cardinality-as-partition-keys"
---

This article discusses why it is suggested to select a column with low cardinality as the partition key when inserting data into tables in ByteHouse Enterprise edition.

in ByteHouse Enterprise edition, when you send an insert statement to a table without a partition key (inserting many rows), all the row data for that table will be written to a new Part (i.e., data fragment) in storage.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b258fd0a46fb4753a1be08b761daa8b1~tplv-goo7wpa0wc-image.image) </span>

However, when you send an insert statement to a table with a partition key in ByteHouse Enterprise edition, ByteHouse will perform the following actions:


1. Check the partition key values of the rows contained in the insert table.

2. Create new Parts (i.e., data fragments) in storage for each different partition key value.

3. Place the rows into the corresponding partitions according to their partition key values.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a0ccd3d086d40a6b48478a8a7266455~tplv-goo7wpa0wc-image.image) </span>

Therefore, to minimize the quantity of write requests sent to ByteHouse Enterprise edition's object storage, use a partition key with low cardinality or avoid using any partition keys in the table.
