# Software installation without internet connection

To be removed

    - Conda packages: installing/using [name=Jonas]
        - alternative: installing with pip
    - R package installation not included in R packages [name=Marcus]
    - Julia [name=Björn C]
    - running jupyter notebooks [name=Lars]
    - containers [name=Björn V]
 
!!! info "Objectives" 

    - We'll go through the methods to work with the modules
    - We'll go through some typical workflows   

## The module system

- As we have seen this morning, there is a lot of praograms and tools installed as tools on Bianca.
- These have typically been installed on Rackham and is synced over to Bianca a couple of times per day.
- You can request installations but that may take several days or even weeks to be handled by the application experts at UPPMAX.
- But you may be able to do installations yourself. Here the use of Rackham comes handy because of the:
  - internet connection
  - the computer architecture is somewhat similar such that precompiled binaries or compiled programs (x86_64) on Rackham will most often work also on Bianca.
  - you can use the wharf to transfer source files and binaries til Bianca from Rackham

## Install software yourself
- You can install in your home directory.
    - This is handy for personal needs, low numbers of files (i.e. not Conda).
- Usually better to install in project directory.
    - This way the project contains both data and software — good for reproducibility, collaboration, and everyone's general sanity.
- If not available on Bianca already you may have to use the wharf to install your tools
    - alternatively let a Application Expert install the tool as a module.



## Packages and libraries to scripting programs

### Python packages with pip
- [Python packages](https://uppmax.uu.se/support/user-guides/python-user-guide/)
- https://uppmax.github.io/bianca_workshop/pip/

### Conda
- [Conda user guide](https://www.uppmax.uu.se/support/user-guides/conda-user-guide/)
- https://uppmax.github.io/bianca_workshop/conda/

### R packages
- https://uppmax.github.io/bianca_workshop/rpackages/

### Julia packages
- https://uppmax.github.io/bianca_workshop/julia/

### "Containers"
#### Singularity
- [Singularity user guide](https://www.uppmax.uu.se/support/user-guides/singularity-user-guide/)

#### Docker
- Docker will unfortunately not work on the clusters, since it requires root permission.

### Build from source
- We have several compiler versions from GNU and INTEL
- [Guide for compiling serial and parallel programs](https://www.uppmax.uu.se/support/user-guides/mpi-and-openmp-user-guide/)
    
### Spack
- The UPPMAX staff has already other ways to install most software applications. 
- Please use Spack only if other ways to install your tool is not possible or very difficult, e.g. requiring very many dependencies and it is not available through, e.g. Easybuild.
- [Spack user guide at UPPMAX](https://www.uppmax.uu.se/support/user-guides/spack-on-uppmax/)

### Own development...
- You may have your own code that you want to run on UPPMAX.
- See the [guide for compiling serial and parallel programs](https://www.uppmax.uu.se/support/user-guides/mpi-and-openmp-user-guide/)
- [User guide for debuggers and profilers](https://www.uppmax.uu.se/support/user-guides/debuggers-and-profiling-tools/)

## Run own scripts or programs
- Unless your script or program is in the active path, you run it by the full path or `./<file>` if you are in the present directory.

## Running Jupyter
- https://uppmax.github.io/bianca_workshop/jupyter/

!!! abstract "Keypoints"
    - You have got an overview of the procedures to install packages/libraries and tools on Bianca through the wharf
    - If you feel uncomfortable or think that many users would benefit from the software, ask the support to install it.
