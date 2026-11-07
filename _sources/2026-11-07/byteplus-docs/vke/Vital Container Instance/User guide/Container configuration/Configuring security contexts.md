---
title: "Configuring security contexts"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring-a-security-context"
---

This topic describes how to configure security contexts for pods or containers in VCI, which define the permissions and access control of the pods or containers.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Security Contexts are used to define the permissions and access control of pods or containers, such as discretionary access control, SELinux, and Linux capabilities. For more information, see [Security Contexts](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/).

Kubernetes provides security context configuration methods at both the pod and container levels:


* Pod security contexts: Apply to all containers and volumes within a pod. For the parameters supported by Kubernetes, see [Pod security context API](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#podsecuritycontext-v1-core).

* Container security context: Applies to the specified container. For the parameters supported by Kubernetes, see Security context API.


<span id=".6YWN572uLXBvZC1zZWN1cml0eS1jb250ZXh0"></span>
## Configuring pod security contexts

VCI allows you to modify sysctls, runAsUser, and runAsGroup by using pod security contexts.

<span id=".5Y-C5pWw6K-05piO"></span>
### Parameter description


|Parameters that can be specified |Type |Description |Kubernetes API |
|---|---|---|---|
|sysctls |List<Sysctl\> |The kernel parameters of the VCI, including:<br><br><br>* kernel.shm\* (excluding kernel.shm_next_id and kernel.shm_rmid_forced)<br><br>* kernel.msg\* (excluding kernel.msg_next_id)<br><br>* kernel.sem<br><br>* fs.mqueue.\*<br><br>* net.\* (excluding net.ipv4.ip_local_port_range and net.ipv4.tcp_syncookies)<br><br>* vm.min_free_kbytes |[Sysctl v1 core](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#sysctl-v1-core) |
|runAsUser |integer |The user ID to run the container. If specified, it overrides the USER instruction in the Dockerfile. |\- |
|runAsGroup |integer |The user group ID to run containers. If specified, all processes in all containers within the specified pod will run with this user group ID.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If runAsGroup is specified, runAsUser must also be specified.</div><br> |\- |


<span id=".6YWN572u56S65L6L"></span>
### Configuration examples


* Sample parameters for sysctls:

   ```yaml
   apiVersion: v1
   kind: Pod
   metadata:
     name: security-context-pod-sysctls-demo
   spec:
     securityContext:  #Pod-level security context configuration
       sysctls:  #sysctls parameters
         - name: kernel.shmmax
           value: "18446744073692774399"
         - name: kernel.msgmax
           value: "8192"
         - name: kernel.sem
           value: "32000 1024000000 500 32000"
     containers:
     - name: busybox
       image: busybox
       command: ["sh", "-c", "sleep 10000"]
   ```
   

* Example parameters for runAsUser:

   ```yaml
   apiVersion: v1
   kind: Pod
   metadata:
     name: security-context-pod-runAsUser-demo
   spec:
     securityContext:  # Pod-level security context configuration
       runAsUser: 1000  #runAsUser parameters
     containers:
     - name: busybox
       image: busybox
       command: ["sh", "-c", "sleep 10000"]
   ```
   

* Example parameters for runAsGroup:

   ```yaml
   apiVersion: v1
   kind: Pod
   metadata:
     name: security-context-pod-runAsUser-demo
   spec:
     securityContext:  #Pod-level security context configuration
       runAsUser: 1000  #runAsUser parameters
       runAsGroup: 1000  #runAsGroup parameters
     containers:
     - name: busybox
       image: busybox
       command: ["sh", "-c", "sleep 10000"]
   ```
   


<span id=".6YWN572uLWNvbnRhaW5lci1zZWN1cml0eS1jb250ZXh0"></span>
## Configuring container security contexts

VCI allows you to modify runAsUser, runAsGroup, and capabilities by using container security contexts.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you configure shared parameters (such as runAsUser) in both the pod and container security contexts, the container's settings will override the pod's settings.</div>


<span id=".5Y-C5pWw6K-05piO"></span>
### Parameter description


|Configurable parameter |Type |Description |Kubernetes API |
|---|---|---|---|
|runAsUser |integer |The user ID to run the container. If specified, it overrides the USER instruction in the Dockerfile. |\- |
|runAsGroup |integer |The user group ID to run the container. If specified, all processes in the specified container run with the user group ID. |\- |
|capabilities |List<String\> |Grant some specific permissions to processes running in the container.<br><br>You can grant the following permissions:<br><br><br>* AUDIT_WRITE<br><br>* CHOWN<br><br>* DAC_OVERRIDE<br><br>* FSETID<br><br>* FOWNER<br><br>* KILL<br><br>* MKNOD<br><br>* NET_ADMIN<br><br>* NET_BIND_SERVICE<br><br>* NET_RAW<br><br>* SETGID<br><br>* SETUID<br><br>* SETFCAP<br><br>* SETPCAP<br><br>* SYS_CHROOT<br><br>* SYS_PTRACE<br><br>* SYS_RAWIO<br><br>* SYS_TIME<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><strong>SYS_RAWIO</strong> and <strong>SYS_TIME</strong> are at the beta stage. To use these capabilities, <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000210">submit a ticket</a> to apply.</div><br> |[Capabilities v1 core](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#capabilities-v1-core) |


The following table describes some parameters that cannot be specified.


|Parameters that cannot be specified |Description |Native Kubernetes API |
|---|---|---|
|privileged |Whether to run the container in privileged mode. Processes in a privileged container have root privileges equivalent to those on the host. The default value is **false**. |Yes |
|readOnlyRootFilesystem |Specifies whether the container's root filesystem is read\-only. The default value is **false**, which means the root filesystem is readable and writable. |Yes |
|procMount |Specify the type of proc that the container can mount. The default value is **DefaultProcMount**. |Yes |


<span id=".6YWN572u56S65L6L"></span>
### Configuration examples


* Example parameters for runAsUser:

   ```yaml
   apiVersion: v1
   kind: Pod
   metadata:
     name: security-context-container-runAsUser-demo
   spec:
     containers:
     - name: busybox01
       image: busybox
       command: ["sh", "-c", "sleep 10000"]
     - name: busybox02
       image: busybox
       command: ["sh", "-c", "sleep 10000"]
       securityContext:  #Container-level security context configuration
         runAsUser: 2000  #Container-level runAsUser parameters
   ```
   

* Example parameters for runAsGroup:

   ```yaml
   apiVersion: v1
   kind: Pod
   metadata:
     name: security-context-container-runAsUser-demo
   spec:
     containers:
     - name: busybox01
       image: busybox
       command: ["sh", "-c", "sleep 10000"]
     - name: busybox02
       image: busybox
       command: ["sh", "-c", "sleep 10000"]
       securityContext:  #Container-level security context configuration
         runAsGroup: 2000  #Container-level runAsGroup parameters
   ```
   

* Example parameters for capabilities:

   ```yaml
   apiVersion: v1
   kind: Pod
   metadata:
     name: security-context-container-runAsUser-demo
   spec:
     containers:
     - name: busybox01
       image: busybox
       command: ["sh", "-c", "sleep 10000"]
       securityContext:  # Container-level security context configuration
         capabilities:  # capabilities parameters
           add: ["NET_ADMIN", "CHOWN", "SYS_CHROOT"]
   ```
