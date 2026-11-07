---
title: "Collecting VCI container logs via a sidecar"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Collecting-VCI-container-logs-using-a-sidecar"
---

VCI supports collecting container logs by using a sidecar. This topic describes how to deploy a container log collection Agent using the sidecar method to collect standard output logs and file logs of containers on VCI.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A host group has been created in TLS. For details, see [Creating host groups (host identification)](https://docs.byteplus.com/en/docs/tls/Create_a_label-based_host_group).

* A **log project** and **log topic** have been created in TLS. For detailed operations, see [Log projects](https://docs.byteplus.com/en/docs/tls/Managing_projects) and [Log topics](https://docs.byteplus.com/en/docs/tls/Managing_topics).

* Log collection configuration has been created in TLS and associated with the host group created above. For detailed instructions, see [Collecting container logs](https://docs.byteplus.com/en/docs/tls/collect_container_logs).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

This topic uses LogCollector, the log collection add\-on provided by BytePlus TLS, as an example sidecar container. If you have your own log collection add\-on, you can configure the Sidecar container yourself.

For details on configurable annotations for collecting container logs using the Sidecar method, see [Pod annotations](https://docs.byteplus.com/en/docs/vke/VCI-Pod-annotations).


1. Create a configuration file for the sidecar container. The following `logcollector-config.yaml` file provides an example:

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Replace the placeholder variables (<code>${placeholder}</code>) with your actual information based on the parameter table below and the comments in the YAML file.   </div>
   

   ```yaml
   apiVersion: v1
   kind: ConfigMap
   metadata:
     name: logcollector-config
     namespace: ${namespace}
   data:
     filebeat.yml: |
       filebeat:
         is_sidecar: true
   
       output.tls:
         endpoint: ${volc_tls_endpoint}
         region: ${volc_region}
         secret_id: ${your_ak}
         secret_key: ${your_sk}
         label: ${your_labels}
   
       # The following code snippet is the log output configuration.
       # For details, visit https://www.elastic.co/guide/en/beats/filebeat/7.17/configuration-logging.html.
       logging.level: info
       logging.to_files: true  
       logging.files:
         name: filebeat
         keepfiles: 7
         permissions: 0644
   ```
   

   Parameter descriptions are as follows:

   
   |Variable |Example |Description |
   |---|---|---|
   |namespace |default |Namespace where the sidecar container is located. |
   |endpoint |https://tls\-cn\-beijing.ivolces.com |The TLS service address. For a list of supported regions and corresponding TLS service address, see [Service addresses](https://docs.byteplus.com/en/docs/tls/endpoint). |
   |region |cn\-beijing |The region where the container logs are collected. For details, see [Regions and availability zones](https://docs.byteplus.com/en/docs/vke/VCI-Regions-and-Availability-Zones). |
   |secret_id |AK\*\*\*\*\*\*\*\* |The access key ID of the BytePlus root user or IAM user. For information on how to obtain one, see [Access key management](https://docs.byteplus.com/en/docs/IAM/about-access-keys). |
   |secret_key |TUdZ\*\*\*\*\*\*\*\* |The secret access key of the BytePlus root user or IAM user. For information on how to obtain one, see [Access key management](https://docs.byteplus.com/en/docs/IAM/about-access-keys). |
   |label |http_module |The custom identifier of the host. It must be consistent with the custom identifier of the host group created in the **Prerequisites** section. |
   

2. Run the following command to create the configuration file for the sidecar container.

   ```bash
   kubectl apply -f logcollector-config.yaml
   ```
   

3. Create a YAML manifest for a VCI pod that contains the sidecar container.

   The following are two YAML examples:

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Replace the parameter values with your actual information according to the comments in the YAML file.   </div>
   

   * When creating the VCI pod, mount `csi-driver` and collect the standard output logs of the application container using the sidecar. The following `sidecar-vci-pod-demo.yaml` file provides an example:

      ```yaml
      apiVersion: v1
      kind: Pod
      metadata:
        name: sidecar-vci-pod-demo   # VCI pod name.
        namespace: default   # Namespace to which the VCI pod belongs.
        annotations:
          vke.volcengine.com/burst-to-vci: enforce   # Forced scheduling to VCI.
      spec:
        containers:
          - name: c1    # Application container name.
            image: nginx:1.14.2    # Container image address and tag. Replace the value with your actual information.
            args:   # The application container prints the current time to the standard output log every second.
              - /bin/sh
              - -c
              - >
                i=0;
                while true;
                do
                  echo "$i: $(date)";
                  i=$((i+1));
                  sleep 1;
                done
            volumeMounts:
              - name: stdlog-volume    # Name of the volume for storing standard output logs of the application container.
                mountPath: /var/log    # Access path for standard output logs of the application container.
          - name: logcollector    # Sidecar container name.
            image: ${logcollector-image}  # Sidecar container image. That is, the LogCollector image address provided by TLS. For details, see https://docs.byteplus.com/en/docs/6470/190394#logcollector-image-address.
            imagePullPolicy: Always
            args:
              - /usr/local/container/filebeat-7.12.0/filebeat
              - -c
              - /usr/local/container/filebeat-7.12.0/etc/filebeat.yml
            livenessProbe:
              initialDelaySeconds: 10
              periodSeconds: 10
              exec:
                command:
                  - sh
                  - -c
                  - |
                    filebeat_num=`ps -ef 2>/dev/null | grep "filebeat" | grep -v "grep" | wc -l`
                    if [ $filebeat_num -eq 0 ]; then
                      return 1
                    fi
            volumeMounts:
              - name: logcollector-config
                mountPath: /usr/local/container/filebeat-7.12.0/etc/
                readOnly: true
              - name: stdlog-volume    # Name of the volume used by the sidecar container to access standard output of the application container.
                mountPath: /var/log    # Access path inside the sidecar container to access standard output of the application container.
              - name: data
                mountPath: /usr/local/container/filebeat-7.12.0/data
            env:
              - name: "LOG_COLLECTOR_ENV_TAGS"
                value: "__pod_name__|__pod_ip__|__namespace__|__node_name__|__node_ip__"
              - name: "__pod_name__"
                valueFrom:
                  fieldRef:
                    fieldPath: metadata.name
              - name: "__pod_ip__"
                valueFrom:
                  fieldRef:
                    fieldPath: status.podIP
              - name: "__namespace__"
                valueFrom:
                  fieldRef:
                    fieldPath: metadata.namespace
              - name: MAX_MEM
                valueFrom:
                 resourceFieldRef:
                   containerName: logcollector
                   resource: limits.memory
        volumes:    # Shared volume definition for collecting container file logs.
          - name: logcollector-config    # Name of the sidecar container configuration file ( the file created in Step 1).
            configMap:
              defaultMode: 420
              name: logcollector-config
          - name: stdlog-volume    # Name of the volume used by the sidecar container to access standard output of the application container.
            csi:
              driver: stdlog.csi.volcengine.com
          - name: data
            emptyDir: { }
      ```
      

   * When creating the VCI pod, mount `empty-dir` and collect the file logs of the application container using the sidecar. The following `sidecar-vci-pod-demo.yaml` file provides an example:

      ```yaml
      apiVersion: v1
      kind: Pod
      metadata:
        name: sidecar-vci-pod-demo    # VCI pod name.
        namespace: default    # Namespace to which the VCI pod belongs.
        annotations:
          vke.volcengine.com/burst-to-vci: enforce    # Forced scheduling to VCI.
      spec:
        containers:
          - name: c1    # Name of the application container.
            image: nginx:1.14.2    # Container image address and tag. Replace the value with your actual information.
            args:
              - /bin/sh
              - -c
              - >
                i=0;
                while true;
                do
                  echo "$i: $(date)" >> /var/log/foo.log;
                  i=$((i+1));
                  sleep 1;
                done
            volumeMounts:
              - name: ${emptydir-name}    # Name of the mount volume for file logs of the application container.
                mountPath: /var/log    # Mount path for the volume for file logs.
          - name: logcollector    # Sidecar container name.
            image: ${logcollector-image}    # Sidecar container image. That is, the LogCollector image address provided by TLS. For details, see https://docs.byteplus.com/en/docs/6470/190394#logcollector-image-address.
            imagePullPolicy: Always
            args:
              - /usr/local/container/filebeat-7.12.0/filebeat
              - -c
              - /usr/local/container/filebeat-7.12.0/etc/filebeat.yml
            livenessProbe:
              initialDelaySeconds: 10
              periodSeconds: 10
              exec:
                command:
                  - sh
                  - -c
                  - |
                    filebeat_num=`ps -ef 2>/dev/null | grep "filebeat" | grep -v "grep" | wc -l`
                    if [ $filebeat_num -eq 0 ]; then
                      return 1
                    fi
            volumeMounts:
              - name: logcollector-config
                mountPath: /usr/local/container/filebeat-7.12.0/etc/
                readOnly: true
              - name: ${emptydir-name}    # Name of the volume used by the sidecar container to access log files of the application container.
                mountPath: /var/log    # Access path inside the sidecar container for the volume for storing logs of the application container.
              - name: data
                mountPath: /usr/local/container/filebeat-7.12.0/data
            env:
              - name: "LOG_COLLECTOR_ENV_TAGS"
                value: "__pod_name__|__pod_ip__|__namespace__|__node_name__|__node_ip__"
              - name: "__pod_name__"
                valueFrom:
                  fieldRef:
                    fieldPath: metadata.name
              - name: "__pod_ip__"
                valueFrom:
                  fieldRef:
                    fieldPath: status.podIP
              - name: "__namespace__"
                valueFrom:
                  fieldRef:
                    fieldPath: metadata.namespace
              - name: MAX_MEM
                valueFrom:
                 resourceFieldRef:
                   containerName: logcollector
                   resource: limits.memory
        volumes:    # Shared volume definition for collecting container file logs.
          - name: logcollector-config    # Name of the sidecar container configuration file ( the file created in Step 1).
            configMap:
              defaultMode: 420
              name: logcollector-config
          - name: ${emptydir-name}    # Name of the volume used by the sidecar container to access log files of the application container.
            emptyDir: { }
          - name: data
            emptyDir: { }
      ```
      

4. Execute the following command to create the VCI pod.

   ```bash
   kubectl apply -f sidecar-vci-pod-demo.yaml
   ```
   

5. Query pod information to verify whether the pod was created successfully.

   ```bash
   kubectl get pods -l app=sidecar-vci-pod-demo
   ```
   

   The expected response is as follows:

   ```bash
   NAME                   READY   STATUS    RESTARTS   AGE
   sidecar-vci-pod-demo   1/1     Running   0          32m
   ```
   

6. Find the target VCI cluster in the [VKE console](https://console.byteplus.com/vke) and view the VCI container logs. For detailed instructions, see [Viewing container logs](https://docs.byteplus.com/en/docs/vke/Collecting-container-logs).
