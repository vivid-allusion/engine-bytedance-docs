---
title: "WHOIS lookup"
product: "BytePlus Domain Names"
product_code: "domain-names"
source: "https://docs.byteplus.com/en/docs/domain-names/whois_en"
---

<span id="overview"></span>
## Overview

On the Internet, information about each domain is stored in the registry's domain information database. This information includes domain registration details, status codes, and more. WHOIS is a protocol for querying domain information databases. WHOIS lookup is a tool that uses this protocol, allowing you to obtain information about a specific domain, which is known as WHOIS information.

BytePlus Domains integrates WHOIS lookup functionality. The WHOIS lookup results display the following information:


* Domain registrar

* Registration date

* Expiration date

* Domain status codes

* DNS servers (Nameservers)


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In compliance with ICANN's "Temporary Specification for gTLD Registration Data" and the "European Union General Data Protection Regulation (GDPR)", since May 25, 2018, when querying WHOIS information in BytePlus Domains, the results no longer display the following information:</div>



* <div data-tips="true" data-tips-type="tip">Names of domain registrant/registration organization</div>


* <div data-tips="true" data-tips-type="tip">Contact information of domain registrant/registration organization, administrative contacts, and technical contacts, including phone numbers and email addresses.</div>



In BytePlus Domains, you can obtain WHOIS information through the following methods:


* In the domain list on the domain registration page, you can click **WHOIS Information** to obtain WHOIS information for a specific domain.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_166ec3dd64a8539a62553ea93b3e02b9.png) </span>

* In the **WHOIS Lookup** card at the top right of the WHOIS lookup results page, you can enter the domain you want to query to obtain its WHOIS information.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_3bc61189465aed861fad0d62a3607aa9.png) </span>


<span id="meanings-of-status-codes-in-whois-information"></span>
## Meanings of Status Codes in WHOIS Information

WHOIS information includes domain status codes. Based on these status codes, you can understand the domain's availability and potential issues.

**Possible Status for Newly Registered Domains**


|**Status** |**Description** |
|---|---|
|active (OK) |Indicates that the domain is in normal status, has no locks, and is within its validity period. Domains in this status can be accessed normally. |
|addPeriod |Indicates a period after successful domain registration, typically 5 days. |


**Possible Status When Domain is Locked**


|**Status** |**Description** |
|---|---|
|serverDeleteProhibited |Indicates that the registry prohibits domain deletion. This is usually due to security or administrative policies by the registry to prevent domain deletion, even if requested by the domain owner, to avoid accidental deletion. |
|serverUpdateProhibited |Indicates that the registry prohibits updating domain information. Domain owners cannot modify DNS servers, contact information, etc., for domains in this status. Common reasons include registry system maintenance or domain disputes. |
|serverTransferProhibited |Indicates that the registry prohibits domain transfer to other registrars. Common reasons include:<br><br><br>* The domain was recently registered. Domains cannot be transferred to other registrars within 60 days of registration.<br><br>* The domain was recently transferred to a new registrar. Before the transfer, you enabled the transfer lock, preventing the domain from being transferred out for 60 days after the transfer.<br><br>* The domain is involved in legal disputes. |
|clientDeleteProhibited |Indicates that the registrar prohibits domain deletion. This may be due to restrictions in the agreement between the domain owner and registrar, or the domain is part of specific service packages that don't allow deletion during certain periods. |
|clientUpdateProhibited |Indicates that the registrar prohibits updating domain information. Common reasons include the registrar enabling an update lock for the domain. |
|clientTransferProhibited |Indicates that the registrar prohibits domain transfer to other registrars. A common reason is that the registrar has enabled a transfer lock for the domain. |


**Other Status**


|**Status** |**Description** |
|---|---|
|pendingTransfer |Indicates that the domain is in the process of being transferred. This status appears when the domain owner initiates a transfer request to another registrar. During this period, both the original and target registrars need to complete a series of confirmation and handover tasks. |
|pendingDelete |Indicates that the domain is in the redemption period, and you must pay a premium fee to recover the domain through the registrar. See [Domain lifecycle](https://docs.byteplus.com/en/docs/domain-names/domain-renewal_en#domain-lifecycle). |
|clientHold |Indicates that the registrar has suspended domain resolution. Possible reasons include violations of the registrar's terms of service, such as domain involvement in illegal content or use in malicious attacks. The registrar sets this status to prevent negative impacts. Domains in this status are inaccessible. |
|serverHold |Indicates that the registry has suspended domain resolution. This may be due to legal disputes. Domains in this status are inaccessible. |
|inactive |Indicates that the domain is suspended. Possible reasons include expired domain without renewal, violation of registrar rules, or incorrect DNS server settings. Domains in this status are inaccessible. |
|clientRenewProhibited |Indicates that the registrar prohibits domain renewal. This may be due to ongoing dispute resolution processes, where the registrar temporarily prohibits renewal to ensure fairness. |
|serverRenewProhibited |Indicates that the registry prohibits domain renewal. This may be due to registrar system failures, contractual disputes with the domain owner, or registry concerns about domain legality or compliance. |
|redemptionPeriod |Indicates that the domain is in the redemption period. See [Domain lifecycle](https://docs.byteplus.com/en/docs/domain-names/domain-renewal_en#domain-lifecycle). |
