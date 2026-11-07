---
title: "Pull and push Helm charts"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/push-and-pull-Helm-charts-in-an-enterprise-instance"
---

CR Standard Edition instances support Helm chart hosting, meeting your requirements for the hosting and distribution of cloud\-native applications. You can manage container images and Helm charts simultaneously in the same OCI artifact repository, enabling the combined use of both within your business projects.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An OCI artifact repository has been created. For detailed operations, see [Creating OCI artifact repositories](https://docs.byteplus.com/en/docs/cr/create-an-OCI-repository).

* The Helm 3 client has been installed. For more information, visit the [Helm official website](https://helm.sh/).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Currently, the Helm 3.13.0 and 3.13.1 client versions have known defects. Use other versions instead.   </div>
   

* Enable OCI support: `export HELM_EXPERIMENTAL_OCI=1`.


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When you upload artifacts, do not set the [Chart version] and [Image tag] to the same value to avoid overwriting and loss of historical data caused by duplicate identifiers.</div>


Example information:


|Username |UserId |Standard Edition instance |Region of the CR instance |Namespace |OCI Artifact Repository |
|---|---|---|---|---|---|
|v\*\* |1007\*\*\* |instance\-a |China (Beijing) |space\-a |mysql |


<span id=".5L2_55SoaGVsbSAzLjfku6XkuIvniYjmnKzmjqjpgIHmi4nlj5ZDaGFydA=="></span>
## Pull and push a chart by using a Helm version earlier than 3.7

<span id=".5ouJ5Y-WQ2hhcnQ="></span>
### Pull a chart

For user `v** Id:1007***`, as an example, pull the `mysql 2021-03` version chart in namespace `space-a` under Standard Edition instance `instance-a`.


1. Run the following command to log in to the CR instance.

   ```Plain Text
   helm registry login --username=<Account name>@<UserID> <Instance name>-cn-<Region>.cr.volces.com
   ```
   

   Example:

   ```Plain Text
   helm registry login --username=v**@1007*** instance-a-cn-beijing.cr.volces.com
   ```
   

2. Execute the following command to pull the chart.

   ```Plain Text
   helm chart pull <Instance name>-cn-<Region>.cr.volces.com/<Namespace>/<Chart name>:[Chart version]
   ```
   

   Example:

   ```Plain Text
   helm chart pull instance-a-cn-beijing.cr.volces.com/space-a/mysql:2021-03
   ```
   


<span id=".5o6o6YCBQ2hhcnQ="></span>
### Push a chart

For user `v** Id:1007***`, as an example, push the `mysql 2021-03` version chart to namespace `space-a` under Standard Edition instance `instance-a`.


1. Run the following command to log in to the CR instance.

   ```Plain Text
   helm registry login --username=<Account name>@<UserID> <Instance name>-cn-<Region>.cr.volces.com
   ```
   

   Example:

   ```Plain Text
   helm registry login --username=v**@1007*** instance-a-cn-beijing.cr.volces.com
   ```
   

2. Execute the following command to save the chart.

   ```Plain Text
   helm chart save [Chart name] <Instance name>-cn-<Region>.cr.volces.com/<Namespace>/<Chart name>:[Chart version]
   ```
   

   Example:

   ```Plain Text
   helm chart save mysql instance-a-cn-beijing.cr.volces.com/space-a/mysql:2021-03
   ```
   

3. Execute the following command to push the chart to the Container Registry instance.

   ```Plain Text
   helm chart push <Instance name>-cn-<Region>.cr.volces.com/<Namespace>/<Chart name>:[Chart version]
   ```
   

   Example:

   ```Plain Text
   helm chart push instance-a-cn-beijing.cr.volces.com/space-a/mysql:2021-03
   ```
   


<span id=".5L2_55SoaGVsbSAzLjcg5Lul5ZCO54mI5pys5o6o6YCB5ouJ5Y-WQ2hhcnQ="></span>
## Pull and push a chart by using a Helm version later than 3.7

<span id=".5ouJ5Y-WQ2hhcnQ="></span>
### Pull a chart

For user `v** Id:1007***`, as an example, pull the `mysql 2021-03` version chart in namespace `space-a` under Standard Edition instance `instance-a`.


1. Run the following command to log in to the CR instance.

   ```Plain Text
   helm registry login --username=<Account name>@<UserID> <Instance name>-cn-<Region>.cr.volces.com
   ```
   

   Example:

   ```Plain Text
   helm registry login --username=v**@1007*** instance-a-cn-beijing.cr.volces.com
   ```
   

2. Execute the following command to pull the chart.

   ```Plain Text
   helm pull oci://<Instance name>-cn-<Region>.cr.volces.com/<Namespace>/<Chart name> --version [Chart version]
   ```
   

   Example:

   ```Plain Text
   helm pull oci://instance-a-cn-beijing.cr.volces.com/space-a/mysql --version 2021-03
   ```
   


<span id=".5o6o6YCBQ2hhcnQ="></span>
### Push a chart

For user `v** Id:1007***`, as an example, push the `mysql 2021-03` version chart to namespace `space-a` under Standard Edition instance `instance-a`.


1. Run the following command to log in to the CR instance.

   ```Plain Text
   helm registry login --username=<Account name>@<UserID> <Instance name>-cn-<Region>.cr.volces.com
   ```
   

   Example:

   ```Plain Text
   helm registry login --username=v**@1007*** instance-a-cn-beijing.cr.volces.com
   ```
   

2. Execute the following command to package the chart.

   ```Plain Text
   helm package [Chart name] --version [Chart version]
   ```
   

   Example:

   ```Plain Text
   helm package mysql --version 2021-03
   ```
   

3. Execute the following command to push the chart to the Container Registry instance.

   ```Plain Text
   helm push [[Chart name]-[Chart version].tgz] oci://<<Instance name>-cn-<Region>.cr.volces.com/<Namespace>
   ```
   

   Example:

   ```Plain Text
   helm push [mysql-2021-03.tgz] oci://instance-a-cn-beijing.cr.volces.com/space-a
   ```
