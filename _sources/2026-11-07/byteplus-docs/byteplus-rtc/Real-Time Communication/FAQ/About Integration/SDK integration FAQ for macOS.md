---
title: "SDK integration FAQ for macOS"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1152682"
---

When integrating the RTC SDK, you need to import the SDK package into the app. If the SDK package file is not placed in the default directory, it may cause problems such as RTC SDK not finding dependent libraries (such as libbytenn, libbytevc0, etc.) and causing crashes.

<span id="terms-explained"></span>
## Terms Explained

`@rpath` (runpath): A variable that holds one or more paths, telling the linker where to find libraries.

`@executable_path`: Represents the directory where the executable program is located.

`@loader_path`: Represents the directory where each loaded binary (including App, dylib, framework, plugin, etc.) is located.

<span id="recommended-path-for-sdk-package-file"></span>
## Recommended Path for SDK Package File

The default `@rpath` for the APP is app/Contents/Frameworks, and the `@rpath` of the RTC SDK is the current directory. It is recommended that the SDK package file be placed in the default directory uniformly.

<span id="what-should-i-do-if-the-sdk-package-cannot-be-placed-in-the-recommended-path"></span>
## What should I do if the SDK package cannot be placed in the recommended path?

If for some reason the SDK package file cannot be placed uniformly in the default directory, but needs to be placed in a custom directory, then the `@rpath` should be modified to redirect the SDK dependencies to ensure that the RTC SDK can find the dependent libraries normally.

**Example**:


1. The `Custom Folder` contains the relevant files of the RTC SDK and its dependencies. Now the BytePlusRTC needs to depend on the libAGFX.dylib, libbytenn.dylib, libbytevc0.dylib, and libeffect.dylib files.

2. Open a terminal in the file path and use the command `otool -L BytePlusRTC` to view the dependencies and library paths of the executable file.

3. Use the command `install_name_tool -change @rpath/libAGFX.dylib @loader_path/../../../libAGFX.dylib BytePlusRTC` sequentially to change the `@rpath` path of the dependent library to a relative path based on `@loader_path`.
