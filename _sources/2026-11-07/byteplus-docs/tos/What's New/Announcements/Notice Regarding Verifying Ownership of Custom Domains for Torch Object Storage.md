---
title: "Notice Regarding Verifying Ownership of Custom Domains for Torch Object Storage"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Notice_Regarding_Verifying_Ownership_of_Custom_Domains_for_Torch_Object_Storage"
---

To ensure business security and stability, BytePlus Torch Object Storage (TOS) will verify ownership of custom domains starting **June 24, 2026**. The system will verify your ownership when you set up a custom domain.

<span id="Y557UlTL"></span>
## Estimated Change Time

**2026\-06\-24**. Please refer to the console for the specific time.

<span id="QYoKjWs7"></span>
## Change Description

Starting **June 24, 2026**, TOS will verify domain ownership information when you set up custom domains.


* **Console**: This change will be implemented simultaneously in the console. Follow the instructions on the page to verify ownership, and then you can continue associating your domain without interruption.

* **SDK**: If you set up a custom domain via an SDK without completing the necessary upgrades and adaptations, the request will return an error. The following is an example error:

   ```Plain Text
   Action: PutBucketCustomDomain
   Service: tos
   RequestID: 3835072a7cc6b3f16a2a7cc6-b611ba5-1wXbVu-PBCD-ccs-front-dualstack
   EC: 0016-00000014
   Code: NeedVerifyDomainOwnership
   Message: The bucket custom domain ownership needs to be verified.
   ```
   


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Ownership verification records typically expire. If you do not complete the verification process before the record expires, you must regenerate the record and verify it again. Refer to the information displayed in the console.</div>


<span id="g2KdLSqf"></span>
## Impacts


* If you primarily use the TOS console to set up custom domains, the impact is minimal. Just follow the instructions on the page to complete the verification process.

* If you set up custom domains via an **SDK or API**, you must promptly update and adapt the SDK to support the verification process.

* Failure to complete the SDK upgrade and adaptation may result in the `NeedVerifyDomainOwnership` error.


<span id="37XBXw00"></span>
## Pre\-change Checklist

Before the change goes live, we recommend completing the following checks:


* Review your business scenarios to identify any that involve custom domains set up through an SDK or API.

* Check the version of the SDK and calling logic you use, and confirm they support domain ownership verification.

* Obtain DNS permissions in advance so that you can configure and verify TXT records in time when setting up a custom domain.

* If your business is sensitive to the domain association process, we recommend verifying it in a test environment beforehand.


For more information about custom domain configuration and ownership verification, see [Setting up a custom domain](https://docs.byteplus.com/en/docs/tos/Set-up-a-custom-domain-name?lang=en).
