---
title: "Delete a GTM Instance"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/umyKsn"
---

This document describes how to delete a GTM instance in BytePlus GTM.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you want BytePlus GTM to stop billing for a specified GTM instance, you need to delete that GTM instance.</div>


* <div data-tips="true" data-tips-type="tip">After deleting the specified GTM instance, the DNS resolution is also deleted.</div>



<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">Please consider carefully before deleting a GTM instance. Deleted GTM instances cannot be recovered and can only be recreated. If you just want to disable all rules of the GTM instance, you can <a href="https://docs.byteplus.com/docs/byteplus-dns-suite/U5nvpy">stop the GTM instance</a>.</div>


<span id="prerequisites"></span>
## Prerequisites

Before deleting a GTM instance, you must ensure that you have stopped the instance. See [Start or Stop a GTM Instance](https://docs.byteplus.com/docs/byteplus-dns-suite/U5nvpy).

<span id="steps"></span>
## Steps

Follow the steps below to delete a GTM instance.


1. On the [Instance management page](https://console.byteplus.com/dns-suite/gtm/instances), find the GTM instance you need to delete.

2. Select the GTM instance you want to delete. Click **Delete**.

3. In the pop\-up dialog box, click **OK** to delete the GTM instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the <strong>Connection method</strong> is <strong>Domain From BytePlus DNS</strong> when you create the GTM instance, the dialog box prompts you whether to delete the associated DNS records in BytePlus DNS.</div>



* <div data-tips="true" data-tips-type="tip"><strong>Yes</strong>: Delete the associated DNS records in BytePlus DNS while deleting the GTM instance.</div>


* <div data-tips="true" data-tips-type="tip"><strong>No</strong>: Do not delete the associated DNS records in BytePlus DNS while deleting the GTM instance.</div>
