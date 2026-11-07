---
title: "Persistent storage of container core dump files"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Container-coredump-persistence"
---

VCI allows you to obtain process core dump files, which enables you to analyze and locate container exceptions. This topic mainly describes how to achieve the persistent storage of container core dump files in VCI.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

The core dump is the process in which the operating system saves the current memory state of a program into a core file when the program abnormally terminates due to a runtime exception. If a VCI container abnormally terminates and the application log does not provide enough information to locate the root cause, you need to use the core dump file for further analysis and troubleshooting. This topic describes how to enable containers to generate core dump files and save them to external storage.

<span id=".5Yqf6IO95LuL57uN"></span>
## Feature introduction

By default, core dumps are disabled for VCIs to prevent excessive disk usage that can lead to service unavailability. You can enable core dumps by using pod annotations when creating a VCI.


|Annotation Key |Annotation sample value |Description |Required |
|---|---|---|---|
|vci.vke.volcengine.com/core\-pattern |"/data/coredump/core.%h.%e.%p.%t" |Specify the path where core dump files are saved for the VCI. After you specify the path, the core dump capability of the VCI is automatically enabled.<br><br>Sample value format: `/data/coredump/core.%h.%e.%p.%t`. The value description is as follows:<br><br><br>* `/data/coredump/`: The directory for saving the core dump file. Replace the value with your own directory.<br><br>* `core.%h.%e.%p.%t`: The name of the core dump file. `%h`, `%e`, `%p`, and `%t` are placeholders, which you can configure based on your business requirements. The placeholder descriptions are as follows:<br><br>   * `%h`: The name of the VCI pod (hostname). This configuration is recommended.<br><br>   * `%e`: The program file name. This configuration is recommended.<br><br>   * `%p`: The process ID. This configuration is optional.<br><br>   * `%t`: The time of the core dump. This configuration is optional.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The configured path cannot start with <code>\|</code>, which indicates that you cannot use a core dump to configure an executable program.</div><br> |Required in this scenario |


The complete path example for the final generated core dump file is as follows:

```Bash
/data/coredump/core.nginx-7855fc5b44-p2rzt.bash.36.1602488967
```


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A cluster that uses VCI has been created. For details, see [Using VCI in VPC-CNI clusters](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Vital-Kubernetes-Engine) and [Using VCI in Flannel clusters](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Flannel-cluster).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

Core dump files are typically used for offline issue analysis. Therefore, when you configure a path for saving core dump files, we recommend that you use attached storage rather than built\-in storage (local container paths). This prevents the loss of core dump files when the container exits.

The following example demonstrates how to enable the core dump capability for a VCI Deployment by using FileNAS as attached storage. This is achieved by mounting FileNAS to the VCI Deployment via the PV method. For detailed instructions and YAML field descriptions, see [Using FileNAS as static PersistentVolumes](https://docs.byteplus.com/en/docs/vke/Using-static-NAS-Volumes).


1. Connect to the VPC\-CNI cluster.

   For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Create a PV of the FileNAS type.

   1. Create a YAML file for the PV. The following `vci-nas-pv.yaml` file serves as an example:

      ```YAML
      apiVersion: v1
      kind: PersistentVolume
      metadata:
        name: vci-nas-pv  # The name of the PV.
      spec:
        accessModes: 
        - ReadWriteMany
        capacity:
          storage: 100Gi # FileNAS storage capacity.
        csi:
          driver: nas.csi.volcengine.com 
          volumeAttributes:
            fsId: enas-cnbj1b9f********  # The ID of the FileNAS file system. This parameter needs to be specified only if the file system type is Extreme speed.
            fsType: Extreme   # File system type. Valid values include Extreme, Cache, and Capacity.
            path: /enas-cnbj1b9f********/temp  # The subdirectory of the FileNAS file system for mounting.
            server: cnbj1b9f********.r*********.nas.ivolces.com  # The mount point of the FileNAS file system.
            volumeAs: subpath  # The subdirectory type. Valid values include subpath and filesystem.
          volumeHandle: vci-nas-pv  # The unique identifier of the PV. Keep it consistent with the PV name.
        mountOptions:
        - nolock,proto=tcp,noresvport
        - vers=3  
        persistentVolumeReclaimPolicy: Retain 
        volumeMode: Filesystem 
      ```
      

   2. Run the following command to create the PV.

      ```Bash
      kubectl create -f vci-nas-pv.yaml
      ```
      

3. Create a PersistentVolumeClaim (PVC).

   1. Create a YAML file for the PVC. The following `vci-nas-pvc.yaml` file serves as an example:

      ```YAML
      apiVersion: v1
      kind: PersistentVolumeClaim
      metadata:
        name: vci-nas-pvc  # The name of the PVC.
        namespace: default
      spec:
        accessModes:
        - ReadWriteMany 
        resources:
          requests:
            storage: 100Gi 
        volumeMode: Filesystem 
        volumeName: vci-nas-pv  # The name of the PV bound to this PVC.
      ```
      

   2. Run the following command to create the PVC.

      ```Bash
      kubectl create -f vci-nas-pvc.yaml
      ```
      

4. Create a VCI, configure a path for storing core dump files, and enable core dumps for the VCI.

   The following content provides an example of how to create a VCI Deployment. For instructions on creating a VCI, see [Creating instances](https://docs.byteplus.com/en/docs/vke/Creating-an-instance).

   1. Create a YAML file for the VCI Deployment. The sample YAML file `vci-nas-coredump-deployment.yaml` is as follows:

      ```YAML
      apiVersion: apps/v1
      kind: Deployment
      metadata:
        name: vci-nas-coredump-deployment  # The name of the Deployment.
        namespace: default  # The namespace of the Deployment.
        labels:
          app: vci-nas-coredump-deployment
      spec:
        replicas: 2
        selector:
          matchLabels:
            app: vci-nas-coredump-deployment
        template:
          metadata:
            annotations:
              vke.volcengine.com/burst-to-vci: enforce  # Force the use of VCI.
              vci.vke.volcengine.com/preferred-instance-family: vci.u1  # Specify the instance family of VCI.
              vci.vke.volcengine.com/core-pattern: "/data/coredump/core.%h.%e.%p.%t"      # Specify the path where the core dump file is saved.
            labels:
              app: vci-nas-coredump-deployment
          spec:
            containers:
            - image: cr-cn-beijing.volces.com/tw/nginx:1.0 # The address and version of the container image. Replace the value with your actual information.
              imagePullPolicy: IfNotPresent
              name: nginx
              volumeMounts:
              - mountPath: /data/coredump/  # The location where the FileNAS storage is mounted in the container. This must be consistent with the path specified in this topic where the core dump file is saved.
                name: vci-nas-volume  # Specify the volume name.
            volumes:
            - name: vci-nas-volume  # The mount volume.
              persistentVolumeClaim:
                claimName: vci-nas-pvc  # The name of the PVC created in the previous step.
      ```
      

   2. Run the following command to create the Deployment.

      ```Bash
      kubectl create -f vci-nas-coredump-deployment.yaml
      ```
      


<span id=".6aqM6K-B57uT5p6c"></span>
## Validating results

You can trigger a core dump in a VCI for which a directory for saving core dump files is configured.


1. Run the following command to obtain the name of the pod in the VCI Deployment.

   ```Bash
   kubectl get pods -l app=vci-nas-coredump-deployment
   ```
   

2. Run the following command to log in to the VCI pod.

   ```Bash
   kubectl exec -it ${the obtained VCI Pod name}
   ```
   

3. Run the `sleep 100` command in the container and then press `Ctrl+\` to trigger a core dump. The generated core dump file will be automatically saved to FileNAS.

   The expected response is as follows:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_13f817b10b9ab20f186b2fcc55c8b212.jpg) </span>
