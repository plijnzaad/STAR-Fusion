

left_fq="reads_1.fq.gz"
right_fq="reads_2.fq.gz"


kickstart:
	../STAR-Fusion --genome_lib_dir ${CTAT_GENOME_LIB}  --left_fq ${left_fq} --right_fq ${right_fq} -J __kickstart_data/Chimeric.out.junction -O star_fusion_kickstarted_outdir 


standard:
	../STAR-Fusion --genome_lib_dir ${CTAT_GENOME_LIB}  --left_fq ${left_fq} --right_fq ${right_fq} -O star_fusion_outdir


standard_bbmerge:
	../STAR-Fusion --genome_lib_dir ${CTAT_GENOME_LIB}  --left_fq ${left_fq} --right_fq ${right_fq} -O star_fusion_bbmerge_outdir --bbmerge


all: standard \
     kickstart \
     kickstart_evreads \
     kickstart_annotate \
     kickstart_coding_effect \
     kickstart_FI_inspect \
     standard_denovo_reconstruct \
     standard_annotate \
     standard_coding_effect \
     standard_SE \
     kickstart_SE \
     standard_bbmerge \
     standard_bbmerge_FI_inspect \
     standard_bbmerge_FI_validate


#####################################################
#### Kickstart, starting from chimeric junctions file

kickstart_evreads: kickstart
	../STAR-Fusion -J __kickstart_data/Chimeric.out.junction --genome_lib_dir ${CTAT_GENOME_LIB}  --extract_fusion_reads --left_fq ${left_fq} --right_fq ${right_fq} -O star_fusion_kickstarted_outdir

kickstart_annotate: kickstart
	../STAR-Fusion -J __kickstart_data/Chimeric.out.junction --genome_lib_dir ${CTAT_GENOME_LIB} --annotate --left_fq ${left_fq} --right_fq ${right_fq} -O star_fusion_kickstarted_outdir

kickstart_coding_effect: kickstart_annotate
	../STAR-Fusion -J __kickstart_data/Chimeric.out.junction --genome_lib_dir ${CTAT_GENOME_LIB} --examine_coding_effect --annotate --left_fq ${left_fq} --right_fq ${right_fq} -O star_fusion_kickstarted_outdir


kickstart_FI_inspect: kickstart_coding_effect
	../STAR-Fusion -J __kickstart_data/Chimeric.out.junction --genome_lib_dir ${CTAT_GENOME_LIB}  --examine_coding_effect --annotate --FusionInspector inspect --left_fq ${left_fq} --right_fq ${right_fq} -O star_fusion_kickstarted_outdir


###################################
#### Full mode, starting from reads

standard_denovo_reconstruct: standard
	../STAR-Fusion --genome_lib_dir ${CTAT_GENOME_LIB}  --denovo_reconstruct --FusionInspector validate --left_fq ${left_fq} --right_fq ${right_fq} -O star_fusion_outdir

standard_annotate: standard
	../STAR-Fusion --genome_lib_dir ${CTAT_GENOME_LIB}  --FusionInspector validate --annotate --left_fq ${left_fq} --right_fq ${right_fq} -O star_fusion_outdir

standard_coding_effect: standard_annotate
	../STAR-Fusion --genome_lib_dir ${CTAT_GENOME_LIB}  --FusionInspector validate --annotate --examine_coding_effect --left_fq ${left_fq} --right_fq ${right_fq} -O star_fusion_outdir


##################################
#### Single-end reads instead of pairs

standard_SE:
	../STAR-Fusion --genome_lib_dir ${CTAT_GENOME_LIB}  --FusionInspector inspect --annotate --examine_coding_effect --left_fq ${left_fq} -O star_fusion_SE_outdir

kickstart_SE:
	../STAR-Fusion --genome_lib_dir ${CTAT_GENOME_LIB} -J __kickstart_data/Chimeric.out.junction  --FusionInspector inspect --annotate --examine_coding_effect --left_fq ${left_fq} -O star_fusion_SE_outdir_kickstart


##############################
### bbmerge

standard_bbmerge_FI_inspect: standard_bbmerge
	../STAR-Fusion --genome_lib_dir ${CTAT_GENOME_LIB}  --left_fq ${left_fq} --right_fq ${right_fq} -O star_fusion_bbmerge_outdir --bbmerge --FusionInspector inspect --annotate --examine_coding_effect 


standard_bbmerge_FI_validate: standard_bbmerge
	../STAR-Fusion --genome_lib_dir ${CTAT_GENOME_LIB}  --left_fq ${left_fq} --right_fq ${right_fq} -O star_fusion_bbmerge_outdir --bbmerge --FusionInspector validate --annotate --examine_coding_effect 





######################
## Cleanup

clean:
	rm -rf ./star_fusion_outdir
	rm -rf ./star_fusion_kickstarted_outdir
	rm -rf ./star_fusion_SE_outdir
	rm -rf ./star_fusion_SE_outdir_kickstart
	rm -rf ./star_fusion_bbmerge_outdir
	(rm -rf ./test_docker_outdir) || sudo rm -rf ./test_docker_outdir

