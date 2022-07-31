Usage
=====

.. _run:

Basic Triomix command line: Detection of intrafamilial contamination in the offspring
------------

By default, TrioMix uses the parental genotypes (*GroupA, B, C SNPs*) to infer the intrafamilial contamination level in the child. The basic command line of using TrioMix is the following:

.. code-block:: console

   $ triomix -f father.bam -m mother.bam -c child.bam -r reference.fasta

   

.. code-block:: console
$ triomix -h
usage: triomix [-h] [--version] -f FATHER -m MOTHER -c CHILD -r REFERENCE [-s SNP] [-t THREAD] [-o OUTPUT_DIR]
               [-p PREFIX] [--runmode {single,joint,all}] [-u {0,1}] [--parent] [-d DOWNSAMPLE]

optional arguments:
  -h, --help            show this help message and exit
  --version             show program's version number and exit
  -f FATHER, --father FATHER
                        Father's BAM or CRAM file
  -m MOTHER, --mother MOTHER
                        Mother's BAM or CRAM file
  -c CHILD, --child CHILD
                        Child's BAM or CRAM file
  -r REFERENCE, --reference REFERENCE
                        Reference FASTA file
  -s SNP, --snp SNP     Optional list of SNP sites as a BED (or BED.gz) file
  -t THREAD, --thread THREAD
                        Multithread to utilize. Default=1
  -o OUTPUT_DIR, --output_dir OUTPUT_DIR
                        Output directory. Default=current working directory
  -p PREFIX, --prefix PREFIX
                        prefix for the output file. If not specified, will use the SM tag from the child bam's
                        header
  --runmode {single,joint,all}
                        Runmode for mle.R script. 'single' assumes only 1 contamination source within family.
                        'joint' calculates the fraction of all family members jointly. 'all' runs both modes.
                        Default=all
  -u {0,1}, --upd {0,1}
                        0: mle will filter out vaf=0 or 1 in sites where parental genotypes are homo-ref + homo-alt
                        (GroupA SNPs) 1: mle will identify UPDs which appears as contamination. Default=1
  --parent              Run detection of parental DNA contamination with child's DNA
  -d DOWNSAMPLE, --downsample DOWNSAMPLE
                        Downsampling for plotting.

Triomix command line with common SNP only
------------

Using a pre-selected list of common SNP would speed up the total runtime of TrioMix as the computation is limited to those regions instead of the entire genome. TrioMix provides a list of common ``GRCh38`` and ``GRCh37`` SNPs selected from the GnomAD database. These two files are included in the github repository as a `common_snp <https://github.com/cjyoon/triomix/tree/master/common_snp/>`_ folder.  A ``-s`` argument specifies the SNP database that can be used. User can provide one's own set of SNP in BED format.


.. code-block:: console

   $ triomix -f father.bam -m mother.bam -c child.bam -r reference.fasta -s common_snps/grch38_common_snps.bed.gz


Other optional arguments
------------




Default output files
------------
Triomix produces several output files files. 


``*.counts``: contains the position of the SNP loci in either GroupA, B, or C. Contains the read depths, alternative read counts for the trios. In addition, based on the parental genotype, will determine whether the child inherited the SNP from the father (F) or the mother (M). This file is used as the input for ``mle.R`` which estimates the contamination level using maximum likelihood estimation. 


``*.counts.summary.tsv``: contains the final estimated values of contamination from various sources. 


``*.homoalt.segements``: 


``*.summary``: contains the final results of ``triomix``. Detailed information on each column is as follows.



Triomix with whole-exome sequencing
------------
TrioMix can be used with whole-exome sequencing. In this case, we recommend running the command without the ``-s common_snp/common_snps.bed.gz``  to capture rare SNPs as well. This increases the overall number of SNPs while having minimal effect on the computational time due to smaller target in the exome sequeincing. For plotting, using ``-d 1`` is recommended to capture all data points in the plot without downsampling.

.. code-block:: console

   $ triomix -f father.bam -m mother.bam -c child.bam -r reference.fasta -d 1


Detection of intrafamilial contamination in the parent (i.e. parent DNA contamminated by child, or by another parent)
------------
To detect intrafamilial DNA contamination in the parent, ``--parent`` option can be used. This will use *GroupD SNPs* (where offspring's genotype is *homo-alt*) to detect the offspring DNA contaminating in the parents. 


.. code-block:: console

   $ triomix -f father.bam -m mother.bam -c child.bam -r reference.fasta -s common_snps/grch38_common_snps.bed.gz --parent

Additional output generated with ``--parent`` 
------------
``*.parent.counts``
``*.parent.counts.summary.tsv``



Running TrioMix with a docker image
------------
Following example demonstrates how docker image can be used for runnint TrioMix.

.. code-block:: console

   $ docker run -t -d  -v /home/ubuntu/data:/data -v /home/ubuntu/results:/results:rw -v /home/ubuntu/data/sib25/:/data/sib25/ --name triomix_local cjyoon/triomix:v1.4
   $ docker exec -it triomix_local triomix -f /data/M008_father.bam -m /data/M008_mother.bam -c /data/sib25/familymix.bam -r /data/Homo_sapiens_assembly38.fasta -t 10 -o results -s /tools/triomix/common_snp/grch38_common_snp.bed.gz


