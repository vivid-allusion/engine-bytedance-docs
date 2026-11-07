---
title: "Release notes"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/function_release_notes"
---

Release notes manage all release tickets for functions, facilitating your release tracking and auditing. This article introduces operations related to release notes.

<span id="view-release-notes"></span>
## View release notes

Support for viewing release records of functions and change details of each release ticket.


1. Log in to the [Function Service console](https://console.byteplus.com/vefaas).

2. On the top navigation bar, select the target region.

3. On the Function list page, search for the target function. Click the function name to enter the basic information tab of the current function.

4. Switch to the release management tab. Click **release notes** to view the list of release records for the current function.

5. Select the target release record, click **release ID**, and view the details of the changes in this release.


<span id="rollback"></span>
## Rollback

After the function release is completed, if the current function does not meet expectations, it supports rapid rollback to the previously successfully released version.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Rollback will initiate a new release work order, rolling back the online traffic to the historical version of the selected work order.</div>


<div data-tips="true" data-tips-type="warning">For example: wanting to rollback the function to version V10. Then in the release record list, select the work order with historical version V10, and click rollback. The system will initiate a new release work order, targeting version V10.</div>



1. In the function's release record list, select the target release work order, and click **rollback** from the operation list.

2. In the pop\-up dialog, confirm the version information to be rolled back, and click **confirm** after ensuring it's correct.
