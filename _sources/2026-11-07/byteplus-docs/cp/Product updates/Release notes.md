---
title: "Release notes"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Release_notes"
---

This article introduces the latest updates to CP\-related features. CP is a Global\-level service. New features are released in all regions. Welcome to experience.

<span id="hzDivJ2F"></span>
## August 2026


|Feature name |Description |Region |Related documentation |
|---|---|---|---|
|A custom private resource pool supports selecting a Kubernetes version |When creating a custom private build resource pool, you can select a Kubernetes version. The platform automatically deploys matching build Agent with pipeline engine (Tekton) addons according to the selected version. |All |[Create a custom private resource pool](https://docs.byteplus.com/en/docs/cp/Create_a_custom_private_resource_pool?lang=en) |


<span id="Fx66N7B4"></span>
## June 2026


|Feature name |Description |Region |Related documentation |
|---|---|---|---|
|Java managed app supports OpenJDK 21 |When creating a Java Managed App, the Java runtime Version now includes the OpenJDK 21 option. Supports JAR and WAR package deployment methods, and supports both Kubernetes Container deployment and ECS Hosts deployment scenarios. |All |* [Create and deploy managed app (JAR/WAR)](https://docs.byteplus.com/en/docs/cp/Create_and_deploy_managed_apps_JAR_WAR?lang=en)<br><br>* [Create and deploy managed app (Java technology stack)](https://docs.byteplus.com/en/docs/cp/Create_and_deploy_managed_applications_ECS?lang=en) |
|Image source Webhook trigger |New built\-in placeholders for the image source Webhook trigger include the complete image address, repository domain name, namespace, OCI artifact repository, image tag, and more. These placeholders can automatically inject information about the image being pushed when triggering the pipeline, and support configuring multiple dynamic variables. |All |[Image source Webhook trigger](https://docs.byteplus.com/en/docs/cp/Trigger_mirror_source_webhook?lang=en) |


<span id="WjBRIGlr"></span>
## April 2026


|Feature name |Description |Region |Related documentation |
|---|---|---|---|
|Create pipelines via YAML |Support creating pipelines via YAML, facilitating review, audit, gray release reuse, and cross\-project migration. |All |[YAML pipeline](https://docs.byteplus.com/en/docs/cp/YAML_pipeline) |
|Start script supports switching execution user |Support selecting the user at the operating system level to execute the deploy command on the host, for example, `root`, `admin`, and more. Different execution users can be granted different resource management permissions. In the deployment phase, a specific execution user can be flexibly specified to ensure the security and compliance of the deployment process. |All |[Create and deploy managed application (non-Java technology stack)](https://docs.byteplus.com/en/docs/cp/Create_and_deploy_managed_applications_non-Java_stack) |
|Pipeline built\-in task<br><br> |Support batch operation and maintenance tasks (such as remote command execution, file distribution, and more) on ECS cloud servers in the pipeline, achieving automated integration of deployment and operation and maintenance processes. |All |[ECS operations](https://docs.byteplus.com/en/docs/cp/ECS_operations_and_maintenance) |
||Supports building container images via Dockerfile and pushing them to the Container Registry (CR) or a custom image repository to automate delivery from code to container images. ||[Build and push images](https://docs.byteplus.com/en/docs/cp/Build_and_push_images) |
||Supports one\-click switching in multi\-cloud active\-active scenarios when third\-party cloud failure occurs, covering key steps such as app expansion, database switching, and traffic switching, helping users quickly implement multi\-cloud disaster recovery solutions and reduce business interruption risk. ||[Cloud disaster recovery](https://docs.byteplus.com/en/docs/cp/Multi-cloud_disaster_recovery) |
||Supports full\-process actions for ECS instance creation/deletion, custom image creation, vulnerability scanning, image cross\-region copy, and image sharing. These can be used with pipeline templates to achieve automatic building and distribution of ECS images. ||[ECS building images](https://docs.byteplus.com/en/docs/cp/Build_ECS_images) |
||Supports one\-click deployment or update of the AgentKit Runtime environment in the pipeline, and integrates AI Agent apps into the CI/CD automated delivery process. ||[AgentKit runtime update](https://docs.byteplus.com/en/docs/cp/AgentKit_Runtime_update) |
|Container\-type managed app |K8s containerized deployment solution centered on Apps, supporting multiple artifact types such as Java (JAR/WAR), container image, and more, enabling one\-click deployment of Apps to container clusters and full life cycle management. |All |[Managed app (K8s)](https://docs.byteplus.com/en/docs/cp/Managed_applications_K8s) |
|Host type managed application |App\-centric ECS host deployment solution, supporting artifact types such as Java (JAR/WAR) packages, provides both full release and batch release policies, enables one\-click deployment of apps to ECS cloud servers, and supports scaling, change management, and access management. |All |[Managed application (ECS)](https://docs.byteplus.com/en/docs/cp/Hosted_applications_ECS) |
|Helm application |Helm application is an instance deployed and managed by the Helm tool, packaged and configured based on Helm Chart, and runs in the K8s cluster. Helm application can simplify K8s application operations and maintenance (no need to manually operate YAML), supporting application lifecycle management. |All |[Creating Helm applications](https://docs.byteplus.com/en/docs/cp/Create_Helm_application) |
|Access VKE cluster |Access VKE cluster as the target resources for pipeline and application delivery deployment. |All |[Integrate VKE cluster](https://docs.byteplus.com/en/docs/cp/Integrate_VKE_cluster) |
|Build resource pool |Provides a dedicated compile and build runtime environment for pipelines, meeting security compliance, network isolation, and high performance build requirements. |All |* [Create a private build resource pool for VKE](https://docs.byteplus.com/en/docs/cp/Create_a_VKE_private_build_resource_pool)<br><br>* [Create custom private resource pools](https://docs.byteplus.com/en/docs/cp/Create_a_custom_private_resource_pool) |
|Host group |Supports connecting ECS instances or free hosts to the CP platform, enabling batch deployment and management at the host level. |All |* [Add ECS host group](https://docs.byteplus.com/en/docs/cp/Add_ECS_host_group)<br><br>* [Add custom host group](https://docs.byteplus.com/en/docs/cp/Add_owned_host_group) |


<span id="wTRkfc79"></span>
## March 2026


|Feature name |Description |Region |Related documentation |
|---|---|---|---|
|Image builds pushed to Container Registry support Nydus conversion |After turning on the Image Nydus conversion feature, the Target Image pushed to the Container Registry will automatically generate an accelerated Nydus\-format Image replica. Using the accelerated image in the Nydus format can effectively reduce container startup time and improve service development efficiency. |All |[Build images and push to the Container Registry Service](https://docs.byteplus.com/en/docs/cp/Building_and_pushing_images_to_the_image_repository_service) |
|Added AgentKit deployment and update tasks |Pass add AgentKit Runtime Deploy OR Update task in pipeline orchestration, Complete AgentKit Runtime Deploy and Update. |All |* [AgentKit runtime deployment](https://docs.byteplus.com/en/docs/cp/AgentKit_Runtime_deployment)<br><br>* [AgentKit runtime update](https://docs.byteplus.com/en/docs/cp/AgentKit_Runtime_update) |


<span id="oU65gSMK"></span>
## September 2025

<span id=".XzIwMjTlubQxMeaciA=="></span>
##
