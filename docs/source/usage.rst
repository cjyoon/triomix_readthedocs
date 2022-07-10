Usage
=====

.. _run:

Triomix command line
------------

By default, TrioMix uses the parental genotypes to infer the intrafamilial contamination level in the child. The basic command line of using TrioMix is the following:

.. code-block:: console

   $ python triomix.py -f father.bam -m mother.bam -c child.bam -r reference.fasta

Triomix command line with common SNP only
------------

Using a pre-selected list of common SNP would speed up the total runtime of TrioMix as the computation is limited to those regions instead of the entire genome. TrioMix provides a list of common ``GRCh38`` and ``GRCh37`` SNPs selected from the GnomAD database. These two files are found in the `github <https://github.com/cjyoon/triomix/tree/master/common_snp/>`_ folder.  A ``-s`` argument specifies the SNP database that can be used. User can provide one's own set of SNP in BED format.


.. code-block:: console

   $ python triomix.py -f father.bam -m mother.bam -c child.bam -r reference.fasta -s common_snps/grch38_common_snps.bed.gz



Triomix with verifybamID2
------------
``verifyBamID2`` is a robust tool that detects contamination from unrelated individuals. ``verifyBamID2`` can be run within TrioMix by adding ``--vbid [verifybamid resource file path]``. This will run ``verifybamID2`` within Triomix for all three family members in the trio. 

.. code-block:: console

   $ python triomix.py -f father.bam -m mother.bam -c child.bam -r reference.fasta -s common_snps/grch38_common_snps.bed.gz --vbid vbid/grch38




Triomix detection of parent contaminated by child
------------
To detect contamination in the parent by the child's DNA, ``--parent`` option can be used.


.. code-block:: console

   $ python triomix.py -f father.bam -m mother.bam -c child.bam -r reference.fasta -s common_snps/grch38_common_snps.bed.gz --parent


