---
title: "Apmplus plugin compilation error"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Apmplus_plugin_compilation_error"
---

<span id="8e26f2d4"></span>
## AGP compatibility: Supported Gradle versions

The Apm plugin depends on the ByteX base library from ByteDance. Currently, ByteX is still not compatible with AGP versions above 7.2.

If your business is using an incompatible version of AGP, you can try downgrading to a compatible version:


|**The AGP plugin version**<br><br>**classpath 'com.android.tools.build:gradle:x.x.x'**  |**The required Gradle version**<br><br>**distributionUrl=gradle/gradle\-y.y\-all.zip** |**Test compatibility** |
|---|---|---|
|3.0.0+ |4.1+ |yes |
|3.1.0+ |4.4+ |yes |
|3.2.0 \- 3.2.1 |4.6+ |yes |
|3.3.0 \- 3.3.3 |4.10.1+ |yes |
|3.4.0 \- 3.4.3 |5.1.1+ |yes |
|3.5.0 \- 3.5.4 |5.4.1+ |yes |
|3.6.0 \- 3.6.4 |5.6.4+ |yes |
|4.0.0+ |6.1.1+ |yes |
|4.1.0+ |6.5+ |yes |
|4.2.0+ |6.7.1+ |yes |
|7.0.2 |7.1.1 |yes |


You can also use the non\-instrumentation method to integrate directly. For details, refer to [How to integrate monitoring capabilities using the non-instrumentation solution?](https://docs.byteplus.com/en/docs/apmplus/How_to_integrate_monitoring_capability_based_on_a_non-instrumentation_approach).

<span id="abb66b89"></span>
## Compilation failed: A freeze occurred when using ApmPlugin

<span id="954eb325"></span>
#### Error examples

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/98e892b3f22c4f69b8e7e7ba973ed569) </span>

<span id="eab663a0"></span>
#### Solutions

Upgrade to the latest version (at least version 1.3.2), and add the following configuration to gradle.properties:

```Plain
bytex.forbidUseLenientMutationDuringGetArtifact=true
```


<span id="e600bba0"></span>
## Compilation failed: A compilation exception occurred when using ApmPlugin. Failed to resolve class module\-info.class

<span id="dee8d6f9"></span>
#### Exception information

```Plain
java.lang.RuntimeException: java.lang.RuntimeException: java.lang.RuntimeException: Failed to resolve class module-info.class
```


<span id="085f2b33"></span>
#### Solutions

Upgrade to the latest version (at least version 1.3.2), and use the following configuration in `gradle.properties`:

```Plain
bytex.enableDuplicateClassCheck=false
```


<span id="c4ccdc62"></span>
## Compilation failed: This feature requires ASM7

<span id="2a913ff8"></span>
#### Solutions

Add to `gradle.properties`:

```Plain
bytex.ASM_API=ASM7
```


<span id="936d2ffb"></span>
## Compilation failed: java.lang.IllegalStateException: was resolved from a thread not managed by Gradle.

<span id="d4b834b9"></span>
#### Error examples

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b2599dad0014459ac3b37a1247ef6a3~tplv-goo7wpa0wc-image.image) </span>

<span id="bbdb991e"></span>
#### Solutions

Configure the following in `gradle.properties`:

```Plain
bytex.forbidUseLenientMutationDuringGetArtifact=true
```


<span id="97915401"></span>
## Compilation failed: Network request forced type cast exception

<span id="08f841ad"></span>
#### Error examples

<span id="6b2b19ce"></span>
#### Solutions

Taking Tencent Cloud as an example:

Tencent Cloud enforces strong type checking, and after instrumentation, uploading a video generates abnormal logs. You can configure the instrumentation blocklist for Tencent package names:

```Plain
ApmPlugin {
    // Only perform bytecode instrumentation on packages in the whitelist.
    whiteList = [
            "com"
    ]
    
    // Do not perform bytecode instrumentation on classes in the blacklist packages. You can configure the package names and class names that should not be instrumented.
    blackList = [
             "com.tencent"
    ]
}
```


<span id="52886c08"></span>
## Compilation failed: ArrayIndexOutOfBoundsException Caused by: java.lang.RuntimeException: Failed to resolve class XXX

<span id="29c21689"></span>
#### Error examples

```Plain
Caused by: java.lang.RuntimeException: Failed to resolve class a/a/a/a/a.class[
transform input:
        /E:\a_e\bbb\libs\read.jar!a/a/a/a/a.class
project input:
        /E:\a_e\bbb\libs\ read.jar!a/a/a/a/a.class
aar input:not found]
        at com.ss.android.ugc.bytex.common.processor.ClassFileAnalyzer.handle(ClassFileAnalyzer.java:113)
        at com.ss.android.ugc.bytex.transformer.processor.ClassFileProcessor.process(ClassFileProcessor.java:27)
Caused by: java.lang.ArrayIndexOutOfBoundsException
```


<span id="ffd357b1"></span>
#### Solutions

This type of crash is mainly caused by ASM throwing an exception when processing certain class files. Because ByteX forcibly throws all build exceptions, filtering these exceptions requires additional configuration of an allowlist, without modifying the original output.


1. Find out which classes encountered processing errors in the ByteX packaging logs.

   Log files are generally located in the `app/build/ByteX` directory.

2. Create a file named `bytex_whitelist.txt` in the root directory of the project. The file should contain multiple regular expressions, each separated by a carriage return and newline character, which are used to filter class files that cause errors during ASM processing.

   For example, the exception class `a/a/a/a/a.class` in the project can be configured as `a/a/a/a/+`.

3. In the project's `gradle.properties` file, add the property: `bytex.globalIgnoreClassList=bytex_whitelist.txt`. The value of the attribute is the relative path of the allowlist file with respect to the project root directory.


<span id="325b3a9e"></span>
## Compilation failed: The apm plugin conflicts with an existing business plugin.

If the apm plugin has issues, try placing it on the first line so it is compiled and processed first.

```Plain
apply plugin: 'com.android.application'
apply plugin: 'apm-plugin'// Place it first after the application.
apply plugin: 'xxxx'
```


If a third\-party plugin encounters an error, you can place the apm plugin on the last line:

```Plain
apply plugin: 'com.android.application'
apply plugin: 'xxxx'
apply plugin: 'apm-plugin'// Place it last to process the bytecode.
```


Instrumentation is used to facilitate application access to the network and to enable features. If the issue still cannot be resolved, you can integrate monitoring capabilities using a non\-instrumentation approach. For details, refer to [How to integrate monitoring capability based on the non-instrumentation solution?](https://docs.byteplus.com/en/docs/apmplus/How_to_integrate_monitoring_capability_based_on_a_non-instrumentation_approach).

&nbsp;
