---
title: "GPU instance naming and type recommendations"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/Best_practices_for_instance_selection"
---

The platform offers a variety of instance types to meet your requirements in different scenarios. This topic describes how to select and purchase a GPU instance based on business requirements to empower your businesses with the elastic ECS service.

<span id=".5a6e5L6L6KeE5qC85ZCN56ew"></span>
## Instance name

The GPU Compute Service (GPU) servers offered by the platform can be categorized into Compute\-optimized and HPC\-optimized based on performance.

<span id="GlDlU734"></span>
### Instance Families

**Format: <Instance family series\><GPU graphics card type\><Processor type\><Instance family generation\><Instance family suffix\>** 


|Instance type family series |GPU graphics card type |**Processor Type** |**Instance type family generation** |**Suffix** |
|---|---|---|---|---|
|Lowercase letters, representing an instance type family type, are usually abbreviations of certain words that represent the performance domain of the instance type family.<br><br><br>* p: Performance, general performance type<br><br>* t: Training, applicable for training scenarios<br><br>* i: Inference, applicable for inference scenarios<br><br>* g: Graphic, graphics\-intensive<br><br>* ebm prefix: the EBM type<br><br>* hpc prefix: HPC\-optimized instances with access to RDMA network |A lowercase English letter representing the GPU graphics card vendor.<br><br>n：NVIDIA GPU |A lowercase English letter representing the CPU vendor.<br><br><br>* i: Intel<br><br>* a: AMD<br><br>* r: ARM |Arabic numerals that indicate the generation of the instance type family. A larger number indicates a later generation. |Lowercase English letters, indicating other attributes of the instance family<br><br><br>* c: customized, indicating customized edition<br><br>* l: light, indicating the lightweight edition<br><br>* e: balanced enhanced attribute. For example, balanced vCPU, memory, and network capability.<br><br>* h: high\-performance, indicating high\-performance edition<br><br>* d: equipped with local volume<br><br>* v/t: GPU card of V/T series<br><br>* vws: Rendering instance configured with vDWS License server and GRID driver<br><br><br>For more instance attributes, please refer to [Instance types](https://docs.byteplus.com/en/docs/95/20686#.5a6e5L6L6KeE5qC857G75Z6L). |


<span id="GnYHZDwn"></span>
### Instance type

**Format**: **ecs.<Instance family name\><Processor tag\>.<Size\>** 


|ecs |Instance type family name |Size |
|---|---|---|
|Represents the product name Elastic Compute Service (ECS) and cannot be changed. |For details, refer to [Instance type family name](https://docs.byteplus.com/en/docs/95/20686#GlDlU734). |The number of vCPUs for an instance type, typically represented as `large` or `<nx>large`. `large` represents 2 vCPUs, `xlarge` represents 4 vCPUs, `2xlarge` represents 2 \* 4 = 8 vCPUs, and `3xlarge` represents 3 \* 4 = 12 vCPUs. So, a larger n value represents more vCPUs and a larger specification.<br><br>For example, ecs.hpcpni2.28xlarge represents an instance in the HPC\-optimized pni2 instance family with 112 vCPUs. |


<span id=".5a6e5L6L6KeE5qC857G75Z6L"></span>
## Instance type

ECS offers multiple instance types with different computing and storage capabilities to suit different scenarios. For more information on instance types, refer to [Instance types](https://docs.byteplus.com/en/docs/gpu/Introduction-to-instance-types).


|Instance family type |Identifier for instance family |Description |
|---|---|---|
|GPU Accelerated |* gni3c<br><br>* ebmgni3c<br><br>* gni3cl |* ebm: The EBM server.<br><br>* g: Graphic, the GPU card applicable for graphics\-intensive scenarios.<br><br>* n: The NVIDIA GPU graphics card.<br><br>* i: Intel processors are associated.<br><br>* 3: the 3rd\-generation series. |
||pni3l |* p: general performance GPU card.<br><br>* n: the NVIDIA GPU graphics card.<br><br>* i: the Intel processor.<br><br>* 3: instance generation. |
|GPU Rendering |* gni3cl\-vws<br><br>* gni3cg\-vws |* g: Graphic, the GPU card applicable for graphics\-intensive scenarios.<br><br>* n: The NVIDIA GPU graphics card.<br><br>* i: Intel processors are associated.<br><br>* 3: the 3rd\-generation series.<br><br>* c: customized, indicating customized edition.<br><br>* vws: configured with vDWS License server and GRID driver installed. |
|HPC\-optimized |hpcpni3lh |* hpc: HPC\-optimized instances that support RDMA network.<br><br>* p: general performance GPU cards are associated.<br><br>* n: the NVIDIA GPU graphics card.<br><br>* i: Intel processors are associated.<br><br>* 3: the 3rd\-generation series. |
||* ebmhpcpni3l<br><br>* hpcpni3ln |* ebm: Elastic Bare Metal.<br><br>* hpc: HPC\-optimized instances that support RDMA network.<br><br>* p: general performance GPU cards are associated.<br><br>* n: the NVIDIA GPU graphics card.<br><br>* i: Intel processors are associated.<br><br>* 3: the 3rd\-generation series.<br><br>* n: Network.<br><br>* l: light, indicating lightweight edition. |
