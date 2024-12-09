Application software
====================

Application software in the cluster is managed through
`environment modules <https://modules.readthedocs.io/en/latest>`__.




Software module can be loaded and unloaded dynamically and atomically.
Basically when you load a software module, you set the needed environment variables
(e.g. PATH, LD_LIBRARY_PATH, etc.) needed to use that software.

A software module is defined by a modulefile, which contains the information needed
to configure the shell for that application.

For the User Inteface node, you can see the available software modules using the
``module avail`` command, e.g.:

::
   
  [sgaravat@cld-ter-ui-01 ~]$ module avail
  -------------------------------------- /usr/share/Modules/modulefiles ---------------------------------------
  dot  module-git  module-info  modules  null  use.own  

  ------------------------------------------ /shared/sw/modulefiles -------------------------------------------
  gcc-12.4.0  openmpi-5.0.5_gcc-12.4.0  

  Key:
  modulepath  
  [sgaravat@cld-ter-ui-01 ~]$ 




To use one of this application, you need to load the relevant module using the
``module load <module>`` command, e.g:

::
   
  [sgaravat@cld-ter-ui-01 ~]$ which mpirun
  /usr/bin/which: no mpirun in (/usr/share/Modules/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin)
  [sgaravat@cld-ter-ui-01 ~]$ module load openmpi-5.0.5_gcc-12.4.0
  [sgaravat@cld-ter-ui-01 ~]$ which mpirun
  /shared/sw/openmpi-5.0.5_gcc-12.4.0/bin/mpirun
  [sgaravat@cld-ter-ui-01 ~]$ 




The list of the loaded modules can be retrieved using the ``module list`` command.
When you don't need anymore an application, you can unload the relevant module
using the ``module unload <module>`` command, e.g.:

::

  [sgaravat@cld-ter-ui-01 ~]$ module list
  Currently Loaded Modulefiles:
   1) openmpi-5.0.5_gcc-12.4.0   2) use.own  
  [sgaravat@cld-ter-ui-01 ~]$ module unload use.own
  [sgaravat@cld-ter-ui-01 ~]$ module list
  Currently Loaded Modulefiles:
   1) openmpi-5.0.5_gcc-12.4.0  
  [sgaravat@cld-ter-ui-01 ~]$ 



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

  [sgaravat@cld-ter-ui-01 ~]$ module load use.own
  [sgaravat@cld-ter-ui-01 ~]$ module avail
  ---------------------------------------------------------- /usr/share/Modules/modulefiles ----------------------------------------------------------
  dot  module-git  module-info  modules  null  use.own  
 
  -------------------------------------------------------------- /shared/sw/modulefiles --------------------------------------------------------------
  gcc-12.4.0  openmpi-5.0.5_gcc-12.4.0  
 
  ------------------------------------------------------- /shared/home/sgaravat/privatemodules --------------------------------------------------------
  gcc-13.4.0  null  
 
  Key:
  loaded  modulepath  
  [sgaravat@cld-ter-ui-01 ~]$ module load gcc-13.4.0
  [sgaravat@cld-ter-ui-01 ~]$ echo $PATH
  /shared/sw/gcc-13.4.0/bin:/shared/home/sgaravat/.local/bin:/shared/home/sgaravat/bin:/root/.local/bin:/root/bin:/usr/share/Modules/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin
  [sgaravat@cld-ter-ui-01 ~]$ 

Use environment modules with SLURM
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
The following example shows a SLURM submit file where the needed software module
is loaded before executing the user payload:

::
   
  #!/bin/sh
  #SBATCH --output=/shared/home/sgaravat/JOB-%x.%j.out
  #SBATCH --error=/shared/home/sgaravat/JOB-%x.%j.err
  #SBATCH --nodes=2
  #SBATCH --ntasks-per-node=3
  module load openmpi-5.0.5_gcc-12.4.0
  srun -l --mpi=pmix /shared/home/sgaravat/hello



  

Other information
^^^^^^^^^^^^^^^^^


For more information on environment module, please see:
https://modules.readthedocs.io/en/latest.
