Overview of the INFN Padova HPC Cluster
=======================================

The resources provided by the INFN Padova HPC cluster are the following:

*  6 CPU only nodes cld-ter-01..06: each node has 2 AMD EPYC 9654 processors
   (192 Cores, 384 threads in total) and 1.5 TB of RAM
*  5 CPU-GPU nodes cld-ter-gpu-01..06: each node has 2 AMD EPYC 9654 processors
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
.. _Partitions:



A Slurm partition exposes a set of resources.
Coupled with each partition there are a list of QOS, that specifies 
constraints (e.g. on the number of maximum usable resources, on the job time
limit, etc.) and other characteristics (e.g. priority).

When you submit a job, you must specify the partition and the QOS to be used (unless
you are fine with the default values)



In the INFN Padova HPC cluster there are:

* partitions available to all users.
* partitions reserved to specific projects (therefore usable only by the relevant users).
* partitions available to all users that allow to use opportunically resources allocated to specific projects, when they are available.
  **Please note that jobs submitted to these partitions will be preempted (requeued) if jobs submitted to higher priority partitions require those resources.**


The following table describes the available partitions:




.. list-table:: 

   * - **Partition**
     - **Usable by**
     - **To be used for**
     - **Priority**
     - **Notes**
   * - **onlycpus**
     - all users
     - | jobs which don't
       | require GPUs
     - 20
     - default partition
   * - **gpus**
     - all users
     - | jobs which need
       | one or more H100 GPUs
     - 20
     - 
   * - **enipiml**
     - | users of the
       | ENIPIML project
     - | both gpus (up to 4 H100
       | GPUS) and only cpus jobs
     - 20
     - 
   * - **enipred**
     - | users of the
       | ENIPRED project
     - | both gpus (up to 4 H100
       | GPUS) and only cpus jobs
     - 20
     - 
   * - **qst**
     - | users of the
       | QST project
     - | both gpu (one L40S) and
       | only cpus jobs
     - 20
     - 
   * - **onlycpus-opp**
     - all users
     - | jobs which don't require 
       | GPUs and which can
       | manage preemption
     - 10  
     - | Jobs submitted to this partition will
       | be cancelled and requeued if jobs
       | submitted to higher priority partitions
       | need those resources
   * - **gpus-opp**
     - all users
     - | jobs which require one or
       | more GPUs (H100 and L40S)
       | and which can manage
       | preemption
     - 15 
     - | Jobs submitted to this partition will
       | be cancelled and requeued if jobs
       | submitted to higher priority partitions
       | need those resources





  
.. NOTE ::

   The `gpus` and `gpus-opp` partitions can be used only if your job needs one or more GPU accelerators.  

  
The following table summarizes which are the available QOS:




+--------------------------+------------------+-----------------------------------+----------+----------------------------------------------+
| QOS                      | MaxWallClockTime | Max usable Resources              | Priority | Notes                                        |
+==========================+==================+===================================+==========+==============================================+
| **normal**               | 24 hours         | 60 cores, 240 GB of RAM memory    | 60       | Default QoS                                  |
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
| **enipiml**              | 30 days          | 384 cores, 1500 GB of RAM memory, | 60       | Default QoS for enipiml users                |
|                          |                  | 4 GPUs NVIDIA H100 80GB HBM3      |          |                                              |
+--------------------------+------------------+-----------------------------------+----------+----------------------------------------------+
| **enipred**              | 30 days          | 384 cores, 1500 GB of RAM memory, | 60       | Default QoS for enipred users                |
|                          |                  | 4 GPUs NVIDIA H100 80GB HBM3      |          |                                              |
+--------------------------+------------------+-----------------------------------+----------+----------------------------------------------+
| **qst**                  | 30 days          | 144 cores, 1500 GB of RAM memory, | 60       | Default QoS for qst users                    |
|                          |                  | 1 GPU NVIDIA L40S                 |          |                                              | 
+--------------------------+------------------+-----------------------------------+----------+----------------------------------------------+

