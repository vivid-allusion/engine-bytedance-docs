---
title: "ExternalName"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/ExternalName"
---

ExternalName maps an internal service name to an external domain name within a cluster, allowing Pods in the cluster to access the external domain name using the Service name. This topic describes how to configure a service of the ExternalName type.

<span id="2SsAQesR"></span>
## Background

When you create a Service of the ExternalName type in a cluster, Kubernetes does not assign a ClusterIP to the Service or create Endpoints. Instead, Kubernetes uses CoreDNS to return a CNAME record that maps the service name to an external DNS domain name. Workloads inside the cluster can access external services using the Service name (for example, `service-demo.default.svc.cluster.local`), without hardcoding the external domain name in the application.

<span id="0v7Z3D0k"></span>
## Procedure

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before configuring an ExternalName Service using the kubectl command\-line interface, ensure that the following conditions are met:</div>



* <div data-tips="true" data-tips-type="tip">The kubectl tool has been installed on your on\-premises computer. For details, see <a href="https://kubernetes.io/docs/tasks/tools/">Installing and configuring kubectl</a>.</div>


* <div data-tips="true" data-tips-type="tip">The target cluster has been connected through kubectl. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster">Connecting to clusters</a>.</div>


1. Create a YAML file for the service. The following `external-service-demo.yaml` file serves as an example:

   ```YAML
   apiVersion: v1
   kind: Service
   metadata:
     name: external-service-demo     # The name of the service.
     namespace: default              # The namespace to which the service belongs.
   spec:
     type: ExternalName              # The Service type is set to ExternalName.
     externalName: byteplus.com    # The external domain name to map to outside the cluster. It must be a valid DNS name. IP addresses are not allowed.
   ```
   

2. Run the following command to create a Service.

   ```Bash
   kubectl apply -f external-service-demo.yaml
   ```
   


<span id="nZkFqtZ6"></span>
## Validate results

<span id="yOEM1j5D"></span>
### Viewing services

The service you created can be found in the service list.

<span id="eCgTWDLH"></span>
### Testing the connections to services

After the Service is created, you can access the external domain name using the Service name. You can run the following command inside the Pod to validate domain name resolution and connectivity.

```Bash
nslookup external-service-demo
```


The expected resolution results include a CNAME record for `byteplus.com`, as well as the resolved real IP address, indicating that the ExternalName mapping has taken effect.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_76cfc2096fcb3ac0ecc47d05f5550fd5.png) </span>
