# MAG Snakemake Workflow


## Contents

- [Overview](#overview)
- [System Requirements](#system-requirements)
- [Workflow setup](#Workflow-setup)
- [Running pipeline](#running-pipeline)
- [CPU time](#CPU-time)
- [License](./LICENSE)
- [Issues](https://github.com/Finn-Lab/MAG_Snakemake_wf/issues)
- [Citation](#citation)

# Overview

This pipeline has the scripts and modules used to generate skin MAGs using different per sample and co-assembly approaches. To use the pipeline a file called coassembly_runs.txt and runs.txt must be produced which detail the co-assembly approaches and the per sample approaches used in our pipeline. If the fukes are bit available locally, they will be downloaded from the SRA to the directory data/raw



# Running pipeline 

### Submitting jobs

To run pipeline on the small gut dataset specified in runs.txt and coassembly_runs.txt, submit jobs with SLURM scheduler:
```
snakemake --use-singularity --restart-times 3 -k -j 50 --cluster-config clusterconfig.yaml --cluster "sbatch -n {cluster.nCPU} --mem {cluster.mem} -e {cluster.error} -o {cluster.output} -t {cluster.time}"
```

Submit jobs with LSF scheduler:
```
snakemake --use-singularity --restart-times 3 -k --jobs 50 --cluster-config clusterconfig.yaml --cluster "bsub -n {cluster.nCPU} -M {cluster.mem} -e {cluster.error} -o {cluster.output}"
```

