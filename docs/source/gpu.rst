Using GPUs
==========

To use one (or more) GPUs, you need to use a partition able to provide the needed GPU accelerators (see :ref:`Available SLURM partitions<Partitions>`)
and you need
to specify how many and which GPUs you need using the `--gres` directive.
E.g. with the following submit file 2 nodes with 2 H100 GPUs on each node (4 in totals) are
requested:

::
   
  #!/bin/sh
  #SBATCH --output=/shared/home/<username>/JOB-%x.out
  #SBATCH --error=/shared/home/<username>/JOB-%x.err
  #SBATCH --ntasks=6
  #SBATCH --nodes=2
  #SBATCH --partition gpus
  #SBATCH --gres gpu:nvidia-h100:2
  #SBATCH --mail-type=ALL
  #SBATCH --mail-user=<email-address>
  cd $TMP_DIR
  module load cuda-12.6
  srun -l /shared/home/<username>/<myapp>



In the following example a L40S GPU is requested:

 ::
   
  #!/bin/sh
  #SBATCH --output=/shared/home/<username>/JOB-%x.out
  #SBATCH --error=/shared/home/<username>/JOB-%x.err
  #SBATCH --ntasks=30
  #SBATCH --nodes=1
  #SBATCH --mem=50G
  #SBATCH --partition qst
  #SBATCH --gres gpu:nvidia-l40s:1
  #SBATCH --mail-type=ALL
  #SBATCH --mail-user=<email-address>
  cd $TMP_DIR
  module load cuda-12.6
  srun -l /shared/home/<username>/<myapp>
