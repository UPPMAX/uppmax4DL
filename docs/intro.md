# Overview

## What is neeed to be able to run at UPPMAX
- SUPR
  - account
  - project

## How to access the clusters?
- login
  - ssh
  - ThinLinc

## Where should keep my data?
  - `uquota`

## How to transfer files?
  - `scp`
  - `rsync`
    - example: `rsync -av /local/dir user@rackham.uppmax.uu.se:/proj/naiss2023-22-247/nobackup/private/user/.`

## The module system
  - LMOD
  - `module avail <name>`
  - `module spider <name>`
  - `module load <module>/<version>`
  - `module list`
  - `module unload <module>/<version>`
  - `module purge`

## Slurm


## Profiling on the GPUs
  - `nvidia-smi`
    - `nvidia-smi dmon -o DT`
    - `nvidia-smi --format=noheader,csv --query-compute-apps=timestamp,gpu_name,pid,name,used_memory --loop=1 -f sample_run.log`
    - `nvidia-smi --help` or `man nvidia-smi`
  - `module load nvtop`
     - `nvtop`
