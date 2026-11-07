---
title: "Disk monitor"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/disk_monitor"
---

Excessive disk usage can lead to insufficient disk space on a mobile device, affect the performance of the app, and may even cause users to uninstall the app to free up disk space. Disk monitor helps users monitor mobile device disk space and App Storage Usage, identify folders and files that occupy excessive disk space, and detect forgotten expired files.

<span id="6d894485"></span>
## **Prerequisites**


* Disk monitor has been integrated. For details, refer to [Android SDK integration](https://docs.byteplus.com/en/docs/apmplus/Android_SDK_integration) and [iOS SDK integration](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_iOS_SDK).

* Disk monitor has been configured. For details, refer to [SDK setting](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration).


<span id="ea955b8b"></span>
## disk metrics

<span id="90ed9b5f"></span>
### Filter criteria

You can filter data using the following filter criteria.


* Filter dimensions supported by the Android operating system:

   Time, Device ID, User ID, OS version, APP version, APP minor version, device model, APM SDK Version, download channel.

* The filter dimensions supported by the iOS operating system:

   Time, Device ID, User ID, jailbreak status, OS version, app version, app minor version number, device model, APM SDK Version, download channel.


<span id="35058434"></span>
### iOS disk metrics

The iOS disk metrics display shows a trend chart of iOS disk metrics based on the filter conditions, and by default displays the average values of certain disk metrics and the sample size.

Click **metric details** to view the disk trend chart and multidimensional analysis.

Metric description:


|**Metric** |**DescriptionS** |
|---|---|
|disk size |disk size |
|device free storage |Device free storage size |
|App Storage Usage |The total size of files in the sandbox |
|App Storage Usage Percentage |**App storage usage/phone storage** |
|App Library and Document Storage Size |Total size of Library and Document files in the sandbox |


<span id="a62bf229"></span>
### Android disk metrics

Android disk metrics displays a trend chart of disk metrics under filter conditions. By default, it displays the average values of certain disk metrics and the sample size.

Click **Metric details**, and view the disk trend chart and multidimensional analysis.

Metrics description


|**Metric** |**DescriptionS** |
|---|---|
|disk size |**Environment.getDataDirectory().getTotalSpace() + Environment.getRootDirectory().getTotalSpace()**  |
|device free storage |**Environment.getDataDirectory().getFreeSpace()**  |
|App Storage Usage |**context.getFilesDir().getParent() + context.getExternalFilesDir(null).getParentFile()**  |
|App Storage Usage Percentage |**App storage usage/phone storage** |
|App Cache Storage |**context.getCacheDir() + context.getExternalCacheDir()**  |


<span id="a38f684c"></span>
## directory analytic

<span id="3849e3b8"></span>
### Filter criteria

You can filter data using the following filter criteria.


* Filter dimensions supported by the Android operating system:

   Time, Device ID, User ID, OS version, APP version, APP minor version, device model, APM SDK Version, download channel.

* Filter dimensions supported by the iOS operating system:

   Time, Device ID, User ID, jailbreak status, OS version, app version, app minor version number, device model, APM SDK Version, download channel.


<span id="be2cda86"></span>
### Subdirectory trend charts

The directory analytic trend chart can analyze directories and files that occupy significant space within App Storage Usage, and supports hierarchical drill\-down analysis.

To prevent differences in directory prefixes obtained on different device models, Android uses 'internal' and 'external' as substitute markers for the directory prefix.


|**Directory prefix** |**DescriptionS** |
|---|---|
|Root file |App Storage Usage is represented by**context.getFilesDir().getParent() + context.getExternalFilesDir(null).getParentFile()**  |
|internal |Represents the directory **context.getFilesDir().getParent()**  |
|external |Represents the directory **context.getExternalFilesDir(null).getParentFile()**  |


Metric description:


|Metric |DescriptionS |
|---|---|
|report volume |Directory report count |
|path percentage |**Current directory size/App Storage Usage** |
|disk usage |Current directory size |
|reporting user |Directory reporting user count |


<span id="76dde5a4"></span>
### Subdirectory list

Parameter description:


|**Parameters** |**DescriptionS** |
|---|---|
|Average size |The current directory size is the average value obtained by aggregating multiple reported data points. |
|Size ratio |**Current directory size/App Storage Usage** |
|Weighted average size |**Average size × (current directory report volume / root file report volume)** <br><br>To prevent scenarios where a directory is reported only once, but because it contains a very large file, it always appears at the top of the sorted list. |


<span id="eeae6920"></span>
## disk anomaly

<span id="171637ff"></span>
### Filter criteria

You can filter data using the following filter criteria.


* Filter dimensions supported by the Android operating system:

   Time, file query, Device ID, User ID, exception type, issue new status, OS version, device model, app version, app minor version, APM SDK Version, download channel, ROM Information, province, manufacturer, issue status, assignee, tag, custom dimension, PV custom dimension.

* Filter dimensions supported by the iOS operating system:

   Time, file query, Device ID, User ID, exception type, issue new status, jailbreak status, OS version, device model, app version, app minor version, APM SDK Version, download channel, province, issue status, assignee, tag, custom dimension, PV custom dimension.


<span id="3b7116f0"></span>
### Exception trends

Exception trends primarily analyze scenarios where App Storage Usage exceeds the specified threshold, examining the current large files and folders, as well as expired files that have exceeded a certain time limit.

<span id="98239aac"></span>
### Exception distribution

In the Exception Distribution section, you can view an overview of the distribution of exceptions where App Storage Usage exceeds the specified threshold.


* By default, the distribution is displayed based on report volume, with the option to switch to user volume.

* By default, the distribution is displayed by exception type, OS version, device model, and APP version. Configuration is supported for additional dimensions such as APP minor version, APM SDK Version, download channel, and province.


<span id="407a8ee2"></span>
### Exception file list


* Exception detail: Click to enter the exception detail page.


<span id="6acc5d44"></span>
### exception detail

The disk anomaly details page allows for in\-depth analysis of the detailed data for each disk anomaly.

Metric description:


|**Metric** |**DescriptionS** |
|---|---|
|exception count |Exception report count under filter conditions |
|Exception rate |Number of exception occurrences under filter conditions / total page views under filter conditions |
|impacted user |Exception reporting user count under filter conditions |
|impacted users rate |Number of users who reported exceptions under filter conditions / total unique visitors under filter conditions |


The details page supports viewing specific information about exception files, exception folders, and expired files.


|Metric |Android metrics definitions |iOS metric definitions |
|---|---|---|
|Exception files |For users included in the "disk anomaly sampling rate", when App Storage Usage exceeds the "exception disk usage threshold", the app files are sorted from largest to smallest. The top files, up to the "maximum number of exception files to report", are selected and reported. |For users who are sampled for 'disk anomaly', if their App Storage Usage exceeds the 'disk file usage analysis threshold', the App files are sorted in descending order by size to obtain the largest files for reporting, with the number of files reported being up to the 'maximum number of exception files to report'. |
|Exception folder |For users selected according to the disk anomaly sampling rate, if the App Storage Usage exceeds the exception disk usage threshold, only up to the exception file maximum report count of subfiles in the App folder that exceed the exception folder disk threshold will be reported. |For users who match the "disk anomaly sampling rate" and whose App Storage Usage exceeds the "disk file usage analysis threshold", a folder is defined as an exception folder if its size exceeds the "exception folder disk threshold" or if the number of files it contains exceeds the "exception folder quantity threshold". Sort folders by size, and report the top folders up to the value specified by "maximum number of exception files to report". |
|Expired files |For users who match the "disk anomaly sampling rate" and whose App Storage Usage exceeds the "exception disk usage threshold", report up to the "exception file maximum report count" of App files whose lastModified time is older than the "file expiration time threshold". |For users who meet the "disk anomaly sampling rate" criteria, when the App Storage Usage exceeds the "disk file usage analysis threshold", report the top "maximum exception file report count" App files whose last access time from now exceeds the "file expiration time threshold". |
