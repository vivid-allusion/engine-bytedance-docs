---
title: "Version management"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/version_management"
---

When the user uploads the release parameter in the sourcemap and the SDK reports with a release field, version\-related capabilities can be turned on.

<span id=".54mI5pys5YiX6KGo"></span>
## version list


* On the version list page, you can monitor PV, JS error, and related information for all versions you have published.

* The version list supports filtering by release time, environment, and version, enabling you to quickly and accurately find the corresponding version information.


<span id=".54mI5pys6K-m5oOF"></span>
## Version details


* Click Details in the version list to view the details page. At the top of the details page, basic information about the current version is displayed, such as release time, total error count, number of new JavaScript errors in the current version, user count, and other information.

* The overview area displays relevant information about JS errors. Click a specific error to go to JS error details for handling.

* The trend chart shows the changes in some metrics of this version over a recent period of time.

   Under SourceMap, users can manage the SourceMap associated with the current version.


<span id=".5o6l5YWl56S65L6L"></span>
## Integrate examples

When configuring SDK versions, it is recommended to use version\-identifying strings, such as scm version, as this helps monitor exceptions and fragmentation between versions.

```javascript
browserClient('init', {
  ...
  release: 'Characters with version significance',
  ...
})
```
