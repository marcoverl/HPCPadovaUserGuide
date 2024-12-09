Running MPI jobs
================

In the HPC cluster, you can use the OpenMPI software to run parallel jobs.

The OpenMPI is provided through an ennvironment module.

Compiling
^^^^^^^^^

In the following example a simple MPI application is compiled using ``mpicc``
after having loaded
the relevant openmpi software module:


::

  [sgaravat@cld-ter-ui-01 ~]$ cat hello.c 
  #include <mpi.h>
  #include <stdio.h>
  #include <stddef.h>

  int main(int argc, char** argv) {
    // Initialize the MPI environment. The two arguments to MPI Init are not
    // currently used by MPI implementations, but are there in case future
    // implementations might need the arguments.
    MPI_Init(NULL, NULL);

    // Get the number of processes
    int world_size;
    MPI_Comm_size(MPI_COMM_WORLD, &world_size);

    // Get the rank of the process
    int world_rank;
    MPI_Comm_rank(MPI_COMM_WORLD, &world_rank);

    // Get the name of the processor
    char processor_name[MPI_MAX_PROCESSOR_NAME];
    int name_len;
    MPI_Get_processor_name(processor_name, &name_len);

    // Print off a hello world message
    printf("Hello world from processor %s, rank %d out of %d processors\n",
           processor_name, world_rank, world_size);

    // Finalize the MPI environment. No more MPI calls can be made after this
    MPI_Finalize();
  }
  [sgaravat@cld-ter-ui-01 ~]$ 

::
  
  [sgaravat@cld-ter-ui-01 ~]$ module load openmpi-5.0.5_gcc-12.4.0
  [sgaravat@cld-ter-ui-01 ~]$ mpicc -o hello hello.c



Submitting a MPI SLURM job
^^^^^^^^^^^^^^^^^^^^^^^^^^

This is an example of a SLURM submit file to run a previously compiled application:

::
   
  [sgaravat@cld-ter-ui-01 ~]$ cat mpi.sh
  #!/bin/sh
  #SBATCH --output=/shared/home/sgaravat/JOB-%x.%j.out
  #SBATCH --error=/shared/home/sgaravat/JOB-%x.%j.err
  #SBATCH --nodes=2
  #SBATCH --ntasks-per-node=3
  module load openmpi-5.0.5_gcc-12.4.0
  srun -l --mpi=pmix /shared/home/sgaravat/hello


Please note the ``module load openmpi-5.0.5_gcc-12.4.0`` directive and the
``--mpi=pmix`` option in the srun command.

Let's submit the job:

::

  [sgaravat@cld-ter-ui-01 ~]$ sbatch mpi.sh
  Submitted batch job 468
  [sgaravat@cld-ter-ui-01 ~]$ squeue 
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
               468 cpu-nodes   mpi.sh sgaravat  R       0:03      2 cld-ter-[01-02]
  [sgaravat@cld-ter-ui-01 ~]$ 


Let's see the output when the job completes:

::
  
  [sgaravat@cld-ter-ui-01 ~]$ cat JOB-mpi.sh.468.out 
  2: Hello world from processor cld-ter-01.cloud.pd.infn.it, rank 2 out of 6 processors
  3: Hello world from processor cld-ter-02.cloud.pd.infn.it, rank 3 out of 6 processors
  0: Hello world from processor cld-ter-01.cloud.pd.infn.it, rank 0 out of 6 processors
  5: Hello world from processor cld-ter-02.cloud.pd.infn.it, rank 5 out of 6 processors
  1: Hello world from processor cld-ter-01.cloud.pd.infn.it, rank 1 out of 6 processors
  4: Hello world from processor cld-ter-02.cloud.pd.infn.it, rank 4 out of 6 processors
  [sgaravat@cld-ter-ui-01 ~]$

  
