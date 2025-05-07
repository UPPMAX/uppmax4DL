# Overview

## What is needed to be able to run at UPPMAX
- SUPR
    - account
    - project

## How to access the clusters?
- login
    - ssh
    - ThinLinc

## Where should you keep your data?
- `uquota`

## How to transfer files?
- `sftp`
- [`scp`](https://docs.uppmax.uu.se/software/rackham_file_transfer_using_scp/)
<!-- - `rsync`
    - example: `rsync -av /local/dir user@rackham.uppmax.uu.se:/proj/naiss2023-22-247/nobackup/private/user/.` -->
- SFTP graphical tools  
    - [WinSCP](https://docs.uppmax.uu.se/software/rackham_file_transfer_using_winscp/) and [FileZilla](https://docs.uppmax.uu.se/software/rackham_file_transfer_using_filezilla/)

## The module system

Built on LMOD, a module system to handle user's environment variables.

Some useful comamnds:

- `module avail <name>`
- `module spider <name>`
- `module load <module>/<version>`
- `module list`
- `module unload <module>/<version>`
- `module purge`

## Slurm

A job schedular used in many supercomputers and HPCs.  

How to submit a job to Slurm?

```bash
sbatch  -A uppmax2025-3-5 -t 02:00:00  -p core  -n 10  my_job.sh
```

What should a jobscript contain?
  
- `-A` : project number 
- `-t` : max time
- `-p` : partition
- `-n/-N` : number or core and/or nodes
- `-J` : job name
- special features : `--gres, --gpus-per-node` etc.
  
### A typical job script:

```bash
#!/bin/bash
#SBATCH -A uppmax2025-3-5
#SBATCH -p node
#SBATCH -N 1
#SBATCH -t 24:00:00

module load software/version

./my-script.sh
```

Useful SBATCH options:

- `--mail-type=BEGIN,END,FAIL,TIME_LIMIT_80`
- `--output=slurm-%j.out`
- `--error=slurm-%j.err `


Useful commands:

- `jobinfo -p devel`
- `sinfo -p node - M snowy`
- `jobinfo -u username --state=running`
- `jobinfo -u username --state=pending`
- `salloc -A naiss2023-22-247 --begin=2023-03-24T08:00:00` starts an interactive job earliest tomorrow at 08:00

### How to cancel jobs?
- `scancel <jobid>`

## Job dependencies
- `sbatch jobscript.sh`   submitted job with jobid1
- `sbatch anotherjobscript.sh`  submitted job with jobid2
- `--dependency=afterok:jobid1:jobid2` job will only start running after the successful end of jobs jobid1:jobid2
- very handy for clearly defined workflows
- One may also use `--dependency=afternotok:jobid` in case you’d like to resubmit a failed job, OOM for example, to a node with a higher memory: `-C mem215GB` or `-C mem1TB`  
- More in [slurm](https://slurm.schedmd.com/sbatch.html#OPT_dependency) documents.


## GPU flags

```bash
#SBATCH -M snowy
#SBATCH --gres=gpu:1
```

??? example "Example of a job running on part of a GPU node"

    ```bash
    #!/bin/bash
    #SBATCH -J GPUjob
    #SBATCH -A uppmax2025-3-5
    #SBATCH -t 03-00:00:00
    #SBATCH -p core
    #SBATCH -n 16
    #SBATCH -M snowy
    #SBATCH --gres=gpu:1

    module use /sw/EasyBuild/snowy/modules/all/
    module load intelcuda/2019b
    ```

??? example "Example of an interactive session on Snowy"

    ```bash
    interactive -A uppmax2025-3-5 -p node -N 1 -t 01:00:00 --gres=gpu:1
    ```

## I/O intensive jobs: use the scratch local to the node

??? example "Example"

    ```bash
    #!/bin/bash
    #SBATCH -J jobname
    #SBATCH -A uppmax2025-3-5
    #SBATCH -p core
    #SBATCH -n 1
    #SBATCH -t 10:00:00

    module load bioinfo-tools
    module load bwa/0.7.17 samtools/1.14

    export SRCDIR=$HOME/path-to-input

    cp $SRCDIR/foo.pl $SRCDIR/bar.txt $SNIC_TMP/.
    cd $SNIC_TMP

    ./foo.pl bar.txt

    cp *.out $SRCDIR/path-to-output/.

    ```

## Job arrays

??? example "Example"  
    Submit many jobs at once with the same or similar parameters
    Use $SLURM_ARRAY_TASK_ID in the script in order to find the correct path

    ```bash
    #!/bin/bash
    #SBATCH -A naiss2023-22-21
    #SBATCH -p node
    #SBATCH -N 2
    #SBATCH -t 01:00:00
    #SBATCH -J jobarray
    #SBATCH --array=0-19
    #SBATCH --mail-type=ALL,ARRAY_TASKS

    # SLURM_ARRAY_TASK_ID tells the script which iteration to run
    echo $SLURM_ARRAY_TASK_ID

    cd /pathtomydirectory/dir_$SLURM_ARRAY_TASK_ID/

    srun -n 40 my-program
    env
    ```

    You may use scontrol to modify some of the job arrays.


## GPU accessibility check

- Chech CUDA environment variable
    ```bash
    [jayan@s180 uppmax2025-3-5]$ env | grep CUDA
    CUDA_VISIBLE_DEVICES=0
    ```
    or
    ```bash
    echo $CUDA_VISIBLE_DEVICES
    ```

- Check CUDA and pytorch accessibility from python  
    ```python
    module load python_ML_packages
    python -c "import torch; print(torch.__version__); print(torch.version.cuda); print(torch.cuda.get_device_properties(0)); print(torch.randn(1).cuda())"
    ```
## Additional information

- [UPPMAX webpage](https://www.uppmax.uu.se/)
- [Slurm](https://docs.uppmax.uu.se/cluster_guides/slurm/)
- [Snowy](https://docs.uppmax.uu.se/cluster_guides/snowy/)
- [GPU:s on Snowy](https://docs.uppmax.uu.se/cluster_guides/slurm/#need-more-resources-or-gpu)
- [Software and package installation](https://docs.uppmax.uu.se/software/install/)
