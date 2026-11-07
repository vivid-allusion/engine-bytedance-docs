---
title: "Coredump"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Coredump"
---

A core dump is a debugging technique that captures memory information at the time of a crash, enabling offline debugging with LLDB.

Conventional stability monitoring tools only capture information such as stack trace, registers, memory, and more. While these tools can resolve most issues, they often miss much of the contextual information. In contrast, Coredump can dump all program information, providing a massive amount of data for troubleshooting.

In theory, all Signal and Mach exceptions can be resolved.

<span id="4399e62a"></span>
## Prerequisites


* The Coredump module has already been integrated. For details, refer to [iOS SDK integration](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_iOS_SDK_app).

* The coredump sampling rate has been configured. For details, refer to [SDK reporting configuration](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration).

   Configuring the coredump sampling rate allows the feature to be turned on only for a subset of online users. The default sampling rate is 0.

    &nbsp;


<span id=".5q2l6aqk5LiA77ya5paw5bu65bel5L2c56m66Ze0"></span>
## Step 1: Create a workspace

Assume that the folder path is `~/Desktop/CoredumpCase`.

<span id="205b41fd"></span>
## Step 2: Download materials

Since using coredump requires a local installation of LLDB, you need to download the relevant files to your local machine in order to set up the environment required by LLDB.

The following diagram contains all the information required by LLDB. The following will introduce the methods for obtaining them one by one.

<span id="90a8766a"></span>
### .app programs and symbol tables

The following demonstration is conducted using the Products method. If you are using Archive or a packaging tool, please obtain them as appropriate for your situation.


1. In the project, locate `Products`, right\-click the product \> Show in Finder.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/225f1bdd27b34a7d8081a9daac760808~tplv-goo7wpa0wc-image.image) </span>

2. Copy the .app program and the symbol table file into the workspace.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Please do not modify the names of .app programs and symbol tables.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Ensure that the .app program and the symbol table match.   </div>
   

* Method to obtain the UUID of a .app program: `dwarfdump --uuid ${appFilePath}/${appName}`.

   Therefore, the method to obtain the UUID of the APMInsight_iOS app is as follows:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9f7566a36626428e8a2f5c4b7050e521~tplv-goo7wpa0wc-image.image) </span>

* Method to obtain the symbol table UUID: `dwarfdump --uuid ${appFilePath}`.

   Therefore, the method for obtaining the UUID of the APMInsight_iOS symbol table is as follows:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/221921a939814bb3a205a51f5779f442~tplv-goo7wpa0wc-image.image) </span>

    &nbsp;


<span id=".Q3Jhc2jmlofku7Y="></span>
### Crash files


1. On the crash details page, download the crash log.

2. Execute the following command to perform further processing on crash files.

   ```PowerShell
   cat ${crash_path} | jq -r '.data' | awk '{gsub(/\\n/,"\n")}1' > ${output_crash_path}/crash.txt
   ```
   

   Assume that the file path after downloading from the platform is `~/Downloads/20230228210309.txt`. The methods for secondary processing of crash files are:

   ```PowerShell
   cat ~/Downloads/20230228210309.txt | jq -r '.data' | awk '{gsub(/\\n/,"\n")}1' > ~/Desktop/CoredumpCase/crash.txt
   ```
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Ensure that the file name after secondary processing is <code>crash.txt</code>.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">You need to install the Homebrew package management tool. For details, refer to <a href="https://brew.sh/">the Homebrew official website</a>.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Configure the jq command: <code>brew install jq</code>.   </div>
   


<span id="57f7c0a5"></span>
### Core dump files


1. In the crash details page \> file download, locate the Coredump file.

2. Decompress the downloaded Coredump file and rename it as `memorydump`.

3. Copy the Coredump file to the workspace.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Please ensure that the file name is memorydump.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Coredump is not turned on by default. To collect Coredump files, adjust the sampling rate as needed.   </div>
   


<span id="2cc44996"></span>
#### How do we determine which file we need?

Open the generated `crash.txt` file and find the value corresponding to the `Incident Identifier` field.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09ec889fa8ff4e77b88e6ea75f30fce6~tplv-goo7wpa0wc-image.image) </span>

In the file download section, locate `cd-${Incident Identifier's value}.zip`. This is the required Coredump file.

<span id="35f62d84"></span>
### Operating system symbol table

There are many methods to obtain the operating system symbol table. This section introduces how to obtain the operating system symbol table from Xcode.

When performing on\-device debugging with Xcode, Xcode will download the operating system symbol table from the phone. The path is: `~/Library/Developer/Xcode/iOS\ DeviceSupport`. When you open it, you will see:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02c6596275d944feb91efedc888e5eab~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If you cannot find the corresponding symbol table locally, you can obtain the operating system symbol table for the corresponding version via ipsw.</div>


<span id="35ef684b"></span>
#### How do we confirm which file is the one we need?

Open the `crash.txt` file generated earlier, and locate the values for the `Code Type` and `OS Version` fields.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/adb6671b0eff4695831b8adcee3060b8~tplv-goo7wpa0wc-image.image) </span>


* If the Code Type is arm64, then ${OS Version} is the operating system symbol table.

* If the Code Type is arm64e, then ${OS Version}${Code Type} is the operating system symbol table.

   Regarding the above, please ignore the iOS field in ${OS Version}.

   In summary, open 15.5 (19F77) and copy Symbols to the workspace.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ba510ea0e83499fb0c0a8a146d700e7~tplv-goo7wpa0wc-image.image) </span>


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Please make sure to copy only the Symbols folder under the symbol table of the corresponding operating system.</div>


* <div data-tips="true" data-tips-type="warning">Do not modify the structure in Symbols to prevent Coredump parsing failure.</div>



<span id="e579921b"></span>
### Coredump scripts

Please download the appropriate Coredump script according to your Python version. After loading, please move to the workspace.

Method to view Python: `Python3 --version`.


|The Python version |Coredump scripts |
|---|---|
|3.9.6 |<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23a8c211739b474aab597a070a844ad7~tplv-goo7wpa0wc-image.image" name="spliceMemory.so">spliceMemory.so</Attachment><br> |


<span id="b7b10298"></span>
### List of artifacts

After completing the above actions, the workspace appears as shown in the following figure.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a30326a27cd24884969b7a09e1f1dc07~tplv-goo7wpa0wc-image.image) </span>

<span id="9d0ba8af"></span>
## Step 3: Consume data

<span id="de83a378"></span>
### Analyze a core dump with LLDB

After completing the above actions, you can perform the following steps to turn on lldb debugging.


1. cd to the workspace.

2. Start LLDB.

3. While LLDB is in status, load the Coredump script.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f3e74da0ed4145a89f6b69d097549d75~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When executing <code>command script import spliceMemory</code>, <code>spliceMemory</code>should not include<code>.so</code>.   </div>
   

<span id="01f7d5ff"></span>
### Debugging tips

After turning on Coredump, you can use [LLDB commands](https://lldb.llvm.org/use/map.html) for actions.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Debugging techniques are the same as executing commands in Xcode.</div>


A mediation diagram:
