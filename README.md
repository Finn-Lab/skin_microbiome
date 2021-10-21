# MAG Snakemake Workflow


## Contents

- [Overview](#overview)
- [Running pipeline](#running-pipeline)
- [License](./LICENSE)
- [Citation](#citation)

# Overview

This pipeline has the scripts and modules used to generate skin MAGs using different per sample and co-assembly approaches. To use the pipeline a file called coassembly_runs.txt and runs.txt must be produced which detail the co-assembly approaches and the per sample approaches used in our pipeline. The metagenomes must be put in the directory data/singlerun and data/coassembly for the single run and co-assembly approaches respectively



# Running pipeline 

### Submitting jobs

To run pipeline on the runs specified in runs.txt and coassembly_runs.txt, submit jobs with SLURM scheduler:
```
snakemake --use-singularity --restart-times 3 -k -j 50 --cluster-config clusterconfig.yaml --cluster "sbatch -n {cluster.nCPU} --mem {cluster.mem} -e {cluster.error} -o {cluster.output} -t {cluster.time}"
```

Submit jobs with LSF scheduler:
```
snakemake --use-singularity --restart-times 3 -k --jobs 50 --cluster-config clusterconfig.yaml --cluster "bsub -n {cluster.nCPU} -M {cluster.mem} -e {cluster.error} -o {cluster.output}"
```

