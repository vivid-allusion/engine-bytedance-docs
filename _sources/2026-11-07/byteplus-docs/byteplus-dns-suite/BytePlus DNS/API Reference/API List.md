---
title: "API List"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-api-overview"
---

You can use the OpenAPI described in this document to perform operations on BytePlus DNS.

<span id="f89dcdd1"></span>
## Domain management


|**API** |**Description** |
|---|---|
|[CreateZone](https://docs.byteplus.com/byteplus-dns-suite/reference/createzone) |Creates a domain. |
|[DeleteZone](https://docs.byteplus.com/byteplus-dns-suite/reference/deletezone) |Deletes a domain. |
|[UpdateZone](https://docs.byteplus.com/byteplus-dns-suite/reference/updatezone) |Updates comments for a domain. |
|[QueryZone](https://docs.byteplus.com/byteplus-dns-suite/reference/queryzone) |Gets detailed information about a domain. |
|[CheckZone](https://docs.byteplus.com/byteplus-dns-suite/reference/checkzone) |Checks whether a domain can be created. |
|[ListZones](https://docs.byteplus.com/byteplus-dns-suite/reference/listzones) |Gets a list of domains. |
|[RetrieveZone](https://docs.byteplus.com/byteplus-dns-suite/reference/retrievezone) |Generates verification information to verify the ownership of a domain. |
|[CheckRetrieveZone](https://docs.byteplus.com/byteplus-dns-suite/reference/checkretrievezone) |Verifies the ownership of your domain. |


<span id="5178ae16"></span>
## Record management


|**API** |**Description** |
|---|---|
|[CreateRecord](https://docs.byteplus.com/byteplus-dns-suite/reference/createrecord) |Creates a DNS record for the specified domain. |
|[DeleteRecord](https://docs.byteplus.com/byteplus-dns-suite/reference/deleterecord) |Deletes a DNS record from the specified domain. |
|[UpdateRecord](https://docs.byteplus.com/byteplus-dns-suite/reference/updaterecord) |Updates the specified DNS record. |
|[UpdateRecordStatus](https://docs.byteplus.com/byteplus-dns-suite/reference/updaterecordstatus) |Enables or disables the specified DNS record. |
|[QueryRecord](https://docs.byteplus.com/byteplus-dns-suite/reference/queryrecord) |Gets detailed information of a specific DNS record. |
|[ListRecords](https://docs.byteplus.com/byteplus-dns-suite/reference/listrecords) |Gets a list of DNS records for a specific domain. |


<span id="40f11d63"></span>
## Record set management


|**API** |**Description** |
|---|---|
|[ListRecordSets](https://docs.byteplus.com/byteplus-dns-suite/reference/listrecordsets) |Gets a list of DNS record sets for a specified domain. |
|[UpdateRecordSet](https://docs.byteplus.com/byteplus-dns-suite/reference/updaterecordset) |Enables or disables load balancing for the specified record set. |


<span id="c1033d39"></span>
## Line management


|**API** |**Description** |
|---|---|
|[ListLines](https://docs.byteplus.com/byteplus-dns-suite/reference/listlines) |Gets the list of ISP lines and geolocation lines provided by BytePlus DNS. |


<span id="c2661764"></span>
## DNS query metrics


|**API** |**Description** |
|---|---|
|[ListZoneStatistics](https://docs.byteplus.com/byteplus-dns-suite/reference/listzonestatistics) |Statistics the number of DNS queries for each specified root domain. |
|[ListDomainStatistics](https://docs.byteplus.com/byteplus-dns-suite/reference/listdomainstatistics) |Retrieves the statistics of DNS query counts for specified subdomains within a root domain. |


<span id="5168117c"></span>
## IP\-based lines


|**API** |**Description** |
|---|---|
|[ListCustomLines](https://docs.byteplus.com/byteplus-dns-suite/reference/listcustomlines) |Gets the list of IP\-based lines for BytePlus DNS. |
|[CreateCustomLine](https://docs.byteplus.com/byteplus-dns-suite/reference/createcustomline) |Creates an IP\-based line. |
|[UpdateCustomLine](https://docs.byteplus.com/byteplus-dns-suite/reference/updatecustomline) |Updates the specified IP\-based line. |
|[BatchDeleteCustomLine](https://docs.byteplus.com/byteplus-dns-suite/reference/batchdeletecustomline) |Batch deletes the specified IP\-based lines. |
|[ListRecordDigestByLine](https://docs.byteplus.com/byteplus-dns-suite/reference/listrecorddigestbyline) |Gets a list of DNS records using the specified IP\-based line. |


<span id="b5f48278"></span>
## DNS backup


|**API** |**Description** |
|---|---|
|[UpdateBackupSchedule](https://docs.byteplus.com/byteplus-dns-suite/reference/updatebackupschedule) |Updates the automatic backup schedule for the specified domain's DNS records. |
|[QueryBackupSchedule](https://docs.byteplus.com/byteplus-dns-suite/reference/querybackupschedule) |Gets the automatic backup schedule for the specified domain's DNS records. |
|[ListUserZoneBackups](https://docs.byteplus.com/byteplus-dns-suite/reference/listuserzonebackups) |Gets the backup list of DNS records for the specified domain. |
|[CreateUserZoneBackup](https://docs.byteplus.com/byteplus-dns-suite/reference/createuserzonebackup) |Manually creates a backup of DNS records for the specified domain. |
|[DeleteUserZoneBackup](https://docs.byteplus.com/byteplus-dns-suite/reference/deleteuserzonebackup) |Deletes the specified backup. |
|[RestoreUserZoneBackup](https://docs.byteplus.com/byteplus-dns-suite/reference/restoreuserzonebackup) |Rolls back the DNS records in the specified domain to the specified backup. |
