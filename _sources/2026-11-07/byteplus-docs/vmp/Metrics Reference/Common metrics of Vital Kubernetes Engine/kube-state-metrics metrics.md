---
title: "kube-state-metrics metrics"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Common-metrics-of-kube-state-metrics"
---

kube\-state\-metrics listens to the Kubernetes API server and generates metrics about the status of different resources. It is used to obtain metrics of various resource objects in the Kubernetes cluster, such as Deployments, DaemonSets, Nodes, and Pods. This topic describes the common metrics of kube\-state\-metrics.

Vital Managed Service for Prometheus (VMP) classifies the metrics reported by VKE clusters into the following types: **basic metrics**, **other metrics**, and **custom metrics**. Billing methods vary based on different metric types. 

<span id="s5iEII3w"></span>
## Basic metrics


|Metric name |Metric type |
|---|---|
|kube_replicaset_status_replicas |Basic metric |
|kube_replicaset_status_ready_replicas |Basic metric |
|kube_replicaset_status_observed_generation |Basic metric |
|kube_replicaset_status_fully_labeled_replicas |Basic metric |
|kube_replicaset_spec_replicas |Basic metric |
|kube_replicaset_owner |Basic metric |
|kube_replicaset_labels |Basic metric |
|kube_pod_status_reason |Basic metric |
|kube_pod_status_ready |Basic metric |
|kube_pod_status_phase |Basic metric |
|kube_pod_owner |Basic metric |
|kube_pod_labels |Basic metric |
|kube_pod_info |Basic metric |
|kube_pod_created |Basic metric |
|kube_pod_container_status_waiting_reason |Basic metric |
|kube_pod_container_status_waiting |Basic metric |
|kube_pod_container_status_terminated_reason |Basic metric |
|kube_pod_container_status_terminated |Basic metric |
|kube_pod_container_status_running |Basic metric |
|kube_pod_container_status_restarts_total |Basic metric |
|kube_pod_container_status_ready |Basic metric |
|kube_pod_container_status_last_terminated_reason |Basic metric |
|kube_pod_container_resource_requests |Basic metric |
|kube_pod_container_resource_limits |Basic metric |
|kube_pod_container_info |Basic metric |
|kube_persistentvolumeclaim_status_phase |Basic metric |
|kube_persistentvolumeclaim_status_condition |Basic metric |
|kube_persistentvolumeclaim_labels |Basic metric |
|kube_persistentvolume_status_phase |Basic metric |
|kube_persistentvolume_labels |Basic metric |
|kube_persistentvolume_capacity_bytes |Basic metric |
|kube_node_status_condition |Basic metric |
|kube_node_status_capacity |Basic metric |
|kube_node_status_allocatable |Basic metric |
|kube_node_spec_unschedulable |Basic metric |
|kube_node_spec_taint |Basic metric |
|kube_node_labels |Basic metric |
|kube_node_info |Basic metric |
|kube_namespace_labels |Basic metric |
|kube_deployment_status_replicas_updated |Basic metric |
|kube_deployment_status_replicas_unavailable |Basic metric |
|kube_deployment_status_replicas_ready |Basic metric |
|kube_deployment_status_replicas_available |Basic metric |
|kube_deployment_status_replicas |Basic metric |
|kube_deployment_status_condition |Basic metric |
|kube_deployment_spec_replicas |Basic metric |
|kube_deployment_labels |Basic metric |
|kube_deployment_created |Basic metric |
|kube_daemonset_status_updated_number_scheduled |Basic metric |
|kube_daemonset_status_number_unavailable |Basic metric |
|kube_daemonset_status_number_ready |Basic metric |
|kube_daemonset_status_number_misscheduled |Basic metric |
|kube_daemonset_status_number_available |Basic metric |
|kube_daemonset_status_desired_number_scheduled |Basic metric |
|kube_daemonset_status_current_number_scheduled |Basic metric |
|kube_daemonset_labels |Basic metric |
|kube_daemonset_created |Basic metric |
|kube_statefulset_status_replicas_ready |Basic metric |
|kube_statefulset_status_replicas_available |Basic metric |
|kube_statefulset_created |Basic metric |
|kube_statefulset_replicas |Basic metric |
|kube_statefulset_status_replicas |Basic metric |
|kube_statefulset_status_replicas_updated |Basic metric |
|kube_horizontalpodautoscaler_info |Basic metric |
|kube_horizontalpodautoscaler_metadata_generation |Basic metric |
|kube_horizontalpodautoscaler_spec_max_replicas |Basic metric |
|kube_horizontalpodautoscaler_spec_min_replicas |Basic metric |
|kube_horizontalpodautoscaler_spec_target_metric |Basic metric |
|kube_horizontalpodautoscaler_status_condition |Basic metric |
|kube_horizontalpodautoscaler_status_current_replicas |Basic metric |
|kube_horizontalpodautoscaler_status_desired_replicas |Basic metric |
|kube_horizontalpodautoscaler_status_target_metric |Basic metric |
|kube_horizontalpodautoscaler_annotations |Basic metric |
|kube_horizontalpodautoscaler_labels |Basic metric |


<span id="lMjPnavx"></span>
## Other metrics


|Metric name |Metric type |
|---|---|
|storage_operation_status_count |Other metrics |
|serviceaccount_valid_tokens_total |Other metrics |
|serviceaccount_stale_tokens_total |Other metrics |
|serviceaccount_legacy_tokens_total |Other metrics |
|kube_validatingwebhookconfiguration_metadata_resource_version |Other metrics |
|kube_validatingwebhookconfiguration_info |Other metrics |
|kube_validatingwebhookconfiguration_created |Other metrics |
|kube_service_status_load_balancer_ingress |Other metrics |
|kube_service_spec_type |Other metrics |
|kube_service_labels |Other metrics |
|kube_service_info |Other metrics |
|kube_service_created |Other metrics |
|kube_service_annotations |Other metrics |
|kube_secret_type |Other metrics |
|kube_secret_metadata_resource_version |Other metrics |
|kube_secret_labels |Other metrics |
|kube_secret_info |Other metrics |
|kube_secret_created |Other metrics |
|kube_secret_annotations |Other metrics |
|kube_replicaset_metadata_generation |Other metrics |
|kube_replicaset_created |Other metrics |
|kube_replicaset_annotations |Other metrics |
|kube_poddisruptionbudget_status_pod_disruptions_allowed |Other metrics |
|kube_poddisruptionbudget_status_observed_generation |Other metrics |
|kube_poddisruptionbudget_status_expected_pods |Other metrics |
|kube_poddisruptionbudget_status_desired_healthy |Other metrics |
|kube_poddisruptionbudget_status_current_healthy |Other metrics |
|kube_poddisruptionbudget_labels |Other metrics |
|kube_poddisruptionbudget_created |Other metrics |
|kube_poddisruptionbudget_annotations |Other metrics |
|kube_pod_status_scheduled_time |Other metrics |
|kube_pod_status_scheduled |Other metrics |
|kube_pod_start_time |Other metrics |
|kube_pod_restart_policy |Other metrics |
|kube_pod_init_container_status_waiting |Other metrics |
|kube_pod_init_container_status_terminated_reason |Other metrics |
|kube_pod_init_container_status_terminated |Other metrics |
|kube_pod_init_container_status_running |Other metrics |
|kube_pod_init_container_status_restarts_total |Other metrics |
|kube_pod_init_container_status_ready |Other metrics |
|kube_pod_init_container_resource_requests |Other metrics |
|kube_pod_init_container_resource_limits |Other metrics |
|kube_pod_init_container_info |Other metrics |
|kube_pod_container_state_started |Other metrics |
|kube_pod_completion_time |Other metrics |
|kube_pod_annotations |Other metrics |
|kube_persistentvolumeclaim_resource_requests_storage_bytes |Basic metrics |
|kube_persistentvolumeclaim_info |Other metrics |
|kube_persistentvolumeclaim_access_mode |Other metrics |
|kube_persistentvolume_info |Other metrics |
|kube_node_created |Other metrics |
|kube_node_annotations |Other metrics |
|kube_namespace_status_phase |Other metrics |
|kube_namespace_created |Basic metrics |
|kube_namespace_annotations |Other metrics |
|kube_lease_renew_time |Other metrics |
|kube_lease_owner |Other metrics |
|kube_ingress_path |Other metrics |
|kube_ingress_metadata_resource_version |Other metrics |
|kube_ingress_labels |Other metrics |
|kube_ingress_info |Other metrics |
|kube_ingress_created |Other metrics |
|kube_ingress_annotations |Other metrics |
|kube_endpoint_ports |Other metrics |
|kube_endpoint_labels |Other metrics |
|kube_endpoint_info |Other metrics |
|kube_endpoint_created |Other metrics |
|kube_endpoint_annotations |Other metrics |
|kube_endpoint_address_not_ready |Other metrics |
|kube_endpoint_address_available |Other metrics |
|kube_deployment_status_observed_generation |Other metrics |
|kube_deployment_spec_strategy_rollingupdate_max_unavailable |Other metrics |
|kube_deployment_spec_strategy_rollingupdate_max_surge |Other metrics |
|kube_deployment_spec_paused |Other metrics |
|kube_deployment_metadata_generation |Other metrics |
|kube_deployment_annotations |Other metrics |
|kube_daemonset_status_observed_generation |Other metrics |
|kube_daemonset_metadata_generation |Other metrics |
|kube_daemonset_annotations |Other metrics |
|kube_configmap_metadata_resource_version |Other metrics |
|kube_configmap_labels |Other metrics |
|kube_configmap_info |Other metrics |
|kube_configmap_created |Other metrics |
|kube_configmap_annotations |Other metrics |
|kube_job_complete |Other metrics |
|kube_job_created |Other metrics |
|kube_job_info |Other metrics |
|kube_job_owner |Other metrics |
|kube_job_spec_completions |Other metrics |
|kube_job_spec_parallelism |Other metrics |
|kube_job_status_active |Other metrics |
|kube_job_status_completion_time |Other metrics |
|kube_job_status_failed |Other metrics |
|kube_volumeattachment_info |Other metrics |
|kube_job_status_start_time |Other metrics |
|kube_job_status_succeeded |Other metrics |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more details about other metrics, see the the <a href="https://github.com/kubernetes/kube-state-metrics/tree/master/docs">official documentation</a>.</div>
