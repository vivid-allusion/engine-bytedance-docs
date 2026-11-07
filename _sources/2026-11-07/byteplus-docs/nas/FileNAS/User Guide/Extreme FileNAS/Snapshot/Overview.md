---
title: "Overview"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Overview"
---

FileNAS Extreme supports creating snapshots. Each snapshot is a backup of the file system's data at that moment. When data is lost or there is a failure, you can roll back the corresponding data using the snapshot.

<span id="d9fdf37f"></span>
## Use cases

You can use the snapshot feature of the file system in the following scenarios:


* To prevent data errors or loss caused by human error, hacker attacks, virus infections, and other reasons.

* To improve fault tolerance by creating snapshots before important maintenance operations such as changing the operating system, upgrading application software, or migrating business data.


<span id="8f662fd1"></span>
## Snapshot principle

To save storage space, snapshots are taken in the form of incremental snapshots. When you create a snapshot, apart from the first snapshot which is a full snapshot, subsequent snapshots are incremental snapshots, which only contain the data changes compared to the previous snapshot.

<span id="前提条件"></span>
## Prerequisite

Already created extreme file system , and the file system status is running. For specific steps, please refer to [Creating a file system](https://docs.byteplus.com/docs/nas/Creating-a-file-system).

<span id="注意事项"></span>
## Precautions


* The current snapshot is in the public testing phase and is not charged for now. The charging time and standards will be notified separately. Please pay attention to SMS and product announcements in a timely manner.

* During the public testing period, a maximum of 5 manual snapshots can be created for the extreme file system.


<span id="相关操作"></span>
## Related operations


* [Creating a snapshot](https://docs.byteplus.com/docs/nas/Creating-a-snapshot)

* [Viewing snapshots](https://docs.byteplus.com/docs/nas/Viewing-snapshots)

* [Deleting a snapshot](https://docs.byteplus.com/docs/nas/Deleting-a-snapshot)

* [Creating a new file system using a snapshot](https://docs.byteplus.com/docs/nas/Creating-a-new-file-system-using-a-snapshot)

* [Modifying snapshot properties](https://docs.byteplus.com/docs/nas/Modifying-snapshot-properties)
