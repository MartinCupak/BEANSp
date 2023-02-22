===========
beans tests
===========

Bayesian Estimation of Accreting Neutron Star parameters (BEANSp)

Settle test suite
-----------------

Short functional test (SFT) for settle
======================================

This is just a simple end-to-end positive test which compares one specific settle solver run with expected results and prints Passed/Failed.

Here is how to run short functional settle test on a linux box (tested on Ubuntu 20.04LTS):
  
#. Create/activate conda environment for beans:

   .. sourcecode::
   
      # create conda env if does not exist
      conda create --name beans python==3.8
      conda activate beans
      pip install -r requirements.txt # assuming we are in the beans git repo checkout folder
   
   \... or only the "activate" line if such an envirinment already does exist.

#. Compile & install settle lib (goes to ``/usr/local/lib``, requires sudo pernissions) and run the SFT, all in one command!

   .. code::

      cd settle
      make test

   This prints a bunch of lines with numbers that are the settle solver results plus binary result of one settle run (comparing with expected values) - either "PASSED" or "FAILED".

   
Performance test (benchmark) for settle
=======================================

Jupyter notebook test runs settle on 60 lines of input data from a file. Repeats the run a number of times in a loop. It prints duration of the solver run for each step, overall and average. The "settle sum time" means accumulated time spent calling settle solver, stripped of the main loop python code overhead, but including the overhead of the python wrapper around the settle C/C++ library interface function. Reference times are TBD, nothing to compare with at the moment.

*Note: execution times depend on overall system load.*

#. Compile & install settle lib (goes to ``/usr/local/lib``, requires sudo pernissions)

   .. code::

      cd settle
      make install
   
#. Use the same conda environment as for beans, just add jupyter

   .. sourcecode::

      conda activate beans
      pip install jupyter

#. Open and run the jupyter motebook

   .. code::

      cd ../tests/benchmark
      jupyter notebook beans_benchmark.ipynb
