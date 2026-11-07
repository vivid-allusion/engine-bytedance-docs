---
title: "Customizing macOS process configuration"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/customizing-macOS-process-configuration"
---

<span id="3b189ba2"></span>
# Applicable conditions


* The method should be executed on macOS 13 or higher. Variations in system versions typically do not impact the signatures of third\-party applications.

* Certain open\-source applications, including some unsigned or self\-signed applications, are temporarily unsupported.

* The characteristics of software can vary between versions, and it may be necessary to conduct separate tests and provide continuous updates for major versions as needed.


<span id="090bed7f"></span>
# Procedure

<span id="b07b24ae"></span>
## Preparing for authorization

Open Terminal.app and execute the command `sudo eslogger open`.

If you encounter the following error, you need to grant full disk permission.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/511e3706eff948e6ab6d23115400ac99~tplv-goo7wpa0wc-image.image" width="1330px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e844ca850f3a4c79a938063b2941438f~tplv-goo7wpa0wc-image.image" width="902px" /></div>


After authorization, re\-execute the command. It should start outputting a large amount of logs. Use Ctrl+C to terminate the command.

<span id="4301bc9f"></span>
## Gathering and analyzing events

Install the application that needs testing onto your device and create a test file on the desktop, such as demo.txt.

Run the following command, replacing 'demo.txt' with the name of the file you wish to send externally:

```Shell
sudo eslogger open | grep -v com.apple | grep -v corplink | grep -v sealsuite | grep Users | grep Desktop | grep demo.txt
```


Next, send the test file through the application and then terminate the command.

Review the command output, locate the desired application name, and identify the 'signing_id' field within the corresponding record to find the target signature information.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24153be9d21444aea71444f267a34647~tplv-goo7wpa0wc-image.image" width="2522px" /></div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Signature information is case\-sensitive.</div>


* <div data-tips="true" data-tips-type="tip">Since there may be a large number of events, it is advisable to send just one file externally per collection to minimize noise interference.</div>


* <div data-tips="true" data-tips-type="tip">Some applications have multiple processes. If the signing_id is different, all signing_ids must be added as features.</div>


* <div data-tips="true" data-tips-type="tip">Certain process features are designed solely for auditing. Even if you set up blocking, the application may still send successfully due to inherent client logic limitations that do not support blocking.</div>



<span id="8f430b13"></span>
## Verifying features

To avoid false positives and omissions, it is necessary to use the extracted features to further verify feature accuracy.

Execute the following command, replacing `com.google.Chrome` with the extracted signing_id.

```Shell
sudo eslogger open | grep -v com.apple | grep -v corplink | grep -v sealsuite | grep Users | grep Desktop | grep com.google.Chrome
```


Send the previous test Source file again, or use a different test Source file to send, and check the command output for irrelevant File paths (false positives) or missing paths of the source file (omissions).

Continuously optimize the process features until there are no false positives or omissions, and then use the signature information as a feature of the application.
