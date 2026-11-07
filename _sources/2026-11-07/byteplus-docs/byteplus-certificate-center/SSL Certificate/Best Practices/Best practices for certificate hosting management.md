---
title: "Best practices for certificate hosting management"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/Best-practices-for-certificate-hosting-management"
---

<span id="tj2o0FP2"></span>
## Overview

The certificate hosting service in by BytePlus Certificate Center automates certificate renewal and deployment, eliminating the operational burden of manual rotation. This document introduces the full lifecycle management of a hosting task—from enabling and canceling to deleting—centered around five OpenAPI operations. It also includes recommendations for handling runtime alerts and answers to frequently asked questions (FAQs).

<span id="cenhkFiK"></span>
## Related APIs

This document covers the following certificate hosting APIs:


|**API** |**Description** |
|---|---|
|[CreateDelegatedCnameRecords](https://docs.byteplus.com/en/docs/byteplus-certificate-center/createdelegatedcnamerecords) |Generates delegated CNAME records. Call this API to generate the required DNS CNAME delegated records for a specified certificate. It returns the host (Host) and record value (Value), which are used to configure CNAME records at your DNS provider to complete the delegation of domain ownership validation. |
|[CheckDelegatedCnameRecords](https://docs.byteplus.com/en/docs/byteplus-certificate-center/checkdelegatedcnamerecords) |Checks the delegated CNAME record configuration. Call this API to verify whether the delegated CNAME records of a specified certificate have been correctly configured and have taken effect in the DNS resolution of the domain covered by the certificate. |
|[CreateManagedTask](https://docs.byteplus.com/en/docs/byteplus-certificate-center/createmanagedtask) |Creates a certificate hosting task. Call this API to create a hosting task for a specified certificate. Once enabled, the system will automatically renew the certificate before it expires and deploy the new certificate to the specified BytePlus cloud services. |
|[TerminateManagedTask](https://docs.byteplus.com/en/docs/byteplus-certificate-center/terminatemanagedtask) |Cancels a hosting task. Call this API to cancel a hosting task that is in the Enabled state. After cancellation, the system stops automatic renewal and certificate replacement. This operation is irreversible. |
|[DeleteManagedTask](https://docs.byteplus.com/en/docs/byteplus-certificate-center/deletemanagedtask) |Deletes a hosting task. Call this API to delete a hosting task that is in the Disabled state. Once deleted, all historical records of the task can no longer be viewed and cannot be recovered. |


<span id="ABkZFfBG"></span>
## **Hosting task lifecycle**

&nbsp;

```Plain Text
──────────────────────────── Enable Stage ─────────────────────────────
  ① Generate delegated CNAME records (CreateDelegatedCnameRecords)
                ↓
  ② Configure CNAME at your DNS provider (User operation, wait 3-5 mins)
                ↓
  ③ Verify CNAME configuration (CheckDelegatedCnameRecords)
        ├─ Failed → Troubleshoot and retry ③
        └─ Passed ↓
  ④ Create hosting task (CreateManagedTask) → Task status: Enabled

──────────────────────────── Running Stage ────────────────────────────

        ┌──────────────────────────────────────────────────┐
        │  Auto-renewal 30 days before expiration          │
        │       ↓                                          │
        │  Renewal successful → Auto-deploy to CDN         │
        │       ↓                                          │
        │  Wait for the next renewal cycle ──────┐         │
        │       ↑                                │         │
        │       └────────────────────────────────┘         │
        └──────────────────────────────────────────────────┘

  ★ Continuous monitoring: Task status / CNAME health / Certificate validity / CDN deployment

─────────────────────────── Offline Stage ─────────────────────────────

  ⑤ Cancel hosting task (TerminateManagedTask) → Enabled → Disabled (Irreversible)
                ↓
  ⑥ Delete hosting task (DeleteManagedTask) → Clear task records (Unrecoverable)
```


<span id="53vb1U6Y"></span>
## Prerequisites

Before managing your hosting tasks, ensure that:


* [A free certificate has been issued](https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-request-free-ssl-certificate). You have successfully applied for a free certificate (DigiCert EE or Let's Encrypt) via BytePlus Certificate Center.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Currently, Let's Encrypt free certificates require allowlist approval. To enable access, contact <a href="https://console.byteplus.com/workorder/create">technical support</a>.   </div>
   

* The certificate is in the **Issued** state, and the certificate has **at least 30 days** remaining before expiration.

* [BytePlus CDN](https://console.byteplus.com/cdn/cdn-bp/welcome) ** ** is activated. The automatic deployment target for hosting tasks currently supports only BytePlus CDN. Ensure that the CDN service is activated and the domain has been added to CDN.


<span id="3Gvqqpmp"></span>
## Enabling the hosting service

<span id="MqT7nRNR"></span>
### Step 1: Generate Delegated CNAME Records

Call the [CreateDelegatedCnameRecords](https://docs.byteplus.com/en/docs/byteplus-certificate-center/createdelegatedcnamerecords) API to generate delegated CNAME records for the domains associated with the certificate.

**Request example:** 

```JSON
POST /?Action=CreateDelegatedCnameRecords&Version=2021-06-01 HTTP/1.1
Host: open.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20260423T095237Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260423/cn-beijing/certificate_service/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  // Certificate instance ID
  "instance_id": "cert-9e3dee3cd50a42f9852f0928507b****"
}
```


**Response example:** 

```JSON
{
  "ResponseMetadata": {
    "RequestId": "2026042309523701020010023045A1B2C3",
    "Action": "CreateDelegatedCnameRecords",
    "Version": "2021-06-01",
    "Service": "certificate_service",
    "Region": "ap-singapore-1"
  },
  "Result": {
    "cnameRecords": [
      {
        // The CNAME record name to create in DNS (Domain name)
        "host": "_acme-challenge.auto.example.com",
        // The CNAME target value (Record value)
        "value": "auto.example.com.dcv.cert.byteplus.com"
      }
    ]
  }
}
```


<span id="jIpkLPVt"></span>
### Step 2: Configure the DNS CNAME record

Add the CNAME record at your domain's DNS provider:


|Field |Value |
|---|---|
|Host |The `host` value returned in [Step 1](https://docs.byteplus.com/en/docs/byteplus-certificate-center/Best-practices-for-certificate-hosting-management?lang=en#MqT7nRNR), e.g., `_acme-challenge.auto.example.com` |
|Record Type |CNAME |
|Value |The `value` returned in [Step 1](https://docs.byteplus.com/en/docs/byteplus-certificate-center/Best-practices-for-certificate-hosting-management?lang=en#MqT7nRNR), e.g., `auto.example.com.dcv.cert.byteplus.com` |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">After configuration, wait <strong>3–5 minutes</strong> before proceeding to verification to allow for DNS propagation.</div>


* <div data-tips="true" data-tips-type="default">This CNAME record <strong>must not be modified or deleted</strong> throughout the entire hosting period; otherwise, subsequent renewals will fail. It is recommended to apply a protection label or change\-approval policy to this record in your DNS console to prevent accidental modification.</div>



<span id="eBPIhxr2"></span>
### Step 3: Verify the CNAME configuration

Call the [CheckDelegatedCnameRecords](https://docs.byteplus.com/en/docs/byteplus-certificate-center/checkdelegatedcnamerecords) API to verify that the DNS CNAME record has been correctly configured and has propagated.

**Request example:** 

```JSON
POST /?Action=CheckDelegatedCnameRecords&Version=2021-06-01 HTTP/1.1
Host: open.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20260423T095837Z
X-Content-Sha256: 3a1f874e******e753b44d21f
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260423/cn-beijing/certificate_service/request, SignedHeaders=host;x-content-sha256;x-date, Signature=58b8e045ff8c48d14049******de8c9389b51b2068d512f93357b1f52196f

{
  // Use the same certificate instance ID as in Step 1
  "instance_id": "cert-9e3dee3cd50a42f9852f0928507b****"
}
```


**Response example (verification passed):** 

```JSON
{
  "ResponseMetadata": {
    "RequestId": "2026042309583701020010023045A1B2C3",
    "Action": "CheckDelegatedCnameRecords",
    "Version": "2021-06-01",
    "Service": "certificate_service",
    "Region": "ap-singapore-1"
  },
  "Result": {
    // true = All domains passed verification; false = At least one domain failed
    "check_result": true,
    // List of domains that failed verification; empty when all passed
    "failed_domains": []
  }
}
```


**Response example (partial domain verification failure):** 

```JSON
{
  "ResponseMetadata": { "..." : "..." },
  "Result": {
    "check_result": false,
    "failed_domains": ["auto.example.com"]
  }
}
```


**Troubleshooting verification failures:** 


* Confirm that the CNAME record has been correctly added.

* Wait a few minutes and retry (DNS propagation may take time).

* Verify that the record `value` exactly matches the value returned by `CreateDelegatedCnameRecords`.


<span id="hihOQhUv"></span>
### Step 4: Create a h**osting task**

Once all CNAMEs are verified, call [CreateManagedTask](https://docs.byteplus.com/en/docs/byteplus-certificate-center/createmanagedtask) to create the hosting task.

**Request example:** 

```JSON
POST /?Action=CreateManagedTask&Version=2024-01-01 HTTP/1.1
Host: open.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20260423T100237Z
X-Content-Sha256: 4b2g985f******f864c55e32g
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260423/cn-beijing/certificate_service/request, SignedHeaders=host;x-content-sha256;x-date, Signature=69c9f156gg9d59e25150******ef9da490c62c3179e623g04468c2g63207g

{
  // Certificate instance ID
  "instance_id": "cert-9e3dee3cd50a42f9852f0928507b****",
  // Target cloud services for automatic certificate replacement; currently only CDN is supported
  "binding_services": ["CDN"],
  // Number of days before expiration to trigger renewal; default is 30
  "renew_period": 30,
  // Task tag; recommended format: {environment}-{service}-{domain-summary} for easy identification
  "tag": "prod-cdn-auto-renew"
}
```


**Response example:** 

```JSON
{
  "ResponseMetadata": {
    "RequestId": "2026042310023701020010023045A1B2C3",
    "Action": "CreateManagedTask",
    "Version": "2024-01-01",
    "Service": "certificate_service",
    "Region": "ap-singapore-1"
  },
  "Result": {
    // Hosting task ID
    "task_id": "task-807aecfba9c7414bb68784cf4126****"
  }
}
```


Once successfully created, the hosting task enters the **Enabled** state. The system will automatically renew the certificate 30 days before expiration and deploy it to CDN.

<span id="5laDoiNz"></span>
## **Hosting** task notifications and emergency handling

After a hosting task is enabled, the system automatically handles certificate renewal and deployment. When issues such as renewal failures, deployment exceptions, or task termination occur, the system sends alert notifications via email and in\-app messages.

Upon receiving a notification about hosting failure or hosting termination, the system will no longer automatically renew or deploy the certificate. You must manually complete certificate renewal and update to prevent service interruption.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Certificate hosting is an automated assistance service, but it does not replace your responsibility for managing service continuity and availability. Be sure to:</div>



* <div data-tips="true" data-tips-type="default">Promptly monitor and respond to alert notifications sent by the system to avoid certificate expiration due to oversight.</div>


* <div data-tips="true" data-tips-type="default">Regularly check the running status of hosting tasks to ensure they remain in the <strong>Enabled</strong> state.</div>



<span id="Hxz7GPiu"></span>
### Notification Channels


* **Email:**  Sent to the email address associated with your account. Ensure the email address is valid and regularly monitored to prevent alert emails from being missed or filtered into spam.

* **Internal message:**  Available in the [Message center](https://console.byteplus.com/message/innermsg) of the BytePlus console. It is recommended to log in to the console regularly to check for unread messages.


<span id="IEewu283"></span>
### Exception scenarios and recommended actions


|**Exception Scenario** |**Possible Causes** |**Recommended Actions** |
|---|---|---|
|Certificate renewal failure |Delegated CNAME invalidated, DNS configuration changed, CA verification failed, etc. |Check whether the delegated CNAME and DNS configuration are intact. If necessary, manually apply for a new certificate and [recreate the hosting task](https://docs.byteplus.com/en/docs/byteplus-certificate-center/Best-practices-for-certificate-hosting-management?lang=en#3Gvqqpmp). |
|Certificate deployment failure |CDN domain configuration changed, CDN service unavailable, etc. |Check CDN domain and service status. Contact [technical support](https://console.byteplus.com/workorder/create) for troubleshooting. |
|Hosting task status changed |Task was canceled by the system or manually. |Confirm whether this was an expected operation. If not, investigate the cause and [recreate the hosting task](https://docs.byteplus.com/en/docs/byteplus-certificate-center/Best-practices-for-certificate-hosting-management?lang=en#3Gvqqpmp). |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Upon receiving related alerts, please address them as soon as possible before the certificate expires. Failure to respond in time may lead to certificate expiration, impacting the HTTPS availability of your live services.</div>


<span id="3q0c7EUo"></span>
## Canceling a hosting Task

When automated renewal and deployment are no longer needed, call [TerminateManagedTask](https://docs.byteplus.com/en/docs/byteplus-certificate-center/terminatemanagedtask) to cancel the hosting task.

**Request example:** 

```JSON
POST /?Action=TerminateManagedTask&Version=2021-06-01 HTTP/1.1
Host: open.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20260423T103037Z
X-Content-Sha256: 5c3h096g******g975d66f43h
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260423/cn-beijing/certificate_service/request, SignedHeaders=host;x-content-sha256;x-date, Signature=70d0g267hh0e60f36261******fg0eb501d73d4280f734h15579d3h74318h

{
  // Hosting task ID to terminate
  "task_id": "task-807aecfba9c7414bb68784cf4126****"
}
```


**Response example:** 

```JSON
{
  "ResponseMetadata": {
    "RequestId": "2026042310303701020010023045A1B2C3",
    "Action": "TerminateManagedTask",
    "Version": "2021-06-01",
    "Service": "certificate_service",
    "Region": "ap-singapore-1"
  },
  // Canceled successfully, no business data returned
  "Result": {}
}
```


**Impact of termination:** 


* The task state changes to **Disabled**, and the system stops automatic renewal and deployment for this certificate.

* The old certificate already deployed on the CDN will not be uninstalled and remains valid until its original expiration date.

* Irreversible Operation: Cancellation cannot be undone. To resume hosting the same certificate, you must repeat the [enabling process](https://docs.byteplus.com/en/docs/byteplus-certificate-center/Best-practices-for-certificate-hosting-management?lang=en#3Gvqqpmp).

* Task records are retained for auditing purposes.


<span id="LgtrNDzJ"></span>
## Deleting a hosting Task

To clear the records of a canceled task, call [DeleteManagedTask](https://docs.byteplus.com/en/docs/byteplus-certificate-center/deletemanagedtask).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can only delete tasks that are in the <strong>Disabled</strong> state. If a task is still running (<strong>Enabled</strong>), you must call <a href="https://docs.byteplus.com/en/docs/byteplus-certificate-center/terminatemanagedtask">TerminateManagedTask</a> to cancel it before proceeding with deletion.</div>


**Request example:** 

```JSON
POST /?Action=DeleteManagedTask&Version=2021-06-01 HTTP/1.1
Host: open.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20260423T104537Z
X-Content-Sha256: 6d4i107h******h086e77g54i
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260423/cn-beijing/certificate_service/request, SignedHeaders=host;x-content-sha256;x-date, Signature=81e1h378ii1f71g47372******gh1fc612e84e5391g845i26680e4i85429i

{
  // The hosting task ID in Disabled state
  "task_id": "task-807aecfba9c7414bb68784cf4126****",
  // Reason for deletion (optional); recommended for audit trails
  "delete_reason": "Service decommissioned; automatic renewal no longer required"
}
```


**Response example:** 

```JSON
{
  "ResponseMetadata": {
    "RequestId": "2026042310453701020010023045A1B2C3",
    "Action": "DeleteManagedTask",
    "Version": "2021-06-01",
    "Service": "certificate_service",
    "Region": "ap-singapore-1"
  },
  // Deletion successful; no business data returned
  "Result": {}
}
```


**Impact of deletion:** 


* The task record and all associated history (renewal records, replacement records) are permanently purged and cannot be recovered.

* The certificate instance itself is not affected and remains in BytePlus Certificate Center.


<span id="HRYr2KkX"></span>
## FAQ

<span id="GvInMXtc"></span>
### Q1: What should I do if CNAME verification fails?


1. Run dig _acme\-challenge.<your\-domain\> CNAME +short to confirm the resolved value.

2. Compare the returned value with the value output by CreateDelegatedCnameRecords to ensure an exact match.

3. Check whether a CAA record is configured for the domain. If so, ensure that digicert.com or letsencrypt.org is allowed.

4. Wait 3–5 minutes and retry (DNS propagation delay may be the cause).


<span id="EvVLq5lP"></span>
### Q2: Can I host multiple certificates simultaneously?

Yes. A single tenant can create multiple hosting tasks, with each task hosting one certificate instance.

<span id="D6qhyNTo"></span>
### Q3: **Can I re\-enable a hosting task after terminating it?** 

No. However, you can create a new hosting task for the same certificate by re\-executing the full activation workflow described in [Enabling the Hosting Service](https://mira.byteintl.net/chat/110109634579#enabling-the-hosting-service). If the original CNAME records have not been deleted, re\-creation will proceed more quickly.

<span id="Fas3NKTG"></span>
### Q4: What happens to the certificate after a hosting task is deleted?

The deletion only purges the hosting task record. The certificate itself is not affected. Certificates already deployed on CDN remain valid until they expire, but they will no longer be automatically renewed.

<span id="kGzbKldU"></span>
### Q5: What should I do if the CNAME record is accidentally deleted?


1. Immediately call CreateDelegatedCnameRecords again to retrieve the host/value (this API is idempotent; the values remain unchanged).

2. Reconfigure the CNAME record in your DNS provider.

3. Call CheckDelegatedCnameRecords to confirm recovery.


It is recommended to apply change protection to hosting\-related CNAME records on the DNS side to prevent accidental modifications at the source.

<span id="xudQ4Vp3"></span>
### Q6: Which services are supported as deployment targets for hosting tasks?

Currently, only **BytePlus CDN** is supported as the automatic deployment target. After a certificate is successfully renewed, the system automatically replaces the certificate on the associated CDN domains.
