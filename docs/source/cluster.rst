Overview of the INFN Padova HPC Cluster
=======================================

The resources provided by the INFN Padova HPC cluster are the following:

*  6 CPU only nodes cld-ter-01..06: each node has 2 AMD EPYC 9654 processors
   (192 Cores, 384 threads in total) and 1.5 TB of RAM
*  6 CPU-GPU nodes cld-ter-gpu-01..06: each node has 2 AMD EPYC 9654 processors
   (192 Cores, 384 threads in total), 1.5 TB of RAM and 4 NVIDIA H100 80GB HBM3 GPUs

These nodes are interconnected through a high bandwith, low latency Infiniband network.

The cluster also integrates a server owned by the the "Quantum Matter and
Information" group:

* a node (cld-dfa-gpu-06) with 2 Intel Xeon Platinum 8452Y processors
  y(72 cores, 144 threads), 1.5 TB
  of RAM and 1 NVIDIA L40S GPU.

Such resources are managed through the SLURM resource manager.


Available SLURM partitions
--------------------------
A Slurm partition exposes a set of resources.
Coupled with each partition there are a list of QOS, that specifies 
constraints (e.g. on the number of maximum usable resources, on the job time
limit, etc.) and other characteristics (e.g. priority).

When you submit a job, you must specify the partition and the QOS to be used (unless
you are fine with the default values)



In the INFN Padova HPC cluster the following partitions are available:

* **onlycpus**: this partition groups compute nodes that don't have GPU. This is the default partition
* **gpus**: the partition that encompasses compute nodes with GPUs.  
* **enipiml**: this partition is usable only by the users of the ENIPIML project.  
* **enipred**: this partition is usable only by the users of the ENIPRED project.  
* **qst**: this partition is usable only by the users of the "Quantum Matter
  and Information" group:
   

.. NOTE ::

   Please use the `gpus` partition only if your job needs one or more GPU accelerators.  

  
The following table summarizes which are the QOS available:




+--------------------------+------------------+-----------------------------------+----------+----------------------------------------------+
| QOS                      | MaxWallClockTime | Max usable Resources              | Priority | Notes                                        |
+==========================+==================+===================================+==========+==============================================+
| **normal**               | 24 hours         | 60 cores, 240 GB of RAM memory    | 60       | Default QoS for onlycpus and gpus partition  |
|                          |                  | 4 GPUs NVIDIA H100 80GB HBM3      |          |                                              | 
+--------------------------+------------------+-----------------------------------+----------+----------------------------------------------+
| **fast**                 | 2 hours          | 80 cores, 320 GB of RAM memory    | 100      |                                              |
|                          |                  | 4 GPUs NVIDIA H100 80GB HBM3      |          |                                              |
+--------------------------+------------------+-----------------------------------+----------+----------------------------------------------+
| **long**                 | 3 days           | 40 cores, 160 GB of RAM memory    | 40       |                                              |
|                          |                  | 2 GPUs NVIDIA H100 80GB HBM3      |          |                                              |
+--------------------------+------------------+-----------------------------------+----------+----------------------------------------------+
| **verylong**             | 7 days           | 20 cores, 80 GB of RAM memory     | 20       |                                              |
|                          |                  | 2 GPUs NVIDIA H100 80GB HBM3      |          |                                              |
+--------------------------+------------------+-----------------------------------+----------+----------------------------------------------+
| **enipiml**              | 30 days          | 384 cores, 1500 GB of RAM memory, | 60       | Default QoS for the enipiml partition        |
|                          |                  | 4 GPUs NVIDIA H100 80GB HBM3      |          |                                              |
+--------------------------+------------------+-----------------------------------+----------+----------------------------------------------+
| **enipred**              | 30 days          | 384 cores, 1500 GB of RAM memory, | 60       | Default QoS for the enipred partition        |
|                          |                  | 4 GPUs NVIDIA H100 80GB HBM3      |          |                                              |
+--------------------------+------------------+-----------------------------------+----------+----------------------------------------------+
| **qst**                  | 30 days          | 144 cores, 1500 GB of RAM memory, | 60       | Default QoS for the qst partition            |
|                          |                  | 1 GPU NVIDIA L40S                 |          |                                              | 
+--------------------------+------------------+-----------------------------------+----------+----------------------------------------------+

