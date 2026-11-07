---
title: "API overview"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/API-overview"
---

This article summarizes the API interfaces provided by PFS.

<span id="be78afb0"></span>
## Overviews


|API |Description |
|---|---|
|[DescribeFileSystemOverview](https://docs.byteplus.com/en/docs/pfs/DescribeFileSystemOverview) |Call the DescribeFileSystemOverview interface to list file system overview information. |
|[DescribeFileSystemStatistics](https://docs.byteplus.com/en/docs/92/DescribeFileSystemStatistics) |Call the DescribeFileSystemStatistics interface to list file system statistics. |


<span id="d8903241"></span>
## Regions


|API |Description |
|---|---|
|[DescribeRegions](https://docs.byteplus.com/en/docs/pfs/DescribeRegions) |Call the DescribeRegions interface to list regions. |
|[DescribeZones](https://docs.byteplus.com/en/docs/pfs/DescribeZones) |Call the DescribeZones interface to list available zones. |


<span id="da3ed196"></span>
## FileSystems


|API |Description |
|---|---|
|[DescribeFileSystems](https://docs.byteplus.com/en/docs/pfs/DescribeFileSystems) |Call the DescribeFileSystems interface to enumerate file systems. |
|[CreateFileSystem](https://docs.byteplus.com/en/docs/pfs/CreateFileSystem) |Call the CreateFileSystem interface to create a file system. |
|[DeleteFileSystem](https://docs.byteplus.com/en/docs/pfs/DeleteFileSystem) |Call the DeleteFileSystem interface to delete the file system. |
|[ExpandFileSystem](https://docs.byteplus.com/en/docs/pfs/ExpandFileSystem) |Call the ExpandFileSystem interface to expand the file system. |
|[UpdateFileSystem](https://docs.byteplus.com/en/docs/pfs/UpdateFileSystem) |Call the UpdateFileSystem interface to update file system information. |


<span id="4f8124f8"></span>
## MountServices


|API |Description |
|---|---|
|[DescribeMountServices](https://docs.byteplus.com/en/docs/pfs/DescribeMountServices) |Call the DescribeMountServices interface to list the mounting services. |
|[CreateMountService](https://docs.byteplus.com/en/docs/pfs/CreateMountService) |Call the CreateMountService interface to create a mounting service. |
|[DeleteMountService](https://docs.byteplus.com/en/docs/pfs/DeleteMountService) |Call the DeleteMountService interface to delete the mounting service. |
|[UpdateMountService](https://docs.byteplus.com/en/docs/pfs/UpdateMountService) |Call the UpdateMountService interface to update the mounting service information. |
|[DescribeMountServiceNodeTypes](https://docs.byteplus.com/en/docs/pfs/DescribeMountServiceNodeTypes) |Call the DescribeMountServiceNodeTypes interface to query the node information that can be created in a certain availability zone. |
|[AttachMountServiceToSelfFileSystem](https://docs.byteplus.com/en/docs/pfs/AttachMountServiceToSelfFileSystem) |Call the AttachMountServiceToSelfFileSystem interface to bind the PFS instance to the mounting service. |
|[DetachMountServiceFromSelfFileSystem](https://docs.byteplus.com/en/docs/pfs/DetachMountServiceFromSelfFileSystem) |Call the DetachMountServiceFromSelfFileSystem interface to unbind the PFS instance from the mounting service. |


<span id="ee4de330"></span>
## Fileset


|API |Description |
|---|---|
|[DescribeFilesets](https://docs.byteplus.com/en/docs/pfs/DescribeFilesets) |Call the DescribeFilesets interface to enumerate Filesets. |
|[CreateFileset](https://docs.byteplus.com/en/docs/pfs/CreateFileset) |Call the CreateFileset interface to create a Fileset. |
|[DeleteFileset](https://docs.byteplus.com/en/docs/pfs/DeleteFileset) |Call the DeleteFileset interface to delete the Fileset. |
|[UpdateFileset](https://docs.byteplus.com/en/docs/pfs/UpdateFileset) |Call the UpdateFileset interface to update Fileset information. |
|[SetFilesetQuota](https://docs.byteplus.com/en/docs/pfs/SetFilesetQuota) |Call the SetFilesetQuota interface to set the Quota information of Fileset. |
|[SetFilesetQos](https://docs.byteplus.com/en/docs/pfs/SetFilesetQos) |Call the SetFilesetQuota interface to set the Qos information of Fileset. |


<span id="89783940"></span>
## Tags


|API |Description |
|---|---|
|[TagResources](https://docs.byteplus.com/en/docs/pfs/TagResources) |Call the TagResources interface to bind tags to PFS related resources. |
|[ListTagsForResources](https://docs.byteplus.com/en/docs/pfs/ListTagsForResources) |Call the ListTagsForResources interface to filter PFS resources by tags. |
|[UntagResources](https://docs.byteplus.com/en/docs/pfs/UntagResources) |Call the UntagResources interface to unbind tags for PFS related resources. |
