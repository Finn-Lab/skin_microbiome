# MAG Snakemake Workflow


## Contents

- [Overview](#overview)
- [System Requirements](#system-requirements)
- [Running pipeline](#running-pipeline)
- [License](./LICENSE)
- [Citation](#citation)

# Overview

This pipeline has the scripts and modules used to generate, quality assess, and taxonomically classify skin MAGs which were obtained using different per sample and co-assembly approaches. The prok.Snakefile and euk.Snakefile detail the prokaryotic and eukaryotic analyses respectively. Note that for the eukaryotic analyses, EukRep and EukCC need to already have been run. To use the pipeline a file called coassembly_runs.txt and runs.txt must be produced which detail the co-assembly approaches and the per sample approaches used in our pipeline. The metagenomes must be put in the directory data/singlerun and data/coassembly for the single run and co-assembly approaches respectively. A sample coassembly_runs.txt and runs.txt file has been provided. The viral analysis was done via the VIRify pipeline (https://github.com/EBI-Metagenomics/emg-viral-pipeline).


# System Requirements

## Hardware Requirements
HPC with at least 500 gigabytes of memory

## Software Requirements
- SPAdes v.3.13.0
- metaWRAP v1.2.1
- CheckM  v1.1.2
- Mash v.2.0
- MUMmer v3.23
- dRep v2.3.2 
- GTDB-Tkv1.0.2
- EukRep v.0.6.7
- EukCC v0.2


# Running pipeline 

### Submitting jobs

To run pipeline on the runs specified in runs.txt and coassembly_runs.txt, submit jobs with SLURM scheduler:
```
snakemake -s prok.Snakefile --use-singularity --restart-times 3 -k -j 50 --cluster-config clusterconfig.yaml --cluster "sbatch -n {cluster.nCPU} --mem {cluster.mem} -e {cluster.error} -o {cluster.output} -t {cluster.time}"
```

Submit jobs with LSF scheduler:
```
snakemake -s prok.Snakefile --use-singularity --restart-times 3 -k --jobs 50 --cluster-config clusterconfig.yaml --cluster "bsub -n {cluster.nCPU} -M {cluster.mem} -e {cluster.error} -o {cluster.output}"
```

