---
title: "Defining appropriate Java 8 heap memory in containers"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Defining_appropriate_Java_8_heap_memory_in_containers"
---

This topic mainly describes best practices for defining appropriate Java 8 heap memory in VKE and VCI of BytePlus.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

When you deploy Java applications, you need to define the amount of memory the Java virtual machine (JVM) can use, which is the maximum heap memory (MaxHeapSize). When you deploy traditional virtual machines or physical machines, you can use the command line parameters `-Xmx`, `-Xms`, and `-Xss` to define the heap memory. This is because resource (such as memory) limits on virtual machines or physical machines are often fixed, which allows you to use a fixed command to start the applications. However, pod resource limits can be easily changed in Kubernetes environments, making the manual method of specifying heap memory via command\-line parameters less suitable.

In Kubernetes environments, users typically want the JVM to automatically allocate an appropriate MaxHeapSize based on the value of the `spec.containers.resources.limits.memory` parameter of the pod. Therefore, VKE and VCI provide a solution for defining appropriate Java 8 heap memory.

<span id=".6Ieq5Yqo5YyW6YWN572u5pa55byP5a6e6aqM"></span>
## Experiments on automatic configuration methods

As Kubernetes becomes widespread, Java has continuously optimized its capabilities to adapt to Kubernetes. Java provides multiple methods in different Java Development Kit (JDK) versions to automatically obtain resource limits within the container environment and specify the maximum heap memory accordingly. In this topic, experiments are conducted across different JDK versions to determine whether each configuration method can run VKE and VCI business pods as expected.

Before the experiments begin, you can run the following command to obtain the maximum heap memory size in the current environment:

```Java
$ java -XshowSettings:vm -version
VM settings:
    Max. Heap Size (Estimated): 479.50M
    Ergonomics Machine Class: client
    Using VM: OpenJDK 64-Bit Server VM

openjdk version "1.8.0_252"
OpenJDK Runtime Environment (AdoptOpenJDK)(build 1.8.0_252-b09)
OpenJDK 64-Bit Server VM (AdoptOpenJDK)(build 25.252-b09, mixed mode)
```


In the preceding code, the value of `Max.` `Heap Size (Estimated)` indicates the maximum heap memory size.

<span id=".amRrLeeJiOacrC04dTEzMQ=="></span>
### JDK version <= 8u131

In versions earlier than JDK 8u131, Java processes running in containers cannot automatically detect the memory limit set by Kubernetes for the containers. Therefore, an appropriate heap memory value cannot be automatically specified, and can only be manually specified through the `-Xmx`, `-Xms`, and `-Xss` commands.

<span id=".Xzh1MTMxLWpkay3niYjmnKwtOHUxOTE="></span>
### 8u131 <= JDK version < 8u191

In JDK 8u131, an experimental parameter `UseCGroupMemoryLimitForHeap` is added, which can detect the container memory limit and automatically specify an appropriate heap memory value when used together with the `UnlockExperimentalVMOptions` parameter.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">A better alternative to the <code>UseCGroupMemoryLimitForHeap</code> parameter is available after JDK 8u191. We do not recommend that you use this parameter to define Java 8 heap memory unless you must use a version from JDK 8u131 to 8u191.</div>


* <div data-tips="true" data-tips-type="tip">The <code>UseCGroupMemoryLimitForHeap</code> parameter only supports Linux cgroup v1 and does not support cgroup v2. In clusters, applications deployed through the VCI method use cgroup v2. Therefore, this solution does not apply to VCI business applications.</div>



<span id=".Xzh1MTkxLWphdmEt54mI5pysLTh1MTky"></span>
### 8u191 <= Java version <= 8u192

Starting from JDK 8u191, Java provides the `UseContainerSupport` feature to enable automatic detection of the container memory limit. This feature is enabled by default. Therefore, you do not need to add this parameter to the Java startup command.

In a VKE cluster environment that meets the Java version requirements, run the following command in an application container deployed through the Elastic Container Service (ECS) method, with a container memory limit of 2048 MiB, to obtain the maximum heap memory size in the current environment. The result is as follows:

```java
$ java -XshowSettings:vm -version
Picked up JAVA_TOOL_OPTIONS: -XX:+UnlockExperimentalVMOptions -XX:+UseCGroupMemoryLimitForHeap
VM settings:
    Max. Heap Size (Estimated): 494.94M
    Ergonomics Machine Class: server
    Using VM: OpenJDK 64-Bit Server VM

openjdk version "1.8.0_192"
OpenJDK Runtime Environment (AdoptOpenJDK)(build 1.8.0_192-b12)
OpenJDK 64-Bit Server VM (AdoptOpenJDK)(build 25.192-b12, mixed mode)
```


The result indicates that the maximum heap memory size is 494.94 MiB, and the container memory limit is 2048 MiB. That means that the maximum heap memory is about one quarter of the container memory limit. One quarter is a default setting, and you can adjust the ratio based on your business requirements. For details, see the [Appendix](https://docs.byteplus.com/en/docs/vke/Defining_appropriate_Java_8_heap_memory_in_containers#maxramfraction) of this topic.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The JDK of this version only automatically specifies <code>-XX:+UnlockExperimentalVMOptions -XX:+UseCGroupMemoryLimitForHeap</code>. JDK 8u191\-8u192 still cannot automatically detect the container memory limit in a cgroup v2 environment. Therefore, this solution does not apply to VCI business applications.</div>


<span id=".amF2YS3niYjmnKwtOHUzNzI="></span>
### Java version \>= 8u372

Starting from JDK 8u372, the `UseContainerSupport` feature provided by Java supports cgroup v2.

In a VKE cluster environment that meets the Java version requirements, run the following command in an application container deployed through the VCI method, with a container memory limit of 2048 MiB, to obtain the maximum heap memory size in the current environment. The result is as follows:

```java
$ java -XshowSettings:vm -version
VM settings:
    Max. Heap Size (Estimated): 479.50M
    Ergonomics Machine Class: client
    Using VM: OpenJDK 64-Bit Server VM

openjdk version "1.8.0_201"
OpenJDK Runtime Environment (IcedTea 3.11.0) (Alpine 8.201.08-r1)
OpenJDK 64-Bit Server VM (build 25.201-b08, mixed mode)
```


Compared with the experiment in the **8u191 <= Java version <= 8u192** section, the container memory limit detected in the VCI environment is slightly smaller than in the VKE environment. As a result, the automatically specified maximum heap memory size is slightly smaller, which aligns with the technical principles of MicroVM.

<span id=".5a6e6aqM57uT5p6c"></span>
## Experiment results

To apply the automatic detection of container memory to both applications deployed through ECS (standard containers) and VCI (elastic containers), test various combinations of JDK versions and command parameters in both standard and elastic containers in this topic. Then, observe whether the commands can run and whether the allocated maximum heap memory is correct. The conclusions are as follows:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>spec.containers.resources.limits.memory</code> is set to 2048 MiB for each pod in the test environment, and the VKE node memory is 32 GiB.</div>



|JDK version |Command line parameter |Standard Container ||VCI ||Test result |
|---|---|---|---|---|---|---|
|||Normal operation |MaxHeapSize |Normal operation |MaxHeapSize ||
|8u131 |UnlockExperimentalVMOptions UseCGroupMemoryLimitForHeap |Yes |455.50M |No |No |Non\-compliant |
||No parameters added |Yes |6.80G |Yes |479.50M |Non\-compliant |
|8u191 |UnlockExperimentalVMOptions UseCGroupMemoryLimitForHeap |Yes |494.94M |No |No |Non\-compliant |
||UseContainerSupport |Yes |494.94M |No |No |Non\-compliant |
|8u372 |UnlockExperimentalVMOptions UseCGroupMemoryLimitForHeap |Yes |494.94M |No |No |Non\-compliant |
||UseContainerSupport |Yes |494.94M |Yes |479.50M |Compliant |


The test results indicate that to ensure that the automatic detection of container memory works as expected in both standard containers and elastic containers, the following conditions need to be met:


* Use JDK 8u372 or later.

* Do not use the combination of the deprecated parameters `UnlockExperimentalVMOptions` and `UseCGroupMemoryLimitForHeap`, and do not add other parameters to the startup parameters. Keep `UseContainerSupport` enabled by default.


<span id=".6ZmE5b2V"></span>
## Appendix

The following section also introduces other parameters related to heap memory settings.

<span id="maxramfraction"></span>
### MaxRAMFraction

In the OpenJDK environment, when automatic container memory detection is enabled, the system uses 1/4 of the container memory limit as the maximum heap memory value by default. You can adjust the denominator by using the `MaxRAMFraction` parameter. For example, if you set the value to 2, you can use one half of the container memory limit as the maximum heap memory value.

```Java
$ java -XX:MaxRAMFraction=2 -XshowSettings:vm -version
VM settings:
    Max. Heap Size (Estimated): 957.00M
    Ergonomics Machine Class: client
    Using VM: OpenJDK 64-Bit Server VM

openjdk version "1.8.0_201"
OpenJDK Runtime Environment (IcedTea 3.11.0) (Alpine 8.201.08-r1)
OpenJDK 64-Bit Server VM (build 25.201-b08, mixed mode)
```


<span id="maxrampercentage"></span>
### MaxRAMPercentage

In Oracle JDK, you can replace the `MaxRAMFraction` parameter with the `MaxRAMPercentage` parameter, which achieves the same capability. For details, see the [official Oracle documentation](https://www.oracle.com/java/technologies/javase/8all-relnotes.html#R180_191).
