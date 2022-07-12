Simulation
=====


.. _simulation:

Simulation
------------
Contamination can be simulated by randomly selecting read sequences from two BAM (or CRAM) files at a defined ratio. The total number of reads in each bam file is adjusted when creating a subsampled BAM file which is later merged into a single 'contaminated' bam file.


Test run with 1000 genomes trio
------------
In our `github <https://github.com/cjyoon/triomix/tree/master/test.sh>`_ a test script ``test.sh`` is provided which can created a simulated contamination BAM files from a 1000 genomes family. 

.. code-block:: console

   $ sh test.sh

This will download the 1000 genomes trio CRAM files, create simulated contamination files by subsampling. Note this will requires ``XXXX`` tool to be installed in your ``$PATH``.


CHECK IF TEST SCRIPT CAN BE CHANGED WITH SAMTOOLS MERGE and CRAM FILE USE, ALSO CRAI DOWNLOAD. 


Test results
------------


Test plots
------------
.. image:: images/1000g_simulation.jpg
