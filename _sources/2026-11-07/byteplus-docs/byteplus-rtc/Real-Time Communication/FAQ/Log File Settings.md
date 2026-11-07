---
title: "Log File Settings"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-114721"
---

<span id="call-the-api-to-set-log-information-recommended"></span>
## Call the API to set log information (Recommended)

Since version 3.54, you can use the `setLogConfig` method to customize the local log level, storage path, and maximum log file size. Please refer to the API documentation for more detailed information.


| |Android |iOS |macOS |Windows |Electron |Web |
|---|---|---|---|---|---|---|
|API |[setLogConfig](https://docs.byteplus.com/en/docs/12/docs-70080#setlogconfig) |[setLogConfig](https://docs.byteplus.com/en/docs/12/docs-70086#setlogconfig) |[setLogConfig](https://docs.byteplus.com/en/docs/12/docs-70092#setlogconfig) |[setLogConfig](https://docs.byteplus.com/en/docs/12/docs-70095#setlogconfig) |[setLogConfig](https://docs.byteplus.com/en/docs/12/docs-85532#static-setlogconfig) |[setLogConfig](https://docs.byteplus.com/en/docs/12/docs-104478#setlogconfig) |


<span id="default-log-file-settings"></span>
## Default log file settings

If API is not called to set local log information, the default local log's storage path, file size, and log level are as follows.

<span id="storage-path"></span>
### Storage path

Android: `/data/data/{packageName}/files/rtc_log/bytertc_log/Logs`

iOS: `${HOME}/Documents/bytertc/monitor/bytertc_log/Logs`

macOS: `${HOME}/.bytertc/monitor/bytertc_log/Logs`

Windows: `C:\Users\admin\AppData\Roaming\BytertcLog\Logs`

Linux: `${HOME}/.bytertc/monitor/bytertc_log/Logs`

<span id="file-size"></span>
### File size

Individual log files have a maximum size of 2 MB. The total size limit for log files on mobile devices is 100 MB, while on PC, it is 500 MB. When the total size of the log files reaches the limit, the oldest log files will be deleted.

<span id="log-level"></span>
### Log level

Only events with the level of `warning` or higher will be logged.
