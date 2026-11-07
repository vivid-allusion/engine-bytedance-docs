---
title: "Instance specification adjustment description"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Instance_specification_adjustment_description"
---

This topic describes the specification adjustment logic for VCI instances when conflicts arise between the specified instance type, instance family, and the resource configurations (such as CPU, memory, and GPU) during instance creation.

## General\-purpose instance

### Create an instance by specifying an instance family

When creating an instance, if you only specify the instance family and configure the vCPU and memory of containers but do not specify a specific instance type, VCI calculates the specific VCI instance type required by your Pod as follows:

1. Calculate the total upper limits for the CPU and memory of pods separately:

   * The total CPU value is the higher of the two values: **the maximum CPU limit among all Init containers in the pod** and **the sum of the CPU limits of all application containers**.

      > **tip**

      > If no CPU limit is configured for an Init container or an application container, the CPU request value of the container is used.

   * The total memory value is the higher of the two values: **the maximum memory limit among all Init containers in the pod** and **the sum of the memory limits of all application containers**.

      > **tip**

      > If no memory limit is configured for an Init or application container, the memory request value of the container is used.

   * If neither the limit nor the request for memory or CPU is configured for a container in the pod, the value of that item is counted as 0.

2. The system automatically adjusts the pod specifications based on the total values and charges fees based on the instance specifications after the automatic adjustment. The adjustment method is as follows:

   |Total value |Calculation method |
   |---|---|
   |Total CPU value = 0<br><br>AND<br><br>Total memory value = 0 |The instance specification of 2 cores and 4 GiB is used by default. |
   |Total CPU value = 0; Total memory value != 0<br><br>OR<br><br>Total CPU value != 0; Total memory value = 0 |Match the lowest specification based on the total value of the non\-zero item:<br><br><br>1. First, match the non\-zero item, and select an instance specification that is consistent or close to but larger than the specification of the matched item.<br><br>2. Then, match the zero item and select an instance specification that is close to but greater than the specification of the matched item.<br><br><br>If the total memory value is 0.8 GiB and the total CPU value is 0, the [vci.u1](https://docs.byteplus.com/en/docs/vke/VCI-General-purpose#.6YCa55So566X5Yqb5Z6LLXUx) instance family is matched in the following order. First, match 1 GiB based on the total memory value of 0.8 GiB. Then, match the CPU of 0.25 cores based on the lowest specification matching principle. As a result, the specification of the created VCI pod is `vci.u1.0.25c-1gi`. |
   |Total CPU value != 0<br><br>AND<br><br>Total memory value != 0 |1. First, match the total CPU value and select an instance specification that is equal to or slightly larger than the matched specification (such as Specification A).<br><br>2. Then, match the total memory value and select an instance specification that is equal to or slightly larger than the matched specification:<br><br>   * If the total memory value is less than the minimum memory value of Specification A, select the minimum memory value of Specification A.<br><br>   * If the total memory value is within the memory range of Specification A, select an instance specification that is consistent or close to but larger than the total memory value.<br><br>   * If the total memory value is greater than the maximum memory value of Specification A, select an instance specification that is close to but larger than the memory value (Specification B), and adjust the total CPU value to the CPU value of Specification B.<br><br><br>For example, when the total CPU value matches the specifications of 1.25 cores in the vci.u1 instance family, two specifications in the vci.u1 instance family are available: `vci.u1.1.25c-2.5gi` and `vci.u1.1.25c-5gi`:<br><br><br>* If the total memory value is 2 GiB, the `vci.u1.1.25c-2.5gi` specification is matched.<br><br>* If the total memory value is 3 GiB, the `vci.u1.1.25c-5gi` specification is matched.<br><br>* If the total memory value is 6 GiB, neither the `vci.u1.1.25c-2.5gi` nor the `vci.u1.1.25c-5gi` specification meets the requirements. Therefore, the `vci.u1.1.5c-6gi` specification is selected, which is close to 6 GiB. In this case, the CPU is no longer matched at 1.25 cores but at 1.5 cores. |
   |Either the total CPU or memory value exceeds the highest specification provided by VCI |If no item is matched, the VCI pod fails to be created. |

### Create an instance by specifying a specific instance type

When creating a general‑purpose instance, if you specify a specific VCI instance type but it conflicts with the vCPU and memory settings of your containers, VCI handles it as follows:

1. Calculate the total upper limits for the CPU and memory of pods separately. The calculation method for the total value is the same as that described in the **Create an instance by specifying only the instance family** section.

2. The system automatically adjusts the pod specifications based on the total values and charges fees based on the instance specifications after the automatic adjustment. The adjustment method is as follows:

   |Total value |Calculation method |
   |---|---|
   |Total CPU value = 0<br><br>AND<br><br>Total memory value = 0 |Use the VCI specifications specified in the annotation. |
   |Total CPU value = 0; Total memory value != 0<br><br>OR<br><br>Total CPU value != 0; Total memory value = 0 |Match the non\-zero items:<br><br><br>* If the specifications of the item are greater than those specified by the annotation, the system reports an error, and the instance fails to be created.<br><br>* If the specifications of the item are less than or equal to the specifications specified by the annotation, the specifications specified by the annotation are used. |
   |Total CPU value != 0<br><br>AND<br><br>Total memory value != 0 |1. Match the total CPU value first:<br><br>   * If the value is greater than the specifications specified by the annotation, the system reports an error, and the instance fails to be created.<br><br>   * If this value is less than or equal to the specifications specified by the annotation, continue to match the total memory value.<br><br>2. Match the total memory value:<br><br>   * If the value is greater than the specifications specified by the annotation, the system reports an error, and the instance fails to be created.<br><br>   * If the value is less than or equal to the specifications specified by the annotation, the specifications specified by the annotation are used. |
