# Flavor

The flavor or instance type determines the resources of the host computer used for your instance. Each flavor offers different compute, memory and other capabilities. Select an flavor based on the requirements of the application or software that you plan to run on your instance.\
In summary, GreenNode provides a variety of flavor so you can choose the type that best meets your requirements. The first part of the flavor name indicates the instance family and generation, for example "s1" means Intel Scalable Gen3 CPU Platform or "a1" for AMD EPYC Milan CPU Platform. The second part indicates the type of resource ratio such as Standard or HighCPU or HighMem. The remain part is the flavor size, which describes the number of vCPU and RAM (unit GB) used for the instance.

<figure><img src="../../../.gitbook/assets/image (445).png" alt=""><figcaption></figcaption></figure>

<figure><img src="https://docs.vngcloud.vn/download/attachments/49648006/download.png?version=1&#x26;modificationDate=1669016444000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

GreenNode provides a wide selection of flavor profile optimized for different use cases. To determine which flavor meet your requirements, such as supported compute resources, or GPU resources, see more at {Flavor detail page}.

* **Instance family**: A curated set of processor and hardware configurations optimized for specific workloads. For example General purpose, Compute Optimized, Memory Optimized or Accelerator (GPU).
  * General Purpose: best price-performance ratio for a variety of workloads.
  * Compute Optimized: highest performance per core on instance and optimized for compute-intensive workloads.
  * Memory Optimized: offering more memory per core than other machine families and optimized for memory-intensive workloads.
  * GPU Optimized: offering GPU Instance optimized for ML/AI workloads that require GPUs. H100 GPU flavors support **Multi-Instance GPU (MIG)** — allowing a single physical GPU to be partitioned into multiple isolated instances. See [Use Multi-Instance GPU (MIG)](use-multi-instance-gpu-mig.md).
* **CPU platform**: Instance families are further classified by CPU platform. For example, the S and S1 series within the General Purpose instance family is the CPU Intel Scalable Gen2 and Gen3 series. Accordingly, A and A1 is described for CPU AMD EPYC Zen2 and Zen3 series. The number after the letter describes the generation of CPU.
* **Instance type**: describes the ratio of instance size which determines the CPU, memory, GPU... resource size used for your instance.
