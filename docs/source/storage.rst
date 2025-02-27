Storage in the HPC cluster
==========================

User home directory ($HOME, /shared/home/<username>) is available on all nodes
of the cluster.
A quota of 100 GB is assigned to each user on this storage area.

.. NOTE ::
   
   Please note that no backups are performed on the home directories.
   

Moreover each job is made available a scratch storage area on a fast local
storage. Such strach area, 
referred by the TMP_DIR environment variable, is available only on the node where
the job gets executed (i.e. it is not shared among all nodes).

.. NOTE ::
   
   Please note that the scratch area referred by the TMP_DIR environment variable
   is automatically deleted when the job completes its execution. It is therefore
   up to the job to copy the needed output files to the home directory or to
   another persistent storage.
