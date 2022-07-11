Install
=====

.. _install:

Install
------------

To use TrioMix, first install it using git:

.. code-block:: console

   $ git clone https://github.com/cjyoon/triomix.git

Dependencies 
----------------

TrioMix is written in Python (v3.5 or later) and R. Following Python and R packages are used in TrioMix. 

* Python
	* pysam

* R
	* optparse
	* tidyverse
	* bbmle


Other dependencies 
----------------

TrioMix internally uses ``samtools`` ``Rscript`` ``gzip``. Make sure these are in your ``$PATH``. Otherwise, you can edit the absolute path of each of these in ``path_config.json``. 


Using the docker images
----------------
Pre-built docker image with all prerequisites installed is available. 

.. code-block:: console

	$ docker pull cjyoon/triomix


