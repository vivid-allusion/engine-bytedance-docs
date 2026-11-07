---
title: "Configure cross-realm trust between Kerberos clusters"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Configure_cross-realm_trust_between_Kerberos_clusters"
---

To enable service access between two Kerberos clusters, you must configure cross\-realm trust between the Kerberos clusters (Cross Realm). In Volcano Engine E\-MapReduce (EMR), if you already have two Kerberos clusters, A and B, and want to access services in cluster B from cluster A across realms, follow these steps.

<span id="43325747"></span>
## Procedure


1. Obtain Realm and FQDN information.

   Log in to the command line interface of the Master nodes of clusters A and B, and obtain the Realm and FQDN information for clusters A and B from `/etc/krb5.conf`, then record them. The format of the Realm information is xxx.EMR.COM. For login methods, see [Log in to the cluster](https://docs.byteplus.com/docs/E-MapReduce/104404).

2. Add the principal for cross\-realm authentication.

   1. Log in to the command line interface of the Master node of cluster A, and execute the following command as the `root` user:

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Please confirm the E\-MapReduce release version you are using. Different release versions use different commands.      </div>
      

      ```bash
      # For EMR-3.8.0 and later versions, use the kadmin.local command. As shown below:
      kadmin.local -q "addprinc -pw <新建一个自定义密码> krbtgt/<集群 B 的 Realm>@<集群 A 的 Realm>"
      
      # For versions earlier than EMR-3.8.0, use the kadmin command. As shown below:
      kadmin -q "addprinc -pw <新建一个自定义密码> krbtgt/<集群 B 的 Realm>@<集群 A 的 Realm>"
      ```
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Content enclosed in angle brackets (“<\>”), including the brackets themselves, must be replaced with the actual values according to your scenario.      </div>
      

   2. Log in to the command line interface of the Master node of cluster B, and execute the same command as the root user (no need to change the order of the Realms in the command), as shown below:

      ```bash
      # For EMR-3.8.0 and later versions, use the kadmin.local command. As shown below:
      kadmin.local -q "addprinc -pw <新建一个自定义密码> krbtgt/<集群 B 的 Realm>@<集群 A 的 Realm>"
      
      # For versions earlier than EMR-3.8.0, use the kadmin command. As shown below:
      kadmin -q "addprinc -pw <新建一个自定义密码> krbtgt/<集群 B 的 Realm>@<集群 A 的 Realm>"
      ```
      

3. Configure krb5.conf for cluster A and restart the KDC service of cluster A.

   Log in to the command line interface of the Master node of cluster A, edit the `/etc/krb5.conf` configuration file, and modify the following content:

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Content enclosed in angle brackets (“<\>”), including the brackets themselves, must be replaced with the actual values according to your scenario.   </div>
   

   1. Add an entry under `[realms]`:

      ```plain
      <集群 B 的 Realm> = {
          kdc = <集群 B 的 Master 节点的 FQDN>:88
      }
      ```
      

   2. Add `[capaths]`:

      ```plain
      [capaths]
          <集群 A 的 Realm> = {
              <集群 B 的 Realm> = .
          }
          <集群 B 的 Realm> = {
              <集群 A 的 Realm> = .
          }
      ```
      

   3. Add `[domain_realm]`:

      ```plain
      [domain_realm]
          <集群 A 的第一个 Master 节点的 FQDN> = <集群 A 的 Realm>
          <集群 A 的第二个 Master 节点的 FQDN> = <集群 A 的 Realm>
          ...
          <集群 A 的第一个 Core 节点的 FQDN> = <集群 A 的 Realm>
          <集群 A 的第二个 Core 节点的 FQDN> = <集群 A 的 Realm>
          ...
          <集群 B 的第一个 Master 节点的 FQDN> = <集群 B 的 Realm>
          <集群 B 的第二个 Master 节点的 FQDN> = <集群 B 的 Realm>
          ...
          <集群 B 的第一个 Core 节点的 FQDN> = <集群 B 的 Realm>
          <集群 B 的第二个 Core 节点的 FQDN> = <集群 B 的 Realm>
          ...
      ```
      

   4. After completing the configuration, restart the KDC.

4. Verify the operation.

   You can log in to a node in cluster A and access services in cluster B. For detailed procedures, refer to the documentation: [Use a Kerberos-authenticated cluster](https://docs.byteplus.com/docs/E-MapReduce/109309).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When accessing services on a remote Kerberos cluster, you must use the FQDN to connect to nodes on the remote Kerberos cluster.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the service being accessed in cluster B is Kafka, you must add a configuration entry to the Kafka service in cluster B and then restart the Kafka service.   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The additional configuration items are as follows (Note: The content enclosed in angle brackets ("<\>")—including the angle brackets themselves—must be replaced with the actual values according to your specific scenario):   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Configuration item: <code>sasl.kerberos.principal.to.local.rules</code>   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Value:   </div>
   

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For versions EMR\-3.8.0 and later (inclusive), configure as: <code>RULE:[2:$1@$0](.*@<源集群（集群 A）的 Realm>)s/@.*//,DEFAULT</code>   </div>
   

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For versions earlier than EMR\-3.8.0 (exclusive), configure as: <code>RULE:[1:$1@$0](.*@<源集群（集群 A）的 Realm>)s/@.*//,DEFAULT</code>   </div>
