***************************
Some additional Examples
***************************

Test --gseq argument
#######################

The optional `--gseq` append genomic sequence as extra columns (chromosome, begin, end, reference sequence and alternative sequence).


A region
^^^^^^^^^

.. code:: bash

   $ transvar panno --ccds -i 'ABCB11:p.200_400' --gseq

:: 

   ABCB11:p.200_400	CCDS46444.1 (protein_coding)	ABCB11	-
      chr2:g.169833195_169851872/c.598_1200/p.T200_K400	inside_[cds_in_exons_[6,7,8,9,10,11]]
      protein_sequence=TRF..DRK;cDNA_sequence=ACA..AAA;gDNA_sequence=TTT..TGT;sourc
      e=CCDS	chr2	169833195	TTTCCTGTCTATTGTCTCAAAAATGCTGGTGGCTGCTGCACGTCCAGTTGCAAAG
      GCTTCCAAACAAGGAGAGGCATTGCCAAGATTTAAAGCTCCTACTATGACACTGAGGAAAATCTGGACAAGGGTTCC
      TGGTGTATATTCTCCTTCATCCAGGACAAGTGTGGAGCCGTACCAGAAGGCCAGTGCATAACACAAAAAGATGAGAC
      ACCACACGAATCCAGTAAAGAATCCCATCACTATTCCTTTTCTAATTCCCCAACGCTGGGCGAACACAAGATTTTTC
      TCATACCTTTCAACCTCTCTTTTCTCACCACCAAAAGCAGCCACTGTTCTCATTGATGAAATGACTTCATCAGCCAC
      CACCCCTGCTTTGGCATAGGCCTTCAGCTCATAGTCCGTAAACTTGGACACACTCAGACCAATGGTGGCTGCTCCAA
      TCCCAATGAGAGGGCTGACAGAAATAATAACCAAGGTCAGTTTCCAACCCCTGAAAAATCCCAACAGGAAACCACAG
      ATGGTCGAGGTCATGCGCTGAATGAAAAGGGCCATTTGGTCAGCTATGGCATCATTGATTTTATTAATATCATCAGA
      GAATCTTGT	[NA]

Point mutation
^^^^^^^^^^^^^^^

.. code:: bash

   $ transvar ganno --ccds -i 'chr3:g.178936091G>A' --gseq

:: 

   chr3:g.178936091G>A	CCDS43171.1 (protein_coding)	PIK3CA	+
      chr3:g.178936091G>A/c.1633G>A/p.E545K	inside_[cds_in_exon_9]
      CSQN=Missense;dbsnp=rs104886003(chr3:178936091G>A);codon_pos=178936091-178936
      092-178936093;ref_codon_seq=GAG;source=CCDS	chr3	178936091	G	A


.. code:: bash

   $ transvar ganno -i "chr9:g.135782704C>G" --ccds --gseq

:: 

   chr9:g.135782704C>G	CCDS55350.1 (protein_coding)	TSC1	-
      chr9:g.135782704C>G/c.1164G>C/p.L388L	inside_[cds_in_exon_10]
      CSQN=Synonymous;dbsnp=rs770692313(chr9:135782704C>G);codon_pos=135782704-1357
      82705-135782706;ref_codon_seq=CTG;source=CCDS	chr9	135782704	C	G
   chr9:g.135782704C>G	CCDS6956.1 (protein_coding)	TSC1	-
      chr9:g.135782704C>G/c.1317G>C/p.L439L	inside_[cds_in_exon_11]
      CSQN=Synonymous;dbsnp=rs770692313(chr9:135782704C>G);codon_pos=135782704-1357
      82705-135782706;ref_codon_seq=CTG;source=CCDS	chr9	135782704	C	G


.. code:: bash

   $ transvar panno -i PIK3CA:p.E545K --ensembl

::

   PIK3CA:p.E545K	ENST00000263967 (protein_coding)	PIK3CA	+
      chr3:g.178936091G>A/c.1633G>A/p.E545K	inside_[cds_in_exon_10]
      CSQN=Missense;reference_codon=GAG;candidate_codons=AAG,AAA;candidate_mnv_vari
      ants=chr3:g.178936091_178936093delGAGinsAAA;dbsnp=rs104886003(chr3:178936091G
      >A);aliases=ENSP00000263967;source=Ensembl


Deletion
^^^^^^^^^^^

INDELs are left-aligned by VCF convention. Note that `--gseq` is also constrained by `--seqmax`

.. code:: bash

   $ transvar ganno -i "chr2:g.234183368_234183380del" --ccds --gseq --seqmax 20

::

   chr2:g.234183368_234183380del	CCDS2502.2 (protein_coding)	ATG16L1	+
      chr2:g.234183368_234183380delACTCATCCTGGTT/c.841_853delACTCATCCTGGTT/p.T281Lfs*5	inside_[cds_in_exon_8]
      CSQN=Frameshift;left_align_gDNA=g.234183367_234183379delTACTCATCCTGGT;unalign
      ed_gDNA=g.234183368_234183380delACTCATCCTGGTT;left_align_cDNA=c.840_852delTAC
      TCATCCTGGT;unalign_cDNA=c.841_853delACTCATCCTGGTT;source=CCDS	chr2	234183366	
      ATACTCATCCTGGT	A
   chr2:g.234183368_234183380del	CCDS2503.2 (protein_coding)	ATG16L1	+
      chr2:g.234183368_234183380delACTCATCCTGGTT/c.898_910delACTCATCCTGGTT/p.T300Lfs*5	inside_[cds_in_exon_9]
      CSQN=Frameshift;left_align_gDNA=g.234183367_234183379delTACTCATCCTGGT;unalign
      ed_gDNA=g.234183368_234183380delACTCATCCTGGTT;left_align_cDNA=c.897_909delTAC
      TCATCCTGGT;unalign_cDNA=c.898_910delACTCATCCTGGTT;source=CCDS	chr2	234183366	
      ATACTCATCCTGGT	A
   chr2:g.234183368_234183380del	CCDS54438.1 (protein_coding)	ATG16L1	+
      chr2:g.234183368_234183380delACTCATCCTGGTT/c.409_421delACTCATCCTGGTT/p.T137Lfs*5	inside_[cds_in_exon_5]
      CSQN=Frameshift;left_align_gDNA=g.234183367_234183379delTACTCATCCTGGT;unalign
      ed_gDNA=g.234183368_234183380delACTCATCCTGGTT;left_align_cDNA=c.408_420delTAC
      TCATCCTGGT;unalign_cDNA=c.409_421delACTCATCCTGGTT;source=CCDS	chr2	234183366	
      ATACTCATCCTGGT	A


.. code:: bash

   $ transvar panno --ccds -i 'AADACL4:p.W263_I267delWRDAI' --gseq --seqmax 200

::

   AADACL4:p.W263_I267delWRDAI	CCDS30590.1 (protein_coding)	AADACL4	+
      chr1:g.12726310_12726324delGGCGTGACGCCATCT/c.788_802delGGCGTGACGCCATCT/p.W263_I267delWRDAI	inside_[cds_in_exon_4]
      CSQN=InFrameDeletion;left_align_gDNA=g.12726308_12726322delCTGGCGTGACGCCAT;un
      aligned_gDNA=g.12726309_12726323delTGGCGTGACGCCATC;left_align_cDNA=c.786_800d
      elCTGGCGTGACGCCAT;unalign_cDNA=c.787_801delTGGCGTGACGCCATC;left_align_protein
      =p.W263_I267delWRDAI;unalign_protein=p.W263_I267delWRDAI;imprecise;source=CCD
      S	chr1	12726307	CCTGGCGTGACGCCAT	C


Insertions
^^^^^^^^^^^

.. code:: bash

   $ transvar ganno -i 'chr7:g.121753754_121753755insCA' --ccds --gseq --seqmax 200

::

   chr7:g.121753754_121753755insCA	CCDS5783.1 (protein_coding)	AASS	-
      chr7:g.121753754_121753755insCA/c.1064_1065insGT/p.I355Mfs*10	inside_[cds_in_exon_9]
      CSQN=Frameshift;left_align_gDNA=g.121753753_121753754insAC;unalign_gDNA=g.121
      753754_121753755insCA;left_align_cDNA=c.1063_1064insTG;unalign_cDNA=c.1063_10
      64insTG;source=CCDS	chr7	121753753	A	AAC

Block substitution
^^^^^^^^^^^^^^^^^^^

.. code:: bash

   $ transvar canno --ccds -i 'CSRNP1:c.1212_1224delinsCCCCC' --gseq --verbose 3

gives


Block substitution reduced to deletion.

.. code:: bash

   $ transvar canno --ccds -i 'CSRNP1:c.1212_1224delinsGGAGGAGGAA' --gseq

gives

::

   CSRNP1:c.1212_1224delinsGGAGGAGGAA	CCDS2682.1 (protein_coding)	CSRNP1	-
      chr3:g.39185102_39185104delTCC/c.1221_1223delGGA/p.E411delE	inside_[cds_in_exon_4]
      CSQN=InFrameDeletion;left_align_gDNA=g.39185093_39185095delTCC;unaligned_gDNA
      =g.39185093_39185095delTCC;left_align_cDNA=c.1212_1214delGGA;unalign_cDNA=c.1
      221_1223delGGA;left_align_protein=p.E405delE;unalign_protein=p.E407delE;sourc
      e=CCDS	chr3	39185092	TTCC	T

Duplication
^^^^^^^^^^^^

.. code:: bash

   $ transvar canno --ccds -i 'CHD7:c.1669_1674dup'

::

   CHD7:c.1669_1674dup	CCDS47865.1 (protein_coding)	CHD7	+
      chr8:g.61693564_61693569dupCCCGTC/c.1669_1674dup/p.P558_S559dupPS	inside_[cds_in_exon_2]
      CSQN=InFrameInsertion;left_align_gDNA=g.61693561_61693562insTCCCCG;unalign_gD
      NA=g.61693562_61693567dupTCCCCG;left_align_cDNA=c.1668_1669insTCCCCG;unalign_
      cDNA=c.1669_1674dupTCCCCG;left_align_protein=p.H556_S557insSP;unalign_protein
      =p.S557_P558dupSP;phase=0;source=CCDS

.. code:: bash

   $ transvar panno -i 'ABCC3:p.Y556_556delinsR' --ensembl --gseq

gives

:: 

   ABCC3:p.Y556_556delinsR	ENST00000285238 (protein_coding)	ABCC3	+
      chr17:g.48745254_48745256delinsAGG/c.1666_1668delinsAGG/p.Y556_556delinsR	inside_[cds_in_exon_13]
      CSQN=MultiAAMissense;candidate_alternative_sequence=AGG/AGA/CGA/CGC/CGG/CGT;a
      liases=ENSP00000285238;source=Ensembl	chr17	48745253	GTAC	GAGG

Frameshift
^^^^^^^^^^^^

.. code:: bash

   $ transvar panno -i 'PTEN:N323Kfs*2' --ensembl --gseq --seqmax 1000

gives

::

   PTEN:N323Kfs*2	ENST00000371953 (protein_coding)	PTEN	+
      chr10:g.89720817dupA/c.968dupA/p.N323Kfs*2	inside_[cds_in_exon_8]
      CSQN=Frameshift;left_align_cDNA=c.962_963insA;left_align_gDNA=g.89720811_8972
      0812insA;candidates=g.89720817_89720818insG/c.968_969insG/g.89720817_89720818
      insG/c.968_969insG,g.89720814_89720815insG/c.965_966insG/g.89720814_89720815i
      nsG/c.965_966insG,g.89720811dupC/c.962dupC/g.89720810_89720811insC/c.961_962i
      nsC,g.89720811_89720812insG/c.962_963insG/g.89720811_89720812insG/c.962_963in
      sG,g.89720811_89720812insT/c.962_963insT/g.89720811_89720812insT/c.962_963ins
      T;aliases=ENSP00000361021;source=Ensembl	chr10	89720811	C	CA


Test --strictversion argument
###############################

`--strictversion` argument requires the version in the transcript database to be the same as the query. This is
sometimes overly strong. 

Without consistent transcript version

.. code:: bash

   $ transvar canno --ccds -i 'CCDS46444.2:c.1198-8C>A' --strictversion

gives

::

   CCDS46444.2:c.1198-8C>A	.	.	.	././.	.	no_valid_transcript_found

With consistent transcript version

.. code:: bash

   $ transvar canno --ccds -i 'CCDS46444.1:c.1198-8C>A' --strictversion

gives

::

   CCDS46444.1:c.1198-8C>A	CCDS46444.1 (protein_coding)	ABCB11	-
      chr2:g.169833205G>T/c.1198-8C>A/.	inside_[intron_between_exon_10_and_11]
      CSQN=IntronicSNV;source=CCDS

This argument only work when the transcript version is explicitly given. The following case doesn't have transcript version. Hence the constraint is removed.

.. code:: bash

   $ transvar canno --ccds -i 'CCDS46444:c.1198-8C>A' --strictversion

gives

::

   CCDS46444:c.1198-8C>A	CCDS46444.1 (protein_coding)	ABCB11	-
      chr2:g.169833205G>T/c.1198-8C>A/.	inside_[intron_between_exon_10_and_11]
      CSQN=IntronicSNV;source=CCDS


