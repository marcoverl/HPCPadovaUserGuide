Using GPUs
==========

To use one (or more) GPUs, you need to use the `gpu-nodes` partition and you need
to specify how many GPUs you need using the `--gres` directive.
E.g. with the following submit file 2 nodes with 2 H100 GPUs on each node (4 in totals) are
requested:

::
   
  #!/bin/sh
  #SBATCH --output=/shared/home/sgaravat/JOB-%x.%A.%a.out
  #SBATCH --error=/shared/home/sgaravat/JOB-%x.%A.%a.err
  #SBATCH --ntasks=6
  #SBATCH --nodes=2
  #SBATCH --partition gpu-nodes
  #SBATCH --gres gpu:nvidia-h100:2
  #SBATCH --mail-type=ALL
  #SBATCH --mail-user=massimo.sgaravatto@pd.infn.it
  cd $TMP_DIR
  srun -l /shared/home/sgaravat/myapp.sh
