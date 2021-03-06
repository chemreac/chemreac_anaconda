Conda recipes for chemreac
==========================
This repo collects build scripts for building conda packages for `chemreac <https://github.com/chemreac/chemreac>`_.
It uses the `conda_builder_linux <https://github.com/ContinuumIO/docker-images/tree/master/conda_builder_linux>`_  image provided by ContinuumIO.

Published packages: https://conda.anaconda.org/chemreac

How to build the recipes
------------------------
If ``start_cpp98.sh`` is in your ``$PATH`` (see ``conda_builder_linux`` above):

::

   $ git clone git://github.com/chemreac/chemreac_anaconda.git
   $ cd chemreac_anaconda
   $ ./orchestrate_all.sh


here is an example how I build lapack on my workstation:

::

   $ PATH=~/vc/docker-images/conda_builder_linux:$PATH ./orchestrate_all.sh recipes/10_non-python/10_lapack/

now when I try to build e.g. sundials

::

   $ PATH=~/vc/docker-images/conda_builder_linux:$PATH ./orchestrate_all.sh recipes/10_non-python/30_sundials/

it will use the conda package built in the previous step.

And that is it. Built packages are then found under ``./opt/miniconda/conda-bld/linux-64``.
Note that the ``./opt`` dir may grow quite large over time, and you will need to remove it if there has
been a new docker image published by ContinuumIO in between your builds.


The built packages are then uploaded manually to anaconda.org using the ``anaconda`` tool.
To test the anaconda.org/chemreac repo another script is provided:

::

   $ ./test_anaconda_chemreac.sh
