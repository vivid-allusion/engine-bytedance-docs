---
title: "Access log overview"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-Access-log-overview"
---

## Overview

CLB supports delivering access log data of **TLS listeners** to [TLS](https://docs.byteplus.com/en/docs/tls/What_is_TLS), facilitating user access behavior analysis or troubleshooting.

## Basic information

### Capabilities

|Concept |Notes |
|---|---|
|Index |After enabling the **access log delivery for TLS**, key\-value indexes are configured for the log topic by default based on the **log fields** described below.<br><br>> **tip**<br><br><br>> The default key\-value index configuration will overwrite the existing index configuration of the log topic. Please operate with caution. To modify indexes, see [Viewing and modifying the indexes](https://docs.byteplus.com/en/docs/clb/NLB-Managing-an-access-log?TagIDs=#OfPZW9vQ).<br> |
|Search query |A search and analysis statement consists of a search statement and an SQL analysis statement, separated by a pipe symbol (\|). This syntax indicates that data statistics and analysis are performed on the results that match the search conditions. For more information, see [Analysis overview](https://docs.byteplus.com/en/docs/6470/75295). |
|Log project |A log project is a project management unit for data, used for tenant resource isolation and control. Typically, one log project corresponds to one application, business, or product. |
|Log Topic |A log topic is a unit for data collection and storage. A log project can contain multiple log topics. Each log topic belongs to one log project. Different data sources and collection rules can be configured for the same log topic. |

### Log fields

|**Field** |Type |Notes |**Example** |
|---|---|---|---|
|log_version |text |The version of the log. The current version is 1.0. |1.0 |
|nlb_id |text |The ID of the NLB instance. |nlb\-bp1o94dp5i6ea\*\*\*\* |
|listener_id |text |ID of the TLS listener. |lsn\-2fek3rgsxhrsw5oxruwec\*\*\*\* |
|listener_protocol |text |The protocol of the listener, with supported value tls. |tls |
|client_address |text |Client IP address and port. Both IPv4 and IPv6 addresses are recorded in this field. When the client connects using a PrivateLink endpoint, the real client IP address and port are also recorded. |192.168.1.66:80 |
|nlb_address |text |* When a client directly accesses an NLB instance, this field records the NLB VPC IP address and port.<br><br>* When a client accesses an NLB instance through PrivateLink, this field records the endpoint IP address and port.<br><br><br>> **tip**<br><br><br>> Both IPv4 and IPv6 addresses are recorded in this field.<br> |172.16.1.88:80 |
|server_address |text |Backend server IP address and port. Both IPv4 and IPv6 addresses are recorded in this field. |172.16.2.22:80 |
|tls_conn_created_time |text |The time when the TLS connection starts, recorded in ISO 8601 standard format local time, UTC+8. |2025\-08\-18T15:30:45+08:00 |
|time |text |The time when the TLS connection ends, recorded in ISO 8601 standard format local time, UTC+8. |2025\-08\-18T15:40:45+08:00 |
|conn_time |double |The total time from connection establishment to closure with the client, in seconds. |1 |
|tls_handshake_time |double |The time taken to complete the TLS handshake after establishing a TCP connection with the client, measured in seconds.<br><br>If the TLS handshake is not performed or fails, the value of this field is set to `-`. |1 |
|received_bytes |long |Number of bytes received by the NLB from the client (after decryption). |19 |
|sent_bytes |long |Number of bytes sent by the NLB to the client (before encryption). |1069 |
|certificate_id |text |The certificate ID used during TLS connection establishment. |cert\-3tjuxoukkq3vj0ww\*\*\*\* |
|ssl_cipher |text |Cipher suite used when the TLS connection is established. |ECDHE\-ECDSA\-AES256\-GCM\-SHA384 |
|ssl_protocol |text |The protocol used during TLS connection establishment, e.g., tls_v1.2. |tls_v1.2 |
|sni_domain_name |text |The SNI domain name provided by the client during TLS handshake.<br><br>If a valid ClientHello message is not sent or this extension information is not included, the value of this field will be `-`. |www.example.com |

## Billing description

Regarding the billing of access logs, the NLB side currently does not charge, while TLS charges for it. For details, see [TLS billing](https://docs.byteplus.com/en/docs/tls/billable_items).

## Usage process

1. [Enable access log](https://docs.byteplus.com/en/docs/clb/NLB-Managing-an-access-log#G6vslG2m)

2. [Analyze access logs](https://docs.byteplus.com/en/docs/clb/NLB-Managing-an-access-log#HlHbBCAP)
