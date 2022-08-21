Plots
=====

Here are some real case example plots from TrioMix. 

.. _plots:


Normal male offspring, uncontaminated 
------------
.. image:: images/normal_male.plot.jpg
This is an example of SNP VAFs in a male offspring without contamination. Note the drop in depth and homozygosity of chrX. 


Normal female offspring, uncontaminated 
------------
.. image:: images/normal_female.plot.jpg
This is an example of SNP VAFs in a female offspring without contamination. Note that there is no paternal GroupB SNP on chrX since father only has one copy of chrX and cannot have heterozygous SNPs.



Uniparental disomy
------------
.. image:: images/upid_example.jpg
Paternal uniparental isodisomy (UPiD) of chr4 is shown. Homozygosity of GroupA SNPs suggests the presence of uniparental disomy. Homozygosity of GroupB SNPs further suggests uniparental isodisomy (UPiD). 


Chimerism (from a sibling)
------------
.. image:: images/chimera_example.jpg
The meiotic recombination pattern between the two sibling zygotes are shown as segmental VAF patterns in GroupB SNPs. In this example TrioMix quantified the ratio between the two zygotes of the chimera 22%:78%. 


Maternal contamination in a placenta biopsy 
------------
.. image:: images/placenta_maternal_contam_example.jpg
Maternal blood can contaminate the fetal portions of the placenta biopsy. Maternal GroupA VAFs are increased (mean VAF=0.53) and paternal GroupA VAFs are decreased (mean VAF=0.47). In GroupB, additional non-zero low level VAFs are seen only from the mother which suggests DNA contamination originating from the mother. In this example, TrioMix quantified that there is 6.6% maternal DNA contamination in the placenta biopsy. 


Sample swap (father <-> offspring)
------------
.. image:: images/father_proband_swap.counts.plot.jpg

Sample swap between the father and offspring would lead to no GroupA SNPs since a offspring and another parent can both be homozygous for a different allele at the same time (i.e. offspring: *homo-alt*, father: *homo-ref*). Thus, there is no GroupA variants. For GroupB SNPs, if the offspring is a *het* genotype, then the father can be a *het* or *homo-alt* genotype. Thus a *homo-alt* (VAF=1) is seen in GroupB in the parent that is swapped with an offspring.


Sample swap (mother <-> offspring)
------------
.. image:: images/mother_proband_swap.counts.plot.jpg

Sample swap between the mother and offspring would lead to no GroupA SNPs since a offspring and another parent can both be homozygous for a different allele at the same time (i.e. offspring: *homo-alt*, mother: *homo-ref*). Thus, there is no GroupA variants. For GroupB SNPs, if the offspring is a *het* genotype, then the mother can be a *het* or *homo-alt* genotype. Thus a *homo-alt* (VAF=1) is seen in GroupB in the parent that is swapped with an offspring.


Sample swap (father <-> mother)
------------
.. image:: images/father_mother_swap.counts.plot.jpg

In the absence of parent sample swap, GroupB is only seen with maternal SNP in chrX since the requirement for GroupB is heterozygous in that parent. For the father with XY genotype, therefore, GroupB SNP is not available. Thus, if the two parents are swapped, 'paternal' chrX GroupB SNPs will be observed instead of 'maternal' chrX GroupB.
