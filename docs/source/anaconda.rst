Create a new virtual environment with Anaconda
==============================================

A Anaconda module is available on the cluster. You can use it to create a virtual environment and install packages in it. This is useful when you need to install custom versions of packages that must comply with the specific requirements of your software.

The first time, you'll need to load the Anaconda module and initialize it:

::

    [<username>@cld-ter-ui-01 ~]$ module load anaconda3-2024.10-1
    [<username>@cld-ter-ui-01 ~]$ conda init

::

The ``conda init`` command will add lines to the ``/shared/home/<username>/.bashrc`` file to initialize the conda environment. You need to source this file anytime you want to activate a virtual environment.


Create the virtual environment
-------------------------------

To create a new virtual environment, load the Anaconda module and run the following commands:

::

    [<username>@cld-ter-ui-01 ~]$ module load anaconda3-2024.10-1
    [<username>@cld-ter-ui-01 ~]$ conda create --name myenv python=3.8

::

Replace ``myenv`` with the name you want to give to your virtual environment. You can also replace ``3.8`` with the version of Python you want to use.

The virtual environment is created in the ``/shared/home/<username>/.conda/envs/`` directory. You can list all the virtual environments you have created with the following command:

::

    [<username>@cld-ter-ui-01 ~]$ conda env list
    # conda environments:
    #
    myenv                    /shared/home/<username>/.conda/envs/myenv

::

Activate the virtual environment
--------------------------------

To activate the virtual environment, run the following commands:

::

    [<username>@cld-ter-ui-01 ~]$ module load anaconda3-2024.10-1
    [<username>@cld-ter-ui-01 ~]$ source .bashrc
    (base) [<username>@cld-ter-ui-01 ~]$ conda activate myenv
    (myenv) [<username>@cld-ter-ui-01 ~]$

::

The prompt will change to show the name of the virtual environment in parentheses. The python binary in the virtual environment is now the default python binary:

::

    (myenv) [<username>@cld-ter-ui-01 ~]$ which python
    /shared/home/<username>/.conda/envs/myenv/bin/python

::

Install packages in the virtual environment
-------------------------------------------

Now you can install packages in your virtual environment with conda. For example:

::

    (myenv) [<username>@cld-ter-ui-01 ~]$ conda install numpy scipy pandas

::

This packages will be installed in the virtual environment and will not interfere with the system packages. The path to the packages is ``/shared/home/<username>/.conda/envs/myenv/lib/python3.8/site-packages/``.


Deactivate the virtual environment
----------------------------------

To deactivate the virtual environment, run:

::

    (myenv) [<username>@cld-ter-ui-01 ~]$ conda deactivate
    (base) [<username>@cld-ter-ui-01 ~]$

::

Delete the virtual environment
------------------------------

To delete a virtual environment, run the following command:

::

    [<username>@cld-ter-ui-01 ~]$ conda env remove --name myenv

::


