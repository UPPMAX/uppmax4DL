# Module system (continued) and Slurm
    - interactive vs. non-interactive sessions
    - why is interactive needed at all?
    - e.g. nextflow - main node should be on interactive

# Software and tools
```{objectives}
- We'll briefly get overviews over 
    -  software tools on UPPMAX
    -  databases
- Introduction quide for installing own software or packages
- Very short introduction to developing old programs
```

- 800+ programs and packages are installed.
- To avoid chaos and collisions, they are managed by a **module system**.
- This system keeps installed software hidden by default, and users have to explicitly tell their terminal which version of which software they need.
- The modules are most often available across cluster (except for Miarka)


```{note}
- Bioinformatics tools require loading the “bioinfo-tools” module first.
```

## Modules

- [Software at UPPMAX](https://www.uppmax.uu.se/resources/software/)
- [Module system](https://www.uppmax.uu.se/resources/software/module-system/)

### Some commands

- list all available modules (also bio-informatics if `bioinfo-tools` is loaded)
  - `module avail` or `ml av`

- Search for modules (full name not needed and case insensitive) 
  - `module avail <part of tool name>` or `ml av <part of toolname>`

- Load a module 
  - `module load <module name>` or `ml <module name>`

- Unload a module 
  - `module unload <module name>` or `ml -<module name>`

- List loaded modules 
  - `module list` or `ml`

- Display a brief module-specific help (not available for all modules)
  - `module help <module name>` or `ml help <module name>` 
 
- Search (like `avail`) but otherwise hidden modules (`bioinfo-tools` and Easybuild modules) 
  -  `module spider <part of tool name>` or `ml spider <module name>` 

## Installed software
- You can also find (almost) all installed software at:
    <https://www.uppmax.uu.se/resources/software/installed-software/>
  
## Installed databases
- [Installed databases at UPPMAX](https://www.uppmax.uu.se/resources/databases/)
    
``````{challenge} Hands on using a tool
1. use matlab

```
$ matlab &
```
- Does not work!
- Load module first
```
$ module avail matlab

$ module load matlab/R2020b

$ matlab &
```
- Matlab starts (if X11 is active)
- `module load matlab` will start default version (often latest)

2. use Samtools

```
$ module load samtools
```
        "These module(s) or extension(s) exist but cannot be loaded as requested: "samtools""
```
module load bioinfo-tools samtools
```
- Bioinformatic tools are hidden by default

``````

## Run own scripts or programs
- Unless your script or program is in the active path, you run it by the full path or `./<file>` if you are in the present directory.


# Submitting jobs
```{objectives}
- This is a short introduction in how to reach the calculation nodes
- Thursday afternoon is wedded to this topic!
```

## Slurm, sbatch, the job queue
- Problem: 1000 users, 500 nodes, 10k cores
- Need a queue:

![Image](./img/queue1.png)
- x-axis: cores, one thread per core
- y-axis: time
<br/><br/>
- [Slurm](https://slurm.schedmd.com/) is a jobs scheduler
- Plan your job and but in the slurm job batch (sbatch)
    `sbatch <flags> <program>` or
    `sbatch <job script>`

- Easiest to schedule *single-threaded*, short jobs

![Image](./img/queue2.png)
![Image](./img/queue3.png)
- Left: 4 one-core jobs can run immediately (or a 4-core wide job).

  - The jobs are too long to fit in core number 9-13.

- Right: A 5-core job has to wait.

  - Too long to fit in cores 9-13 and too wide to fit in the last cores.

## Jobs
- Job = what happens during booked time
- Described in a Bash script file
  - Slurm parameters (**flags**)
  - Load software modules
  - (Move around file system)
  - Run programs
  - (Collect output)
- ... and more

## Slurm parameters
- 1 mandatory setting for jobs:
  - Which compute project? (`-A`)
- 3 settings you really should set:
  - Type of queue? (`-p`)
    - core, node, (for short development jobs and tests: devcore, devel)
  - How many cores? (`-n`)
    - up to 16 (20 on Rackham) for core job
  - How long at most? (`-t`)
- If in doubt:
  - -`p core`
  - -`n 1`
  - `-t 7-00:00:00`

![Image](./img/queue1.png)

- Where should it run? (`-p node` or `-p core`)
- Use a whole node or just part of it?
  - 1 node = 20 cores (16 on Bianca & Snowy)
  - 1 hour walltime = 20 core hours = expensive
   -Waste of resources unless you have a parallel program or need all the memory, e.g. 128 GB per node
- Default value: core

## Interactive jobs
- Most work is most effective as submitted jobs, but e.g. development needs responsiveness
- Interactive jobs are high-priority but limited in `-n` and `-t`
- Quickly give you a job and logs you in to the compute node
- Require same Slurm parameters as other jobs

``````{challenge} Try interactive

```bash=
  interactive -A naiss2023-22-21 -p core -n 1 -t 10:00
```
- Which node are you on?
  - Logout with `<Ctrl>-D` or `logout`
``````



 
### A simple job script template

```bash=
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

## Other Slurm tools

- Squeue — quick info about jobs in queue
- Jobinfo — detailed info about jobs
- Finishedjobinfo — summary of finished jobs
- Jobstats — efficiency of booked resources

``````{challenge} Exercise at home
- Copy the code just further up!
- Put it into a file named “jobtemplate.sh”
- Make the file executable (chmod)
- Submit the job:
```
$ sbatch jobtemplate.sh
```
- Note the job id!
- Check the queue:
```
$ squeue -u <username>
$ jobinfo -u <username>
```
- When it’s done (rather fast), look for the output file (slurm-<jobid>.out):
```
$ ls -lrt slurm-*
```
- Check the output file to see if it ran correctly
```
$ cat <filename>
```
``````
 
 


!!! abstract "Keypoints"
    - Centrally installed software are reached through the module system and available throughout all nodes.
    - Your own installed software, scripts, python packages etcetera are available from their paths.
    - You are always in the login node unless you:
        - start an interactive session
        - start a batch job
    - Slurm is a job scheduler
        - add flags to describe your job.
 
