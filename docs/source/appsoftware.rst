Application software
====================
.. _appsw:

Application software in the cluster is managed through:

* CVMFS
* Environment modules


Application software through CVMFS
----------------------------------
Many experiments are using CVMFS to distribute the relevant software.
In the HPC Cluster CVMFS is installed on every compute node.
By default the LHC and EGI repositories are made available. If some other
repository is needed, please contact the suppport team.
  
Application software throgh Environment modules
-----------------------------------------------

`Environment software modules <https://modules.readthedocs.io/en/latest>`__
can be loaded and unloaded dynamically and atomically.
Basically when you load a software module, you set the needed environment variables
(e.g. PATH, LD_LIBRARY_PATH, etc.) needed to use that software.

A software module is defined by a modulefile, which contains the information needed
to configure the shell for that application.

For the User Inteface node, you can see the available software modules using the
``module avail`` command, e.g.:

::
   
  [<username>@cld-ter-ui-01 ~]$ module avail
  -------------------------------------- /usr/share/Modules/modulefiles ---------------------------------------
  dot  module-git  module-info  modules  null  use.own  

  ------------------------------------------ /shared/sw/modulefiles -------------------------------------------
  gcc-12.4.0  openmpi-5.0.5_gcc-12.4.0  

  Key:
  modulepath  
  [<username>@cld-ter-ui-01 ~]$ 




To use one of this application, you need to load the relevant module using the
``module load <module>`` command, e.g:

::
   
  [<username>@cld-ter-ui-01 ~]$ which mpirun
  /usr/bin/which: no mpirun in (/usr/share/Modules/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin)
  [<username>@cld-ter-ui-01 ~]$ module load openmpi-5.0.5_gcc-12.4.0
  [<username>@cld-ter-ui-01 ~]$ which mpirun
  /shared/sw/openmpi-5.0.5_gcc-12.4.0/bin/mpirun
  [<username>@cld-ter-ui-01 ~]$ 




The list of the loaded modules can be retrieved using the ``module list`` command.
When you don't need anymore an application, you can unload the relevant module
using the ``module unload <module>`` command, e.g.:

::

  [<username>@cld-ter-ui-01 ~]$ module list
  Currently Loaded Modulefiles:
   1) openmpi-5.0.5_gcc-12.4.0   2) use.own  
  [<username>@cld-ter-ui-01 ~]$ module unload use.own
  [<username>@cld-ter-ui-01 ~]$ module list
  Currently Loaded Modulefiles:
   1) openmpi-5.0.5_gcc-12.4.0  
  [<username>@cld-ter-ui-01 ~]$ 



Create your own application module
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The modules in /shared/sw/modulefiles are the ones made available by the
administrators.

You can create your own module, creating the relevant modulefile in the
$HOME/privatemodules directory.
To use this module, you need to load first the ``use.own`` module:

::

  module load use.own
  module load <proprio-modulo>


In the following example the gcc-13.4.0 module was created by the end user:

::

  [<username>@cld-ter-ui-01 ~]$ module load use.own
  [<username>@cld-ter-ui-01 ~]$ module avail
  ---------------------------------------------------------- /usr/share/Modules/modulefiles ----------------------------------------------------------
  dot  module-git  module-info  modules  null  use.own  
 
  -------------------------------------------------------------- /shared/sw/modulefiles --------------------------------------------------------------
  gcc-12.4.0  openmpi-5.0.5_gcc-12.4.0  
 
  ------------------------------------------------------- /shared/home/<username>/privatemodules --------------------------------------------------------
  gcc-13.4.0  null  
 
  Key:
  loaded  modulepath  
  [<username>@cld-ter-ui-01 ~]$ module load gcc-13.4.0
  [<username>@cld-ter-ui-01 ~]$ echo $PATH
  /shared/sw/gcc-13.4.0/bin:/shared/home/<username>/.local/bin:/shared/home/<username>/bin:/root/.local/bin:/root/bin:/usr/share/Modules/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin
  [<username>@cld-ter-ui-01 ~]$ 

Use environment modules with SLURM
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
The following example shows a SLURM submit file where the needed software module
is loaded before executing the user payload:

::
   
  #!/bin/sh
  #SBATCH --output=/shared/home/<username>/JOB-%x.%j.out
  #SBATCH --error=/shared/home/<username>/JOB-%x.%j.err
  #SBATCH --nodes=2
  #SBATCH --ntasks-per-node=3
  #SBATCH --mail-type=ALL
  #SBATCH --mail-user=<email-address>
  module load openmpi-5.0.5_gcc-12.4.0
  srun -l --mpi=pmix /shared/home/<username>/hello



  

Other information
^^^^^^^^^^^^^^^^^


For more information on environment module, please see:
https://modules.readthedocs.io/en/latest.
