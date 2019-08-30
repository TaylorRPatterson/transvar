*************************
Genomic level annotation
*************************

Annotation from genomic level is handled by the `ganno` subcommand in TransVar.

Short genomic regions
###########################

To annotate a short genomic region in a gene,

.. code:: bash

   $ transvar ganno --ccds -i 'chr3:g.178936091_178936192'

outputs

::

   chr3:g.178936091_178936192	CCDS43171.1 (protein_coding)	PIK3CA	+
      chr3:g.178936091_178936192/c.1633_1664+70/p.E545_R555	from_[cds_in_exon_9]_to_[intron_between_exon_9_and_10]
      C2=donor_splice_site_on_exon_9_at_chr3:178936123_included;start_codon=1789360
      91-178936092-178936093;end_codon=178936121-178936122-178936984;source=CCDS

	
Results indicates the beginning position is at coding region while ending position is at intronic region (c.1633_1664+70). Note that there is no consequence label (`CSQN` tag) when performing a region annotation (instead of a variant).

For intergenic sites, TransVar also reports the identity and distance to the gene upstream and downstream. For example, `chr6:116991832` is simply annotated as intergenic in the original annotation. TransVar reveals that it is 1,875 bp downstream to ZUFSP and 10,518 bp upstream to KPNA5 showing a vicinity to the gene ZUFSP. There is no limit in the reported distance. If a site is at the end of the chromosome, TransVar is able to report the distance to the telomere.

Long genomic regions
##########################

.. code:: bash

   $ transvar ganno -i 'chr19:g.41978629_41983350' --ensembl --refversion mm10

::

   chr19:g.41978629_41983350	ENSMUST00000167927 (nonsense_mediated_decay),ENSMUST00000026170 (protein_coding)	MMS19,UBTD1	-,+
      chr19:g.41978629_41983350/./.	from_[intron_between_exon_1_and_2;MMS19]_to_[intron_between_exon_1_and_2;UBTD1]
      .
   chr19:g.41978629_41983350	ENSMUST00000171561 (protein_coding),ENSMUST00000026170 (protein_coding)	MMS19,UBTD1	-,+
      chr19:g.41978629_41983350/./.	from_[intron_between_exon_1_and_2;MMS19]_to_[intron_between_exon_1_and_2;UBTD1]
      .
   chr19:g.41978629_41983350	ENSMUST00000163398 (nonsense_mediated_decay),ENSMUST00000026170 (protein_coding)	MMS19,UBTD1	-,+
      chr19:g.41978629_41983350/./.	from_[intron_between_exon_1_and_2;MMS19]_to_[intron_between_exon_1_and_2;UBTD1]
      .
   chr19:g.41978629_41983350	ENSMUST00000164776 (nonsense_mediated_decay),ENSMUST00000026170 (protein_coding)	MMS19,UBTD1	-,+
      chr19:g.41978629_41983350/./.	from_[intron_between_exon_1_and_2;MMS19]_to_[intron_between_exon_1_and_2;UBTD1]
      .
   chr19:g.41978629_41983350	ENSMUST00000026168 (protein_coding),ENSMUST00000026170 (protein_coding)	MMS19,UBTD1	-,+
      chr19:g.41978629_41983350/./.	from_[intron_between_exon_1_and_2;MMS19]_to_[intron_between_exon_1_and_2;UBTD1]
      .
   chr19:g.41978629_41983350	ENSMUST00000171755 (retained_intron),ENSMUST00000026170 (protein_coding)	MMS19,UBTD1	-,+
      chr19:g.41978629_41983350/./.	from_[intron_between_exon_1_and_2;MMS19]_to_[intron_between_exon_1_and_2;UBTD1]
      .
   chr19:g.41978629_41983350	ENSMUST00000169775 (nonsense_mediated_decay),ENSMUST00000026170 (protein_coding)	MMS19,UBTD1	-,+
      chr19:g.41978629_41983350/./.	from_[intron_between_exon_1_and_2;MMS19]_to_[intron_between_exon_1_and_2;UBTD1]
      .
   chr19:g.41978629_41983350	ENSMUST00000168484 (nonsense_mediated_decay),ENSMUST00000026170 (protein_coding)	MMS19,UBTD1	-,+
      chr19:g.41978629_41983350/./.	from_[intron_between_exon_1_and_2;MMS19]_to_[intron_between_exon_1_and_2;UBTD1]
      .

Results indicates a 4721 bp region spanning the promoters of two closely located, opposite-oriented genes MMS19 and UBTD1. The starting point and ending point are situated in the first introns of the two genes.

.. code:: bash

   $ transvar ganno -i '9:g.133750356_137990357' --ccds

outputs

::

   9:g.133750356_137990357	CCDS35165.1 (protein_coding),CCDS6986.1 (protein_coding)	ABL1,OLFM1	+,+
      chr9:g.133750356_137990357/./.	from_[cds_in_exon_7;ABL1]_to_[intron_between_exon_4_and_5;OLFM1]_spanning_[51_genes]
      .
   9:g.133750356_137990357	CCDS35166.1 (protein_coding),CCDS6986.1 (protein_coding)	ABL1,OLFM1	+,+
      chr9:g.133750356_137990357/./.	from_[cds_in_exon_7;ABL1]_to_[intron_between_exon_4_and_5;OLFM1]_spanning_[51_genes]
      .

The result indicates that the region span 53 genes. The beginning of the region resides in the coding sequence of ABL1, c.1187A and the ending region resides in the intronic region of OLFM1, c.622+6C. 2 different usage of transcripts in annotating the starting position is represented in two lines, each line corresponding to a combination of transcript usage.
This annotation not only shows the coverage of the region, also reveals the fine structure of the boundary.

In another example, where the ending position exceeds the length of the chromosome, TransVar truncates the region and outputs upstream and downstream information of the ending position.

.. code:: bash

   $ transvar ganno -i '9:g.133750356_1337503570' --ccds

outputs

::

   9:g.133750356_1337503570	CCDS35165.1 (protein_coding),	ABL1,	+
      chr9:g.133750356_141213431/./.	from_[cds_in_exon_7;ABL1]_to_[intergenic_between_EHMT1(484026_bp_downstream)_and_3'-telomere(0_bp)]_spanning_[136_genes]
      .
   9:g.133750356_1337503570	CCDS35166.1 (protein_coding),	ABL1,	+
      chr9:g.133750356_141213431/./.	from_[cds_in_exon_7;ABL1]_to_[intergenic_between_EHMT1(484026_bp_downstream)_and_3'-telomere(0_bp)]_spanning_[136_genes]
      .

Genomic variant
#################

Single nucleotide variation (SNV)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This is the forward annotation


.. code:: bash

   $ transvar ganno --ccds -i 'chr3:g.178936091G>A'

outputs

::

   chr3:g.178936091G>A	CCDS43171.1 (protein_coding)	PIK3CA	+
      chr3:g.178936091G>A/c.1633G>A/p.E545K	inside_[cds_in_exon_9]
      CSQN=Missense;dbsnp=rs104886003(chr3:178936091G>A);codon_pos=178936091-178936
      092-178936093;ref_codon_seq=GAG;source=CCDS

Another example:

.. code:: bash

   $ transvar ganno -i "chr9:g.135782704C>G" --ccds

outputs

::

   chr9:g.135782704C>G	CCDS55350.1 (protein_coding)	TSC1	-
      chr9:g.135782704C>G/c.1164G>C/p.L388L	inside_[cds_in_exon_10]
      CSQN=Synonymous;dbsnp=rs770692313(chr9:135782704C>G);codon_pos=135782704-1357
      82705-135782706;ref_codon_seq=CTG;source=CCDS
   chr9:g.135782704C>G	CCDS6956.1 (protein_coding)	TSC1	-
      chr9:g.135782704C>G/c.1317G>C/p.L439L	inside_[cds_in_exon_11]
      CSQN=Synonymous;dbsnp=rs770692313(chr9:135782704C>G);codon_pos=135782704-1357
      82705-135782706;ref_codon_seq=CTG;source=CCDS

and a nonsense mutation:

.. code:: bash

   $ transvar ganno -i 'chr1:g.115256530G>A' --ensembl

outputs

::

   chr1:g.115256530G>A	ENST00000369535 (protein_coding)	NRAS	-
      chr1:g.115256530G>A/c.181C>T/p.Q61*	inside_[cds_in_exon_3]
      CSQN=Nonsense;codon_pos=115256528-115256529-115256530;ref_codon_seq=CAA;alias
      es=ENSP00000358548;source=Ensembl

CSQN fields indicates a nonsense mutation.

Deletions
^^^^^^^^^^^^

A frameshift deletion

.. code:: bash

   $ transvar ganno -i "chr2:g.234183368_234183380del" --ccds

outputs

::

   chr2:g.234183368_234183380del	CCDS2502.2 (protein_coding)	ATG16L1	+
      chr2:g.234183368_234183380del13/c.841_853del13/p.T281Lfs*5	inside_[cds_in_exon_8]
      CSQN=Frameshift;left_align_gDNA=g.234183367_234183379del13;unaligned_gDNA=g.2
      34183368_234183380del13;left_align_cDNA=c.840_852del13;unalign_cDNA=c.841_853
      del13;source=CCDS
   chr2:g.234183368_234183380del	CCDS2503.2 (protein_coding)	ATG16L1	+
      chr2:g.234183368_234183380del13/c.898_910del13/p.T300Lfs*5	inside_[cds_in_exon_9]
      CSQN=Frameshift;left_align_gDNA=g.234183367_234183379del13;unaligned_gDNA=g.2
      34183368_234183380del13;left_align_cDNA=c.897_909del13;unalign_cDNA=c.898_910
      del13;source=CCDS
   chr2:g.234183368_234183380del	CCDS54438.1 (protein_coding)	ATG16L1	+
      chr2:g.234183368_234183380del13/c.409_421del13/p.T137Lfs*5	inside_[cds_in_exon_5]
      CSQN=Frameshift;left_align_gDNA=g.234183367_234183379del13;unaligned_gDNA=g.2
      34183368_234183380del13;left_align_cDNA=c.408_420del13;unalign_cDNA=c.409_421
      del13;source=CCDS

Note the difference between left-aligned identifier and the right aligned identifier.

An in-frame deletion

.. code:: bash

   $ transvar ganno -i "chr2:g.234183368_234183379del" --ccds

outputs

::

   chr2:g.234183368_234183379del	CCDS2502.2 (protein_coding)	ATG16L1	+
      chr2:g.234183368_234183379del12/c.841_852del12/p.T281_G284delTHPG	inside_[cds_in_exon_8]
      CSQN=InFrameDeletion;left_align_gDNA=g.234183367_234183378del12;unaligned_gDN
      A=g.234183368_234183379del12;left_align_cDNA=c.840_851del12;unalign_cDNA=c.84
      1_852del12;left_align_protein=p.T281_G284delTHPG;unalign_protein=p.T281_G284d
      elTHPG;source=CCDS
   chr2:g.234183368_234183379del	CCDS2503.2 (protein_coding)	ATG16L1	+
      chr2:g.234183368_234183379del12/c.898_909del12/p.T300_G303delTHPG	inside_[cds_in_exon_9]
      CSQN=InFrameDeletion;left_align_gDNA=g.234183367_234183378del12;unaligned_gDN
      A=g.234183368_234183379del12;left_align_cDNA=c.897_908del12;unalign_cDNA=c.89
      8_909del12;left_align_protein=p.T300_G303delTHPG;unalign_protein=p.T300_G303d
      elTHPG;source=CCDS
   chr2:g.234183368_234183379del	CCDS54438.1 (protein_coding)	ATG16L1	+
      chr2:g.234183368_234183379del12/c.409_420del12/p.T137_G140delTHPG	inside_[cds_in_exon_5]
      CSQN=InFrameDeletion;left_align_gDNA=g.234183367_234183378del12;unaligned_gDN
      A=g.234183368_234183379del12;left_align_cDNA=c.408_419del12;unalign_cDNA=c.40
      9_420del12;left_align_protein=p.T137_G140delTHPG;unalign_protein=p.T137_G140d
      elTHPG;source=CCDS

Another example

.. code:: bash

   $ transvar ganno --ccds -i 'chr12:g.53703425_53703427del'

outputs

::

   chr12:g.53703425_53703427del	CCDS53797.1 (protein_coding)	AAAS	-
      chr12:g.53703427_53703429delCCC/c.670_672delGGG/p.G224delG	inside_[cds_in_exon_7]
      CSQN=InFrameDeletion;left_align_gDNA=g.53703424_53703426delCCC;unaligned_gDNA
      =g.53703425_53703427delCCC;left_align_cDNA=c.667_669delGGG;unalign_cDNA=c.669
      _671delGGG;left_align_protein=p.G223delG;unalign_protein=p.G223delG;source=CC
      DS
   chr12:g.53703425_53703427del	CCDS8856.1 (protein_coding)	AAAS	-
      chr12:g.53703427_53703429delCCC/c.769_771delGGG/p.G257delG	inside_[cds_in_exon_8]
      CSQN=InFrameDeletion;left_align_gDNA=g.53703424_53703426delCCC;unaligned_gDNA
      =g.53703425_53703427delCCC;left_align_cDNA=c.766_768delGGG;unalign_cDNA=c.768
      _770delGGG;left_align_protein=p.G256delG;unalign_protein=p.G256delG;source=CC
      DS

Note the difference between left and right-aligned identifiers on both protein level and cDNA level.

An in-frame out-of-phase deletion

.. code:: bash

   $ transvar ganno -i "chr2:g.234183372_234183383del" --ccds

outputs

::

   chr2:g.234183372_234183383del	CCDS2502.2 (protein_coding)	ATG16L1	+
      chr2:g.234183372_234183383del12/c.845_856del12/p.H282_G286delinsR	inside_[cds_in_exon_8]
      CSQN=MultiAAMissense;left_align_gDNA=g.234183372_234183383del12;unaligned_gDN
      A=g.234183372_234183383del12;left_align_cDNA=c.845_856del12;unalign_cDNA=c.84
      5_856del12;source=CCDS
   chr2:g.234183372_234183383del	CCDS2503.2 (protein_coding)	ATG16L1	+
      chr2:g.234183372_234183383del12/c.902_913del12/p.H301_G305delinsR	inside_[cds_in_exon_9]
      CSQN=MultiAAMissense;left_align_gDNA=g.234183372_234183383del12;unaligned_gDN
      A=g.234183372_234183383del12;left_align_cDNA=c.902_913del12;unalign_cDNA=c.90
      2_913del12;source=CCDS
   chr2:g.234183372_234183383del	CCDS54438.1 (protein_coding)	ATG16L1	+
      chr2:g.234183372_234183383del12/c.413_424del12/p.H138_G142delinsR	inside_[cds_in_exon_5]
      CSQN=MultiAAMissense;left_align_gDNA=g.234183372_234183383del12;unaligned_gDN
      A=g.234183372_234183383del12;left_align_cDNA=c.413_424del12;unalign_cDNA=c.41
      3_424del12;source=CCDS

Insertions
^^^^^^^^^^^^^

An in-frame insertion of three nucleotides

.. code:: bash

   $ transvar ganno -i 'chr2:g.69741762_69741763insTGC' --ccds

outputs

::

   chr2:g.69741762_69741763insTGC	CCDS1893.2 (protein_coding)	AAK1	-
      chr2:g.69741780_69741782dupCTG/c.1614_1616dupGCA/p.Q546dupQ	inside_[cds_in_exon_12]
      CSQN=InFrameInsertion;left_align_gDNA=g.69741762_69741763insTGC;unalign_gDNA=
      g.69741762_69741763insTGC;left_align_cDNA=c.1596_1597insCAG;unalign_cDNA=c.16
      14_1616dupGCA;left_align_protein=p.Y532_Q533insQ;unalign_protein=p.Q539dupQ;p
      hase=2;source=CCDS

Note the proper right-alignment of protein level insertion Q. The left-aligned identifier is also given in the `LEFTALN` field.

A frame-shift insertion of two nucleotides

.. code:: bash

   $ transvar ganno -i 'chr7:g.121753754_121753755insCA' --ccds

outputs

::

   chr7:g.121753754_121753755insCA	CCDS5783.1 (protein_coding)	AASS	-
      chr7:g.121753754_121753755insCA/c.1064_1065insGT/p.I355Mfs*10	inside_[cds_in_exon_9]
      CSQN=Frameshift;left_align_gDNA=g.121753753_121753754insAC;unalign_gDNA=g.121
      753754_121753755insCA;left_align_cDNA=c.1063_1064insTG;unalign_cDNA=c.1063_10
      64insTG;source=CCDS

.. code:: bash

   $ transvar ganno -i 'chr17:g.79093270_79093271insGGGCGT' --ccds

outputs

::

   chr17:g.79093270_79093271insGGGCGT	CCDS45807.1 (protein_coding)	AATK	-
      chr17:g.79093282_79093287dupTGGGCG/c.3988_3993dupACGCCC/p.T1330_P1331dupTP	inside_[cds_in_exon_13]
      CSQN=InFrameInsertion;left_align_gDNA=g.79093270_79093271insGGGCGT;unalign_gD
      NA=g.79093270_79093271insGGGCGT;left_align_cDNA=c.3976_3977insCGCCCA;unalign_
      cDNA=c.3988_3993dupACGCCC;left_align_protein=p.A1326_P1327insPT;unalign_prote
      in=p.T1330_P1331dupTP;phase=0;source=CCDS

Notice the difference in the inserted sequence when left-alignment and right-alignment conventions are followed.

A frame-shift insertion of one nucleotides in a homopolymer

.. code:: bash

   $ transvar ganno -i 'chr7:g.117230474_117230475insA' --ccds

outputs

::

   chr7:g.117230474_117230475insA	CCDS5773.1 (protein_coding)	CFTR	+
      chr7:g.117230479dupA/c.1752dupA/p.E585Rfs*4	inside_[cds_in_exon_13]
      CSQN=Frameshift;left_align_gDNA=g.117230474_117230475insA;unalign_gDNA=g.1172
      30474_117230475insA;left_align_cDNA=c.1747_1748insA;unalign_cDNA=c.1747_1748i
      nsA;source=CCDS

Notice the right alignment of cDNA level insertion and the left alignment reported as additional information.

A in-frame, in-phase insertion

.. code:: bash

   $ transvar ganno -i 'chr12:g.109702119_109702120insACC' --ccds

::

   chr12:g.109702119_109702120insACC	CCDS31898.1 (protein_coding)	ACACB	+
      chr12:g.109702119_109702120insACC/c.6870_6871insACC/p.Y2290_H2291insT	inside_[cds_in_exon_49]
      CSQN=InFrameInsertion;left_align_gDNA=g.109702118_109702119insCAC;unalign_gDN
      A=g.109702119_109702120insACC;left_align_cDNA=c.6869_6870insCAC;unalign_cDNA=
      c.6870_6871insACC;left_align_protein=p.Y2290_H2291insT;unalign_protein=p.Y229
      0_H2291insT;phase=0;source=CCDS


Block substitutions
^^^^^^^^^^^^^^^^^^^^^^

A block-substitution that results in a frameshift.

.. code:: bash

   $ transvar ganno -i 'chr10:g.27329002_27329002delinsAT' --ccds

::

   chr10:g.27329002_27329002delinsAT	CCDS41499.1 (protein_coding)	ANKRD26	-
      chr10:g.27329009dupT/c.2266dupA/p.M756Nfs*6	inside_[cds_in_exon_21]
      CSQN=Frameshift;left_align_gDNA=g.27329002_27329003insT;unalign_gDNA=g.273290
      02_27329003insT;left_align_cDNA=c.2259_2260insA;unalign_cDNA=c.2266dupA;sourc
      e=CCDS

A block-substitution that is in-frame,

.. code:: bash

   $ transvar ganno -i 'chr10:g.52595929_52595930delinsAA' --ccds

::

   chr10:g.52595929_52595930delinsAA	CCDS7243.1 (protein_coding)	A1CF	-
      chr10:g.52595929_52595930delinsAA/c.532_533delinsTT/p.P178L	inside_[cds_in_exon_4]
      CSQN=Missense;codon_cDNA=532-533-534;source=CCDS
   chr10:g.52595929_52595930delinsAA	CCDS7241.1 (protein_coding)	A1CF	-
      chr10:g.52595929_52595930delinsAA/c.508_509delinsTT/p.P170L	inside_[cds_in_exon_4]
      CSQN=Missense;codon_cDNA=508-509-510;source=CCDS
   chr10:g.52595929_52595930delinsAA	CCDS7242.1 (protein_coding)	A1CF	-
      chr10:g.52595929_52595930delinsAA/c.508_509delinsTT/p.P170L	inside_[cds_in_exon_4]
      CSQN=Missense;codon_cDNA=508-509-510;source=CCDS


Promoter region
##################

One can define the promoter boundary through the `--prombeg` and `--promend` option. Default promoter region is defined from 1000bp upstream of the transcription start site to the transcription start site. One could customize this setting to e.g., [-1000bp, 2000bp] by

.. code:: bash

   $ transvar ganno -i 'chr19:g.41978629_41980350' --ensembl --prombeg 2000 --promend 1000 --refversion mm10

::

   chr19:g.41978629_41980350	ENSMUST00000167927 (nonsense_mediated_decay)	MMS19	-
      chr19:g.41978629_41980350/c.115+649_115+2370/.	inside_[intron_between_exon_1_and_2]
      promoter_region_of_[MMS19]_overlaping_237_bp(13.76%);aliases=ENSMUSP000001324
      83;source=Ensembl
   chr19:g.41978629_41980350	ENSMUST00000171561 (protein_coding)	MMS19	-
      chr19:g.41978629_41980350/c.115+649_115+2370/.	inside_[intron_between_exon_1_and_2]
      promoter_region_of_[MMS19]_overlaping_194_bp(11.27%);aliases=ENSMUSP000001309
      00;source=Ensembl
   chr19:g.41978629_41980350	ENSMUST00000163398 (nonsense_mediated_decay)	MMS19	-
      chr19:g.41978629_41980350/c.115+649_115+2370/.	inside_[intron_between_exon_1_and_2]
      promoter_region_of_[MMS19]_overlaping_234_bp(13.59%);aliases=ENSMUSP000001268
      64;source=Ensembl
   chr19:g.41978629_41980350	ENSMUST00000164776 (nonsense_mediated_decay)	MMS19	-
      chr19:g.41978629_41980350/c.115+649_115+2370/.	inside_[intron_between_exon_1_and_2]
      promoter_region_of_[MMS19]_overlaping_215_bp(12.49%);aliases=ENSMUSP000001294
      78;source=Ensembl
   chr19:g.41978629_41980350	ENSMUST00000026168 (protein_coding)	MMS19	-
      chr19:g.41978629_41980350/c.115+649_115+2370/.	inside_[intron_between_exon_1_and_2]
      promoter_region_of_[MMS19]_overlaping_219_bp(12.72%);aliases=ENSMUSP000000261
      68;source=Ensembl
   chr19:g.41978629_41980350	ENSMUST00000171755 (retained_intron)	MMS19	-
      chr19:g.41978629_41980350/c.141+649_141+2370/.	inside_[intron_between_exon_1_and_2]
      promoter_region_of_[MMS19]_overlaping_212_bp(12.31%);source=Ensembl
   chr19:g.41978629_41980350	ENSMUST00000169775 (nonsense_mediated_decay)	MMS19	-
      chr19:g.41978629_41980350/c.115+649_115+2370/.	inside_[intron_between_exon_1_and_2]
      promoter_region_of_[MMS19]_overlaping_214_bp(12.43%);aliases=ENSMUSP000001282
      34;source=Ensembl
   chr19:g.41978629_41980350	ENSMUST00000168484 (nonsense_mediated_decay)	MMS19	-
      chr19:g.41978629_41980350/c.115+649_115+2370/.	inside_[intron_between_exon_1_and_2]
      promoter_region_of_[MMS19]_overlaping_221_bp(12.83%);aliases=ENSMUSP000001268
      81;source=Ensembl

The last result shows that 12-13% of the target region is inside the promoter region. The overlap is as long as ~200 base pairs.

Splice sites
################

Consider a splice donor site chr7:5568790_5568791 (a donor site, intron side by definition, reverse strand, chr7:5568792- is the exon),

The 1st exonic nucleotide before donor splice site:

.. code::

   $ transvar ganno -i 'chr7:5568792C>G' --ccds

output a exonic variation and a missense variation

::

   chr7:5568792C>G	CCDS5341.1 (protein_coding)	ACTB	-
      chr7:g.5568792C>G/c.363G>C/p.Q121H	inside_[cds_in_exon_2]
      CSQN=Missense;C2=NextToSpliceDonorOfExon2_At_chr7:5568791;codon_pos=5568792-5
      568793-5568794;ref_codon_seq=CAG;source=CCDS


The 1st nucleotide in the canonical donor splice site (intron side, this is commonly regarded as the splice site location):

.. code::

   $ transvar ganno -i 'chr7:5568791C>G' --ccds

output a splice variation

::

   chr7:5568791C>G	CCDS5341.1 (protein_coding)	ACTB	-
      chr7:g.5568791C>G/c.363+1G>C/.	inside_[intron_between_exon_2_and_3]
      CSQN=SpliceDonorSNV;C2=SpliceDonorOfExon2_At_chr7:5568791;source=CCDS


The 2nd nucleotide in the canonical donor splice site (2nd on the intron side, still considered part of the splice site):

.. code::

   $ transvar ganno -i 'chr7:5568790A>G' --ccds

output a splice variation

::

   chr7:5568790A>G	CCDS5341.1 (protein_coding)	ACTB	-
      chr7:g.5568790A>G/c.363+2T>C/.	inside_[intron_between_exon_2_and_3]
      CSQN=SpliceDonorSNV;C2=SpliceDonorOfExon2_At_chr7:5568791;source=CCDS


The 1st nucleotide downstream next to the canonical donor splice site (3rd nucleotide in the intron side, not part of the splice site):

.. code::

   $ transvar ganno -i 'chr7:5568789C>G' --ccds

output a pure intronic variation

::

   chr7:5568789C>G	CCDS5341.1 (protein_coding)	ACTB	-
      chr7:g.5568789C>G/c.363+3G>C/.	inside_[intron_between_exon_2_and_3]
      CSQN=IntronicSNV;source=CCDS


UTR region
#############

.. code:: bash

   $ transvar ganno -i 'chr2:25564781G>T' --refseq

results in a UTR-containing CSQN field

::

   chr2:25564781G>T	NM_022552.4 (protein_coding)	DNMT3A	-
      chr2:g.25564781G>T/c.1-27928C>A/.	inside_[5-UTR;noncoding_exon_1]
      CSQN=5-UTRSNV;dbxref=GeneID:1788,HGNC:2978,HPRD:04141,MIM:602769;aliases=NP_0
      72046;source=RefSeq
   chr2:25564781G>T	NM_175629.2 (protein_coding)	DNMT3A	-
      chr2:g.25564781G>T/c.1-27928C>A/.	inside_[5-UTR;intron_between_exon_1_and_2]
      CSQN=IntronicSNV;dbxref=GeneID:1788,HGNC:2978,HPRD:04141,MIM:602769;aliases=N
      P_783328;source=RefSeq
   chr2:25564781G>T	NM_175630.1 (protein_coding)	DNMT3A	-
      chr2:g.25564781G>T/c.1-27928C>A/.	inside_[5-UTR;intron_between_exon_1_and_2]
      CSQN=IntronicSNV;dbxref=GeneID:1788,HGNC:2978,HPRD:04141,MIM:602769;aliases=N
      P_783329;source=RefSeq

Non-coding RNA
####################

Given Ensembl, GENCODE or RefSeq database, one could annotate non-coding transcripts such as lncRNA.
E.g.,

.. code:: bash

   $ transvar ganno --gencode -i 'chr1:g.3985200_3985300' --refversion mm10

results in

::

   chr1:g.3985200_3985300	ENSMUST00000194643.1 (lincRNA)	GM37381	-
      chr1:g.3985200_3985300/c.121_221/.	inside_[noncoding_exon_2]
      source=GENCODE
   chr1:g.3985200_3985300	ENSMUST00000192427.1 (lincRNA)	GM37381	-
      chr1:g.3985200_3985300/c.685_785/.	inside_[noncoding_exon_1]
      source=GENCODE

or

.. code:: bash

   $ transvar ganno --refseq -i 'chr14:g.20568338_20569581' --refversion mm10

results in

::

   chr14:g.20568338_20569581	NR_033571.1 (lncRNA)	1810062O18RIK	+
      chr14:g.20568338_20569581/c.260-1532_260-289/.	inside_[intron_between_exon_4_and_5]
      dbxref=GeneID:75602,MGI:MGI:1922852;source=RefSeq
   chr14:g.20568338_20569581	NM_030180.2 (protein_coding)	USP54	-
      chr14:g.20568338_20569581/c.2188+667_2188+1910/.	inside_[intron_between_exon_15_and_16]
      dbxref=GeneID:78787,MGI:MGI:1926037;aliases=NP_084456;source=RefSeq
   chr14:g.20568338_20569581	XM_006519703.3 (protein_coding)	USP54	-
      chr14:g.20568338_20569581/c.2359+667_2359+1910/.	inside_[intron_between_exon_16_and_17]
      dbxref=GeneID:78787,MGI:MGI:1926037;aliases=XP_006519766;source=RefSeq
   chr14:g.20568338_20569581	XM_011245226.2 (protein_coding)	USP54	-
      chr14:g.20568338_20569581/c.1972+667_1972+1910/.	inside_[intron_between_exon_13_and_14]
      dbxref=GeneID:78787,MGI:MGI:1926037;aliases=XP_011243528;source=RefSeq
   chr14:g.20568338_20569581	XM_011245225.2 (protein_coding)	USP54	-
      chr14:g.20568338_20569581/c.2359+667_2359+1910/.	inside_[intron_between_exon_16_and_17]
      dbxref=GeneID:78787,MGI:MGI:1926037;aliases=XP_011243527;source=RefSeq
   chr14:g.20568338_20569581	XM_006519705.3 (protein_coding)	USP54	-
      chr14:g.20568338_20569581/c.2188+667_2188+1910/.	inside_[intron_between_exon_15_and_16]
      dbxref=GeneID:78787,MGI:MGI:1926037;aliases=XP_006519768;source=RefSeq
   chr14:g.20568338_20569581	XM_011245227.2 (protein_coding)	USP54	-
      chr14:g.20568338_20569581/c.2359+667_2359+1910/.	inside_[intron_between_exon_16_and_17]
      dbxref=GeneID:78787,MGI:MGI:1926037;aliases=XP_011243529;source=RefSeq
   chr14:g.20568338_20569581	XM_017316224.1 (protein_coding)	USP54	-
      chr14:g.20568338_20569581/c.2359+667_2359+1910/.	inside_[intron_between_exon_16_and_17]
      dbxref=GeneID:78787,MGI:MGI:1926037;aliases=XP_017171713;source=RefSeq

or using Ensembl

.. code:: bash

   $ transvar ganno --ensembl -i 'chr1:g.29560_29570'

results in

::

   chr1:g.29560_29570	ENST00000488147 (unprocessed_pseudogene)	WASH7P	-
      chr1:g.29560_29570/c.1_11/.	inside_[noncoding_exon_1]
      promoter_region_of_[WASH7P]_overlaping_1_bp(9.09%);source=Ensembl
   chr1:g.29560_29570	ENST00000538476 (unprocessed_pseudogene)	WASH7P	-
      chr1:g.29560_29570/c.237_247/.	inside_[noncoding_exon_1]
      source=Ensembl
   chr1:g.29560_29570	ENST00000473358 (lincRNA)	MIR1302-10	+
      chr1:g.29560_29570/c.7_17/.	inside_[noncoding_exon_1]
      source=Ensembl

Coding Start and Stop
#######################

The following illustrates deletion of a coding start.

.. code:: bash

   $ transvar ganno -i "chr7:g.5569279_5569288del" --ccds

results in

::

   chr7:g.5569279_5569288del	CCDS5341.1 (protein_coding)	ACTB	-
      chr7:g.5569279_5569288delCATCATCCAT/c.3_12delGGATGATGAT/.	inside_[cds_in_exon_1]
      CSQN=CdsStartDeletion;left_align_gDNA=g.5569277_5569286delATCATCATCC;unaligne
      d_gDNA=g.5569279_5569288delCATCATCCAT;left_align_cDNA=c.1_10delATGGATGATG;una
      lign_cDNA=c.1_10delATGGATGATG;cds_start_at_chr7:5569288_lost;source=CCDS

Deletion of a coding stop

.. code:: bash

   $ transvar ganno -i "chr7:g.5567379_5567380del" --ccds

results in


Coding start loss due to SNP

.. code:: bash

   $ transvar ganno -i "chr7:g.5568911T>A" --refseq

results in

::

   chr7:g.5568911T>A	NM_001101.3 (protein_coding)	ACTB	-
      chr7:g.5568911T>A/c.244A>T/p.M82L	inside_[cds_in_exon_3]
      CSQN=Missense;codon_pos=5568909-5568910-5568911;ref_codon_seq=ATG;dbxref=Gene
      ID:60,HGNC:132,HPRD:00032,MIM:102630;aliases=NP_001092;source=RefSeq
   chr7:g.5568911T>A	XM_005249818.1 (protein_coding)	ACTB	-
      chr7:g.5568911T>A/c.244A>T/p.M82L	inside_[cds_in_exon_3]
      CSQN=Missense;codon_pos=5568909-5568910-5568911;ref_codon_seq=ATG;dbxref=Gene
      ID:60,HGNC:132,HPRD:00032,MIM:102630;aliases=XP_005249875;source=RefSeq
   chr7:g.5568911T>A	XM_005249819.1 (protein_coding)	ACTB	-
      chr7:g.5568911T>A/c.1A>T/.	inside_[cds_in_exon_2]
      CSQN=CdsStartSNV;C2=cds_start_at_chr7:5568911;dbxref=GeneID:60,HGNC:132,HPRD:
      00032,MIM:102630;aliases=XP_005249876;source=RefSeq
   chr7:g.5568911T>A	XM_005249820.1 (protein_coding)	ACTB	-
      chr7:g.5568911T>A/c.1-564A>T/.	inside_[5-UTR;noncoding_exon_3]
      CSQN=5-UTRSNV;dbxref=GeneID:60,HGNC:132,HPRD:00032,MIM:102630;aliases=XP_0052
      49877;source=RefSeq


Coding stop loss due to SNP

.. code:: bash

   $ transvar ganno -i "chr7:g.5567379C>A" --refseq

results in

::

   chr7:g.5567379C>A	NM_001101.3 (protein_coding)	ACTB	-
      chr7:g.5567379C>A/c.1128G>T/.	inside_[cds_in_exon_6]
      CSQN=CdsStopSNV;C2=cds_end_at_chr7:5567379;dbxref=GeneID:60,HGNC:132,HPRD:000
      32,MIM:102630;aliases=NP_001092;source=RefSeq
   chr7:g.5567379C>A	XM_005249818.1 (protein_coding)	ACTB	-
      chr7:g.5567379C>A/c.1128G>T/.	inside_[cds_in_exon_6]
      CSQN=CdsStopSNV;C2=cds_end_at_chr7:5567379;dbxref=GeneID:60,HGNC:132,HPRD:000
      32,MIM:102630;aliases=XP_005249875;source=RefSeq
   chr7:g.5567379C>A	XM_005249819.1 (protein_coding)	ACTB	-
      chr7:g.5567379C>A/c.885G>T/.	inside_[cds_in_exon_5]
      CSQN=CdsStopSNV;C2=cds_end_at_chr7:5567379;dbxref=GeneID:60,HGNC:132,HPRD:000
      32,MIM:102630;aliases=XP_005249876;source=RefSeq
   chr7:g.5567379C>A	XM_005249820.1 (protein_coding)	ACTB	-
      chr7:g.5567379C>A/c.762G>T/.	inside_[cds_in_exon_7]
      CSQN=CdsStopSNV;C2=cds_end_at_chr7:5567379;dbxref=GeneID:60,HGNC:132,HPRD:000
      32,MIM:102630;aliases=XP_005249877;source=RefSeq

Batch processing
###################


To Illustrate batch processing with the following small batch input

.. code:: bash

   $ cat data/small_batch_input

::

   chr3	178936091	G	A	CCDS43171
   chr9	135782704	C	G	CCDS6956

.. code:: bash

   $ transvar ganno -l data/small_batch_input -g 1 -n 2 -r 3 -a 4 -t 5 --ccds

::

   chr3|178936091|G|A|CCDS43171	CCDS43171.1 (protein_coding)	PIK3CA	+
      chr3:g.178936091G>A/c.1633G>A/p.E545K	inside_[cds_in_exon_9]
      CSQN=Missense;dbsnp=rs104886003(chr3:178936091G>A);codon_pos=178936091-178936
      092-178936093;ref_codon_seq=GAG;source=CCDS
   chr9|135782704|C|G|CCDS6956	CCDS6956.1 (protein_coding)	TSC1	-
      chr9:g.135782704C>G/c.1317G>C/p.L439L	inside_[cds_in_exon_11]
      CSQN=Synonymous;dbsnp=rs770692313(chr9:135782704C>G);codon_pos=135782704-1357
      82705-135782706;ref_codon_seq=CTG;source=CCDS


One can also make a HGVS-like input and call

.. code:: bash

   $ cat data/small_batch_hgvs

::

   CCDS43171	chr3:g.178936091G>A
   CCDS6956	chr9:g.135782704C>G

.. code:: bash

   $ transvar ganno -l data/small_batch_hgvs -m 2 -t 1 --ccds

::

   CCDS43171|chr3:g.178936091G>A	CCDS43171.1 (protein_coding)	PIK3CA	+
      chr3:g.178936091G>A/c.1633G>A/p.E545K	inside_[cds_in_exon_9]
      CSQN=Missense;dbsnp=rs104886003(chr3:178936091G>A);codon_pos=178936091-178936
      092-178936093;ref_codon_seq=GAG;source=CCDS
   CCDS6956|chr9:g.135782704C>G	CCDS6956.1 (protein_coding)	TSC1	-
      chr9:g.135782704C>G/c.1317G>C/p.L439L	inside_[cds_in_exon_11]
      CSQN=Synonymous;dbsnp=rs770692313(chr9:135782704C>G);codon_pos=135782704-1357
      82705-135782706;ref_codon_seq=CTG;source=CCDS


The first column for transcript ID restriction is optional.
