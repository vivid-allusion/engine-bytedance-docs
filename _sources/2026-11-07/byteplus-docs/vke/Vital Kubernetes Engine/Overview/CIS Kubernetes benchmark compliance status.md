---
title: "CIS Kubernetes benchmark compliance status"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/CIS_Kubernetes_benchmark_compliance_status"
---

<span id=".5o6n5Yi26Z2i57uE5Lu2"></span>
## Control plane add\-ons

<span id=".bWFzdGVyLeiKgueCuemFjee9ruaWh-S7tg=="></span>
### Master node configuration file


|**Item description** |**VKE** **compliance status** |**Non\-compliance reason** |
|---|---|---|
|Make sure that the permission on the pod configuration file for the API server is set to 600 or stricter. |N/A |VKE adopts a Kubernetes\-on\-Kubernetes architecture in which the control plane is deployed as Kubernetes Deployments, so file permissions on the host node are not applicable. |
|Make sure that the ownership of the pod configuration file for the API server is set to root: root. |N/A |VKE adopts a Kubernetes\-on\-Kubernetes architecture in which the control plane is deployed as Kubernetes Deployments, so file permissions on the host node are not applicable. |
|Make sure that the permission on the pod configuration file for the controller manager is set to 600 or lower. |N/A |VKE adopts a Kubernetes\-on\-Kubernetes architecture in which the control plane is deployed as Kubernetes Deployments, so file permissions on the host node are not applicable. |
|Make sure that the ownership of the pod configuration file for the controller manager is set to root: root |N/A |VKE adopts a Kubernetes\-on\-Kubernetes architecture in which the control plane is deployed as Kubernetes Deployments, so file permissions on the host node are not applicable. |
|Make sure that the permission on the pod configuration file for the scheduler is set to 600 or lower. |N/A |VKE adopts a Kubernetes\-on\-Kubernetes architecture in which the control plane is deployed as Kubernetes Deployments, so file permissions on the host node are not applicable. |
|Make sure that the ownership of the pod configuration file for the scheduler is set to root: root. |N/A |VKE adopts a Kubernetes\-on\-Kubernetes architecture in which the control plane is deployed as Kubernetes Deployments, so file permissions on the host node are not applicable. |
|Make sure that the permission on the pod configuration file for etcd is set to 600 or lower. |N/A |VKE adopts a Kubernetes\-on\-Kubernetes architecture in which the control plane is deployed as Kubernetes Deployments, so file permissions on the host node are not applicable. |
|Make sure that the ownership of the pod configuration file for etcd is set to root: root. |N/A |VKE adopts a Kubernetes\-on\-Kubernetes architecture in which the control plane is deployed as Kubernetes Deployments, so file permissions on the host node are not applicable. |
|Make sure that the permission on the container network interface (CNI) configuration file is set to 644 or lower. |Compliant |None |
|Make sure that the ownership of the CNI configuration file is set to root:root. |Compliant |None |
|Make sure that the permission on the etcd data directory is set to 700 or lower. |Compliant |None |
|Make sure that the ownership of the etcd data directory is set to etcd: etcd or root: root. |Compliant |VKE adopts a Kubernetes\-on\-Kubernetes architecture in which the control plane is deployed as Kubernetes Deployments, so file permissions on the host node are not applicable. The corresponding data directory is mounted into the container through a persistent volume claim (PVC). etcd runs as the root user. Therefore, the owner of the etcd data directory is also set to root:root. We consider the root user to be equivalent to the etcd user. |
|Make sure that the admin.conf file permission is set to 600 or lower. |N/A |The admin.conf file does not exist. |
|Make sure that the ownership of the admin.conf file is set to root:root. |N/A |The admin.conf file does not exist. |
|Make sure that the scheduler.conf file permission value is set to 600 or lower. |N/A |VKE adopts a Kubernetes\-on\-Kubernetes architecture in which the control plane is deployed as Kubernetes Deployments, so file permissions on the host node are not applicable. The ConfigMap file required to start the add\-on is mounted to the container through a volume, and the mount permission value is 644. |
|Make sure that the ownership of the scheduler.conf file is set to root:root. |N/A |VKE adopts a Kubernetes\-on\-Kubernetes architecture in which the control plane is deployed as Kubernetes Deployments, so file permissions on the host node are not applicable. The ConfigMap file required to start the add\-on is mounted to the container through a volume, and the mount permission is 644. |
|Make sure that the controller\-manager.conf file permission value is set to 600 or lower. |N/A |VKE adopts a Kubernetes\-on\-Kubernetes architecture in which the control plane is deployed as Kubernetes Deployments, so file permissions on the host node are not applicable. The ConfigMap file required to start the add\-on is mounted to the container through a volume, and the mount permission value is 644. |
|Make sure that the ownership of the controller\-manager.conf file is set to root: root. |N/A |VKE adopts a Kubernetes\-on\-Kubernetes architecture in which the control plane is deployed as Kubernetes Deployments, so file permissions on the host node are not applicable. The ConfigMap file required to start the add\-on is mounted to the container through a volume, and the mount permission is 644. |
|Make sure that the ownership of the Kubernetes Public Key Infrastructure (PKI) directory and file is set to root:root. |N/A |VKE adopts a Kubernetes\-on\-Kubernetes architecture in which the control plane is deployed as Kubernetes Deployments, so file permissions on the host node are not applicable. The ConfigMap file required to start the add\-on is mounted to the container through a volume, and the mount permission is 644. |
|Make sure that the permission on the Kubernetes PKI certificate file is set to 644 or lower. |N/A |VKE adopts a Kubernetes\-on\-Kubernetes architecture in which the control plane is deployed as Kubernetes Deployments, so file permissions on the host node are not applicable. The ConfigMap file required to start the add\-on is mounted to the container through a volume, and the mount permission is 644. |
|Make sure that the permission on the Kubernetes PKI key file is set to 600. |N/A |VKE adopts a Kubernetes\-on\-Kubernetes architecture in which the control plane is deployed as Kubernetes Deployments, so file permissions on the host node are not applicable. The ConfigMap file required to start the add\-on is mounted to the container through a volume, and the mount permission is 644. |


<span id="api-server"></span>
### API server


|**Item description** |**VKE** **compliance status** |**Non\-compliance reason** |
|---|---|---|
|Make sure that the \-\-anonymous\-auth parameter of the API server is set to false. |Non\-compliant |VKE allows anonymous access to the API server for health checks and resource discovery. In addition, VKE forcibly enables the role\-based access control (RBAC) authorization mode and does not grant anonymous access permissions on other sensitive APIs by default. |
|Make sure that the \-\-token\-auth\-file parameter of the API server is not specified. |Compliant |None |
|Make sure that the \-\-DenyServiceExternalIPs parameter of the API server is not specified. |Compliant |None |
|Make sure that the \-\-kubelet\-client\-certificate and \-\-kubelet\-client\-key parameters of the API server are set correctly. |Compliant |None |
|Make sure that the \-\-kubelet\-certificate\-authority parameter of the API server is set to a valid kubelet certificate authority (CA) certificate. |Compliant |None |
|Make sure that the \-\-authorization\-mode parameter of the API server is not set to AlwaysAllow |Compliant |None |
|Make sure that the \-\-authorization\-mode parameter of the API server includes Node. |Compliant |None |
|Make sure that the \-\-authorization\-mode parameter of the API server includes RBAC. |Compliant |None |
|Make sure that the access control add\-on EventRateLimit is configured. |Compliant |None |
|Make sure that the access control add\-on AlwaysAdmit is not configured. |Compliant |None |
|Make sure that the access control add\-on AlwaysPullImages is configured. |Compliant |None |
|If PodSecurityPolicy is not used, make sure that the access control add\-on SecurityContextDeny is configured. |Non\-compliant |By default, VKE does not enable the SecurityContextDeny admission controller. We recommend that you use Pod security policies to enforce finer\-grained control instead. |
|Make sure that the access control add\-on ServiceAccount is configured. |Compliant |None |
|Make sure that the access control add\-on NamespaceLifecycle is configured. |Compliant |None |
|Make sure that the access control add\-on NodeRestriction is configured. |Compliant |None |
|Make sure that the \-\-secure\-port parameter of the API server is not set to 0. |Compliant |None |
|Make sure that the \-\-profiling parameter of the API server is set to false. |Non\-compliant |VKE performs debugging by using performance profiling. |
|Make sure that the \-\-audit\-log\-path parameter of the API server is specified. |Non\-compliant |Audit logging is a service feature that is disabled by default. You need to enable it manually. After it is enabled, this rule becomes compliant. |
|Make sure that the \-\-audit\-log\-maxage parameter of the API server is set to 30 or to an appropriate value. |Non\-compliant |Audit logging is a service feature that is disabled by default. You need to enable it manually. After it is enabled, this rule becomes compliant. |
|Make sure that the \-\-audit\-log\-maxbackup parameter of the API server is set to 10 or to an appropriate value. |Non\-compliant |Audit logging is a service feature that is disabled by default. You need to enable it manually. After it is enabled, this rule becomes compliant. |
|Make sure that the \-\-audit\-log\-maxsize parameter of the API server is set to 100 or to an appropriate value. |Non\-compliant |Audit logging is a service feature that is disabled by default. You need to enable it manually. After it is enabled, this rule becomes compliant. |
|Make sure that the \-\-request\-timeout parameter of the API server is set to an appropriate value. |Non\-compliant |VKE uses the community default value 1m0s. |
|Make sure that the \-\-service\-account\-lookup parameter of the API server is set to true. |Compliant |None |
|Make sure that the \-\-service\-account\-key\-file parameter of the API server is set to an appropriate value. |Compliant |None |
|Make sure that the \-\-etcd\-certfile and \-\-etcd\-keyfile parameters of the API server are set to appropriate values. |Compliant |None |
|Make sure that the \-\-tls\-cert\-file and \-\-tls\-private\-key\-file parameters of the API server are set to appropriate values. |Compliant |None |
|Make sure that the \-\-client\-ca\-file parameter of the API server is set to an appropriate value. |Compliant |None |
|Make sure that the \-\-etcd\-cafile parameter of the API server is set to an appropriate value. |Compliant |None |
|Make sure that the \-\-encryption\-provider\-config parameter of the API server is set to an appropriate value. |Non\-compliant |None |


<span id=".5o6n5Yi25Zmo566h55CG5Zmo"></span>
### Controller manager


|**Item description** |**VKE** **compliance status** |**Non\-compliance reason** |
|---|---|---|
|Make sure that the \-\-terminated\-pod\-gc\-threshold parameter of the controller manager is set to an appropriate value. |Non\-compliant |VKE uses the community default value of 12500. |
|Make sure that the \-\-profiling parameter of the controller manager is set to false. |Non\-compliant |VKE performs debugging by using performance profiling. |
|Make sure that the \-\-use\-service\-account\-credentials parameter of the controller manager is set to true. |Compliant |None |
|Make sure that the \-\-service\-account\-private\-key\-file parameter of the controller manager is set to an appropriate value. |Compliant |None |
|Make sure that the \-\-root\-ca\-file parameter of the controller manager is set to an appropriate value. |Compliant |None |
|Make sure that the RotateKubeletServerCertificate parameter of the controller manager is set to true. |Compliant |None |
|Make sure that the \-\-bind\-address parameter of the controller manager is set to 127.0.0.1. |Non\-compliant |VKE platform components need to monitor the status and metrics of the controller manager, so VKE binds the controller manager to 0.0.0.0. In addition, starting from Kubernetes v1.17, the listening port of the controller manager API service enforces TLS authentication and encryption, so unauthenticated users cannot retrieve runtime status or metrics through it. |


<span id=".6LCD5bqm5Zmo"></span>
### Scheduler


|**Item description** |**VKE** **compliance status** |**Non\-compliance reason** |
|---|---|---|
|Make sure that the \-\-profiling parameter of the scheduler is set to false. |Non\-compliant |VKE performs debugging by using performance profiling. |
|Make sure that the \-\-bind\-address parameter of the scheduler is set to 127.0.0.1. |Non\-compliant |Add\-ons in VKE need to monitor the status and metrics of the scheduler. Therefore, you need to set the bound address to 0.0.0.0. In addition, for Kubernetes v1.17 or later, the listening port of the scheduler API service requires Transport Layer Security (TLS) authentication and encryption. As a result, unauthenticated users cannot obtain running status and monitoring metrics through it. |


<span id=".ZXRjZC3oioLngrnphY3nva4="></span>
## etcd node configuration


|**Item description** |**VKE** **compliance status** |**Non\-compliance reason** |
|---|---|---|
|Make sure that the \-\-cert\-file and \-\-key\-file parameters of etcd are set correctly. |Compliant |None |
|Make sure that the \-\-client\-cert\-auth parameter of etcd is set to true. |Compliant |None |
|Make sure that the \-\-auto\-tls parameter of etcd is not set to true. |Compliant |None |
|Make sure that the values of the \-\-peer\-cert\-file and \-\-peer\-key\-file parameters for etcd are valid. |Compliant |None |
|Make sure that the \-\-peer\-client\-cert\-auth parameter of etcd is set to true. |Compliant |None |
|Make sure that the \-\-peer\-auto\-tls parameter of etcd is not set to true. |Compliant |None |
|Make sure that etcd uses a single CA. |Compliant |None |


<span id=".5o6n5Yi26Z2i6YWN572u"></span>
## Control plane configuration

<span id=".6Lqr5Lu96aqM6K-B5ZKM5o6I5p2D"></span>
### Authentication and authorization


|**Item description** |**VKE** **compliance status** |**Non\-compliance reason** |
|---|---|---|
|Client certificates cannot be used for user authentication. |Non\-compliant |VKE does not currently support client certificate\-based user authentication. Client authentication is performed through other mechanisms. |


<span id=".5pel5b-X5a6h6K6h"></span>
### Log audit


|**Item description** |**VKE** **compliance status** |**Non\-compliance reason** |
|---|---|---|
|Make sure that a minimal audit policy is created for Kubernetes. |Non\-compliant |Audit logging is a service feature that is disabled by default. |
|Make sure that the Kubernetes audit policy covers key security issues |Non\-compliant |Audit logging is a service feature that is disabled by default. |


<span id=".d29ya2VyLeiKgueCuQ=="></span>
## Worker node

<span id=".d29ya2VyLeiKgueCuemFjee9ruaWh-S7tg=="></span>
### Worker node configuration file


|**Item description** |**VKE** **compliance status** |**Non\-compliance reason** |
|---|---|---|
|Make sure that the permission of the kubelet service file is set to 644 or stricter. |Compliant |None |
|Make sure that the ownership of the kubelet service file is set to root:root. |Compliant |None |
|If the kubeconfig file exists for kube\-proxy, make sure that the permission is set to 644 or lower. |Compliant |None |
|If the kubeconfig file exists for kube\-proxy, make sure that the ownership is set to root:root. |Compliant |None |
|Make sure that the permission value of the \-\-kubeconfig kubelet.conf file of kubelet is set to 644 or lower. |Compliant |None |
|Make sure that the ownership of the \-\-kubeconfig kubelet.conf file for kubelet is set to root:root. |Compliant |None |
|Make sure that the permission on the CA file of kubelet is set to 644 or lower. |Compliant |None |
|Make sure that the ownership of the CA file for kubelet is set to root: root. |Compliant |None |
|Make sure that the permission on the \-\-config configuration file of kubelet is set to 644 or lower. |Compliant |None |
|Make sure that the ownership of the \-\-config configuration file for kubelet is set to root: root. |Compliant |None |


<span id="kubelet"></span>
### Kubelet


|**Item description** |**VKE** **compliance status** |**Non\-compliance reason** |
|---|---|---|
|Make sure that the \-\-anonymous\-auth parameter of kubelet is set to false. |Compliant |None |
|Make sure that the \-\-authorization\-mode parameter of kubelet is not set to AlwaysAllow. |Compliant |None |
|Make sure that the \-\-client\-ca\-file parameter of kubelet is set to an appropriate value. |Compliant |None |
|Check whether the \-\-read\-only\-port parameter of kubelet is set to 0. |Compliant |None |
|Make sure that the \-\-streaming\-connection\-idle\-timeout parameter of kubelet is not set to 0. |Compliant |None |
|Make sure that the \-\-protect\-kernel\-defaults parameter of kubelet is set to true. |Non\-compliant |VKE does not protect the default kernel settings in Kubernetes because customer workloads may require modifications to these settings. |
|Make sure that the \-\-make\-iptables\-util\-chains parameter of kubelet is set to true. |Compliant |None |
|Make sure that the \-\-hostname\-override parameter of kubelet is not specified. |Non\-compliant |VKE does not use the hostname of the host to identify kubelet. Instead, VKE uses \-\-hostname\-override to set the kubelet identity to an appropriate value that maps one\-to\-one with the node name, so neither security analysis nor fully qualified domain name (FQDN) resolution is affected. |
|Make sure that the eventRecordQPS parameter of kubelet is set to an appropriate value. |Non\-compliant |Events are Kubernetes objects stored in etcd. To prevent overloading etcd, events are retained for only one hour. Therefore, they are not a suitable security audit mechanism. Following this control's recommendation to allow unbounded event rates would expose the cluster to unnecessary DoS risks and conflict with the recommended use of the EventRateLimits. Security\-related events that require permanent storage need to be sent to logs. |
|Make sure that the \-\-tls\-cert\-file and \-\-tls\-private\-key\-file parameters of kubelet are set to appropriate values |Compliant |None |
|Make sure that the \-\-rotate\-certificates parameter of kubelet is not set to false |Compliant |None |
|Check whether the RotateKubeletServerCertificate parameter of kubelet is set to true. |Compliant |None |
|Make sure that kubelet uses only strong cipher suites. |Non\-compliant |VKE uses [the default allowed cipher suite of the Go language](https://go.dev/blog/tls-cipher-suites). These cipher suites are considered safe by the Go cryptography team and are also the default cipher suites used by Kubernetes. |


<span id="policy"></span>
## Policy

<span id=".cmJhYy3lkozmnI3liqHotKblj7c="></span>
### RBAC and service account


|**Item description** |**VKE** **compliance status** |**Non\-compliance reason** |
|---|---|---|
|Make sure that the cluster\-admin role is used only when necessary. |Environment\-dependent |None |
|Minimize the access permissions on keys. |Environment\-dependent |None |
|Minimize the use of wildcards in Roles and ClusterRoles. |Environment\-dependent |None |
|Minimize the access permissions used to create pods. |Environment\-dependent |None |
|Make sure that the default service account is not frequently used. |Environment\-dependent |None |
|Make sure that the service account token is mounted only when necessary. |Environment\-dependent |None |


<span id=".cG9kLeWuieWFqOetlueVpQ=="></span>
### Pod security policy


|**Item description** |**VKE** **compliance status** |**Non\-compliance reason** |
|---|---|---|
|Minimize the permissions granted to privileged containers. |Environment\-dependent |None |
|Minimize the permissions granted to containers that intend to share the process ID (PID) namespace of the host. |Environment\-dependent |None |
|Minimize the permissions granted to containers that intend to share the inter\-process communication (IPC) namespace of the host. |Environment\-dependent |None |
|Minimize the permissions granted to containers that intend to share the host network namespace. |Environment\-dependent |None |
|Minimize the permissions granted to containers with allowPrivilegeEscalation enabled. |Environment\-dependent |None |
|Minimize the permissions granted to root containers |Environment\-dependent |None |
|Minimize the permissions granted to containers with the NET_RAW feature. |Environment\-dependent |None |
|Minimize the permissions granted to containers with additional features. |Environment\-dependent |None |
|Minimize the permissions granted to containers with assigned features. |Environment\-dependent |None |


<span id=".572R57uc562W55Wl5ZKMLWNuaQ=="></span>
### Network policy and CNI


|**Item description** |**VKE** **compliance status** |**Non\-compliance reason** |
|---|---|---|
|Make sure that the used CNI supports network policies. |Compliant |None |
|Make sure that network policies are defined for all namespaces. |Environment\-dependent |None |


<span id=".5a-G5paH566h55CG"></span>
### Ciphertext management


|**Item description** |**VKE** **compliance status** |**Non\-compliance reason** |
|---|---|---|
|Ciphertext is preferentially used as files rather than as environment variables. |Environment\-dependent |None |
|Consider external ciphertext storage. |Environment\-dependent |None |


<span id=".5Y-v5ouT5bGV55qE5YeG6K645o6n5Yi2"></span>
### Scalable admission control


|**Item description** |**VKE** c**ompliance Status** |**Non\-compliance reason** |
|---|---|---|
|Use the ImagePolicyWebhook admission controller to configure image sources. |Environment\-dependent |None |


<span id=".5bi46KeE562W55Wl"></span>
### General policy


|**Item description** |**VKE** c**ompliance status** |**Non\-compliance reason** |
|---|---|---|
|Namespaces are used to create management boundaries between resources. |Environment\-dependent |None |
|Make sure that the seccomp configuration file is set to docker/default in the pod definition. |Environment\-dependent |None |
|Apply security context to your pods and containers. |Environment\-dependent |None |
|Do not use the default namespace |Environment\-dependent |None |
