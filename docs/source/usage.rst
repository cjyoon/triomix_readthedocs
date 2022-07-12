Usage
=====

.. _run:

Basic Triomix command line: Detection of intrafamilial contamination in the offspring
------------

By default, TrioMix uses the parental genotypes (*GroupA, B, C SNPs*) to infer the intrafamilial contamination level in the child. The basic command line of using TrioMix is the following:

.. code-block:: console

   $ python triomix.py -f father.bam -m mother.bam -c child.bam -r reference.fasta

Triomix command line with common SNP only
------------

Using a pre-selected list of common SNP would speed up the total runtime of TrioMix as the computation is limited to those regions instead of the entire genome. TrioMix provides a list of common ``GRCh38`` and ``GRCh37`` SNPs selected from the GnomAD database. These two files are included in the github repository as a `common_snp <https://github.com/cjyoon/triomix/tree/master/common_snp/>`_ folder.  A ``-s`` argument specifies the SNP database that can be used. User can provide one's own set of SNP in BED format.


.. code-block:: console

   $ python triomix.py -f father.bam -m mother.bam -c child.bam -r reference.fasta -s common_snps/grch38_common_snps.bed.gz


Other optional arguments
------------




Default output files
------------
Triomix produces several output files files. 


``*.counts``: contains the position of the SNP loci in either GroupA, B, or C. Contains the read depths, alternative read counts for the trios. In addition, based on the parental genotype, will determine whether the child inherited the SNP from the father (F) or the mother (M). This file is used as the input for ``mle.R`` which estimates the contamination level using maximum likelihood estimation. 


``*.counts.summary.tsv``: contains the final estimated values of contamination from various sources. 


``*.homoalt.segements``: 


``*.summary``: contains the final results of ``triomix``. Detailed information on each column is as follows.



Triomix with verifybamID2
------------
``verifyBamID2`` is a robust tool that detects contamination from unrelated individuals. ``verifyBamID2`` can be run within TrioMix by adding ``--vbid [verifybamid resource file path]``. This resource file is also included in TrioMix as a `vbid <https://github.com/cjyoon/triomix/tree/master/vbid/>`_ folder in the github repository. This will run ``verifybamID2`` within Triomix for all three family members in the trio. 

.. code-block:: console

   $ python triomix.py -f father.bam -m mother.bam -c child.bam -r reference.fasta -s common_snps/grch38_common_snps.bed.gz --vbid vbid/grch38


Detection of intrafamilial contamination in the parent (i.e. parent DNA contamminated by child, or by another parent)
------------
To detect intrafamilial DNA contamination in the parent, ``--parent`` option can be used. This will use *GroupD SNPs* (where offspring's genotype is *homo-alt*) to detect the offspring DNA contaminating in the parents. 


.. code-block:: console

   $ python triomix.py -f father.bam -m mother.bam -c child.bam -r reference.fasta -s common_snps/grch38_common_snps.bed.gz --parent

Additional output generated with ``--parent`` 
------------
``*.groupd.counts``



Running TrioMix with a docker image
------------
Following example demonstrates how docker image can be used for runnint TrioMix.

.. code-block:: console

   $ docker run -t -d  -v /home/ubuntu/data:/data -v /home/ubuntu/results:/results:rw -v /home/ubuntu/data/sib25/:/data/sib25/ --name triomix_local cjyoon/triomix:v1.4
   $ docker exec -it triomix_local python /tools/triomix/triomix.py -f /data/M008_father.bam -m /data/M008_mother.bam -c /data/sib25/familymix.bam -r /data/Homo_sapiens_assembly38.fasta -t 10 -o results -s /tools/triomix/common_snp/grch38_common_snp.bed.gz


