Install
=====

.. _install:

Install
------------

To use TrioMix, first install it using git:

.. code-block:: console

   $ git clone https://github.com/cjyoon/triomix.git

To verify installation, you can use the following commands. If everything is setup correctly, the following commands should result in the TrioMix help menu being printed in your terminal.

.. code-block:: console

   $ cd triomix
   $ python triomix.py -h
   

Dependencies 
----------------

TrioMix is written in Python (v3.5 or later) and R. Following Python and R packages are used in TrioMix. 

* Python
	* pysam
	* pandas

* R
	* optparse
	* tidyverse
	* bbmle
	* PSCBS


Other dependencies 
----------------

TrioMix internally uses ``samtools``, ``Rscript``, and ``gzip``. Make sure these are in your ``$PATH``. Otherwise, you can edit the absolute path of each of these in ``path_config.json``. 

.. code-block:: console

  $ cat path_config.json
  {"SAMTOOLS": "/path/to/samtools", # default is 'samtools'
   "RSCRIPT": "/path/to/Rscript", # default is 'Rscript'
   "GZIP": "/path/to/gzip" # default is 'gzip'
  }



Using the docker images
----------------
Pre-built docker image with all prerequisites installed is available. 

.. code-block:: console

	$ docker pull cjyoon/triomix


