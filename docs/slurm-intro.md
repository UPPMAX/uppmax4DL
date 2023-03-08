# Introduction to compute nodes

To be removed later

    - interactive vs. non-interactive sessions
    - why is interactive needed at all?
    - **e.g. nextflow - main node should be on interactive**

## Submitting jobs

!!! info "Objectives"
    - This is a short introduction in how to reach the calculation nodes

### Slurm, sbatch, the job queue
- Problem: _1000 users, 500 nodes, 10k cores_
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
        - up to 16 (20 on Rackham) for core job
    - How long at most? (`-t`)
- If in doubt:
    - `-p core`
    - `-n 1`
    - `-t 7-00:00:00`

![Image](./img/queue1.png)

- Where should it run? (`-p node` or `-p core`)
- Use a whole node or just part of it?
    - 1 node = 20 cores (16 on Bianca & Snowy)
    - 1 hour walltime = 20 core hours = expensive
        - Waste of resources unless you have a parallel program or need all the memory, e.g. 128 GB per node
- Default value: core

### Interactive jobs
- Most work is most effective as submitted jobs, but e.g. development needs responsiveness
- Interactive jobs are high-priority but limited in `-n` and `-t`
- Quickly give you a job and logs you in to the compute node
- Require same Slurm parameters as other jobs

#### Try interactive

```
$ interactive -A naiss2023-22-21 -p core -n 1 -t 10:00
```

- Which node are you on?
  - Logout with `<Ctrl>-D` or `logout`
 
#### A simple job script template

```bash
#!/bin/bash -l 
# tell it is bash language and -l is for starting a session with a "clean environment, e.g. with no modules loaded and paths reset"

#SBATCH -A naiss2023-22-21  # Project name

#SBATCH -p devcore  # Asking for cores (for test jobs and as opposed to multiple nodes) 

#SBATCH -n 1  # Number of cores

#SBATCH -t 00:10:00  # Ten minutes

#SBATCH -J Template_script  # Name of the job

# go to some directory

cd /proj/introtouppmax/labs
pwd -P

# load software modules

module load bioinfo-tools
module list

# do something

echo Hello world!  

```

### Other Slurm tools

- Squeue — quick info about jobs in queue
- Jobinfo — detailed info about jobs
- Finishedjobinfo — summary of finished jobs
- Jobstats — efficiency of booked resources

!!! info "Objectives"
    - We'll briefly get overviews over 
        -  software tools on UPPMAX
        -  databases
    - Introduction quide for installing own software or packages
    - Very short introduction to developing old programs



- 800+ programs and packages are installed.
- To avoid chaos and collisions, they are managed by a **module system**.
- This system keeps installed software hidden by default, and users have to explicitly tell their terminal which version of which software they need.
- The modules are most often available across cluster (except for Miarka)


!!! warning 
    - Bioinformatics tools require loading the “bioinfo-tools” module first.

!!! abstract "Keypoints"
    - Centrally installed software are reached through the module system and available throughout all nodes.
    - Your own installed software, scripts, python packages etcetera are available from their paths.
    - You are always in the login node unless you:
        - start an interactive session
        - start a batch job
    - Slurm is a job scheduler
        - add flags to describe your job.
 