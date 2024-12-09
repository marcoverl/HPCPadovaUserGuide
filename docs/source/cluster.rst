Overview of the INFN Padova HPC Cluster
=======================================

The resources provided by the INFN Padova HPC cluster are the following:

*  6 CPU only nodes cld-ter-01..06: each node has 2 AMD EPYC 9654 processors
   (192 Cores, 384 threads in total) and 1.5 TB of RAM
*  6 CPU-GPU nodes cld-ter-gpu-01..06: each node has 2 AMD EPYC 9654 processors
   (192 Cores, 384 threads in total), 1.5 TB of RAM and 4 NVIDIA H100 GPUs

The nodes are interconnected through a high bandwith, low latency Infiniband network.

Such resources are managed through the SLURM resource manager.

User interface
^^^^^^^^^^^^^^
cld-ter-ui-01 is the node configured as user interface.
Such node is the node that must be used to submit your SLURM jobs.

SLURM Partitions
^^^^^^^^^^^^^^^^


