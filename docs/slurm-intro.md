# Introduction to compute nodes

## Submitting jobs

!!! info "Objectives"
    - This is a short introduction in how to reach the calculation nodes

### Slurm, sbatch, the job queue
- Problem: _1000 users, 300 nodes, 4.5k cores_
    - Need a queue:

- [Slurm](https://slurm.schedmd.com/) is a jobs scheduler
- Plan your job and but in the slurm job batch (sbatch)
    
    - `sbatch <flags> <program>` or
     `sbatch <job script>`

### Jobs
- Job = what happens during booked time
- Described in a Bash script file
    - Slurm parameters (**flags**)
    - Load software modules
    - (Move around file system)
    - Run programs
    - (Collect output)
- ... and more

### Slurm parameters
- 1 mandatory setting for jobs:
    - Which compute project? (`-A`)
- 3 settings you really should set:
    - Type of queue? (`-p`)
        - core, node, (for short development jobs and tests: devcore, devel)
    - How many cores? (`-n`)
        - up to 16 for core job
    - How long at most? (`-t`)
- If in doubt:
    - `-p core`
    - `-n 1`
    - `-t 10-00:00:00`

![Image](./img/queue1.png)

- Where should it run? (`-p node` or `-p core`)
- Use a whole node or just part of it?
    - 1 node = 16 cores
    - 1 hour walltime = 16 core hours = expensive
        - Waste of resources unless you have a parallel program or need all the memory, e.g. 128 GB per node
- Default value: core

### Interactive jobs
- Most work is most effective as submitted jobs, but e.g. development needs responsiveness
- Interactive jobs are high-priority but limited in `-n` and `-t`
- Quickly give you a job and logs you in to the compute node
- Require same Slurm parameters as other jobs

#### Try interactive

```
$ interactive -A uppmax2025-3-5 -p core -n 1 -t 10:00
```

- Which node are you on?
  - Logout with `<Ctrl>-D` or `logout`
 
#### A simple job script template

```bash
#!/bin/bash

#SBATCH -A uppmax2025-3-5  # Project ID

#SBATCH -p devcore  # Asking for cores (for test jobs and as opposed to multiple nodes) 

#SBATCH -n 1  # Number of cores

#SBATCH -t 00:10:00  # Ten minutes

#SBATCH -J Template_script  # Name of the job

# go to some directory

cd /proj/uppmax2025-3-5/
pwd -P

# load software modules

module load python3/3.12.7
module list

# do something

echo Hello world!  

```

## How compute nodes are moved between project clusters

The total job queue, made by putting together job queues of all project clusters, is monitored, and acted upon, by an external program, named meta-scheduler.

In short, this program goes over the following procedure, over and over again:

    Finds out where all the compute nodes are: on a specific project cluster or yet unallocated.
    Reads status reports from all compute nodes, about all their jobs, all their compute nodes, and all their active users.
    Are there unallocated compute nodes for all queued jobs?
    Otherwise, try to "steal" nodes from project clusters, to get more unallocated compute nodes. This "stealing" is done in two steps: a/ "drain" a certain node, i.e. disallow more jobs to start on it; b/ remove the compute node from the project cluster, if no jobs are running on the node.
    Use all unallocated nodes to create new compute nodes. Jobs with a higher priority get compute nodes first.


### Other Slurm tools

- `squeue` — quick info about jobs in queue
- `jobinfo` — detailed info about jobs
- `finishedjobinfo` — summary of finished jobs
- `jobstats` — efficiency of booked resources
- `bianca_combined_jobinfo`

!!! info "Objectives"
    - We'll briefly get overviews over 
        -  software tools on UPPMAX
        -  databases
    - Introduction quide for installing own software or packages
    - Very short introduction to developing old programs

<!-- !!! note "Node types"

    - Bianca has three node types: thin, fat and gpu. 
        - thin being the typical cluster node with 128 GB memory 
        - fat nodes having 256 GB or 512 GB of memory. 
            - You may specify a node with more RAM, by adding the words "-C fat" to your job submission line and thus making sure that you will get at least 256 GB of RAM on each node in your job. 
            - If you absolutely must have more than 256 GB of RAM then you can request to get 512 GB of RAM specfifically by adding the words "-C mem512GB" to your job submission line. 
            - Please note that requesting 512 GB can not be combined with requesting GPUs.
        - You may also add "-C gpu" to your submission line to request a GPU node with two NVIDIA A100 40 GB. 
            - Please note that all GPU nodes have 256 GB of RAM, and are thus "fat" as well. All compute nodes in Bianca has 16 CPU cores in total.
    - Please note that there are only 5 nodes with 256 GB of RAM, 2 nodes with 512 GB of RAM and 4 nodes with 2xA100 GPUs. The wait times for these node types are expected to be somewhat longer. -->
   
<!-- !!! note "Some Limits"

    - There is a job walltime limit of ten days (240 hours).
    - We restrict each user to at most 5000 running and waiting jobs in total.
    - Each project has a 30 days running allocation of CPU hours. We do not forbid running jobs after the allocation is overdrafted, but instead allow to submit jobs with a very low queue priority, so that you may be able to run your jobs anyway, if a sufficient number of nodes happens to be free on the system.
 -->

!!! abstract "Keypoints"
    - You are always in the login node unless you:
        - start an interactive session
        - start a batch job
    - Slurm is a job scheduler
        - add flags to describe your job.
    - There is a job walltime limit of ten days (240 hours).
 
