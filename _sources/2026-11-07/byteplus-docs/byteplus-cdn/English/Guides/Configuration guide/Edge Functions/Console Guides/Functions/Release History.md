---
title: "Release History"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-release-history"
---

This document describes how to manage function versions. You can manage function versions in Edge Functions through the following methods:


* [View code release history](https://docs.byteplus.com/en/docs/18/17377#view-code-release-history)

* [View code of a specific historical version](https://docs.byteplus.com/en/docs/18/17377#view-code-of-a-specific-historical-version)

* [Roll back code to a historical version](https://docs.byteplus.com/en/docs/18/17377#roll-back-code-to-a-historical-version)


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Edge Functions only supports version management for function code, and does not currently support version management for function configurations.</div>


<span id="view-code-release-history"></span>
## View code release history

Follow these steps to view the release history of the code.


1. Open the [Functions](https://console.byteplus.com/cdn/edge-function/list) page.

2. Find your function and click on the function name.

3. Select the **Release history** tab. You can view the historical release records of the function code, including version number, status, release type, release time, and description.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The version number of a function is 1.0.x. Each time you publish the function, the last digit of the version number will increment. For example, the first version number of the function is 1.0.1, and the second version number is 1.0.2.</div>


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_28789c993a7c7e16d71a8eb0e045d3a2.jpeg) </span>

<span id="view-code-of-a-specific-historical-version"></span>
## View code of a specific historical version


1. Open the [Functions](https://console.byteplus.com/cdn/edge-function/list) page.

2. Find your function and click on the function name.

3. Select the **Release history** tab.

4. Find the version you want to view, click **View** in the corresponding Actions column to see the code content of that function version. In the upper left corner of the version details dialog box, you can find the **Compare versions** toggle. Click this toggle to compare the differences between the selected version and the current latest version of the function code.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_d71347e0797c008508f8f1e0a056b0c9.jpeg) </span>


<span id="roll-back-code-to-a-historical-version"></span>
## Roll back code to a historical version


1. Open the [Functions](https://console.byteplus.com/cdn/edge-function/list) page.

2. Find your function and click on the function name.

3. Select the **Release history** tab.

4. Find the version you want to roll back to, click **Rollback** under the **Actions** column.

5. In the **Publish** dialog box that appears, enter your description and select a release type, then click **OK**. Edge Functions will publish a new function version that rolls back to the historical version you specified.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_1124bcf48bd88d9d669053aceff4dc7f.jpeg) </span>
