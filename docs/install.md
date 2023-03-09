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
  - you can use the wharf to transfer source files and binaries to Bianca from Rackham

## Install software yourself
- You can install in your home directory.
    - This is handy for personal needs, low numbers of files (i.e. not Conda).
- Usually better to install in project directory.
    - This way the project contains both data and software — good for reproducibility, collaboration, and everyone's general sanity.
- If not available on Bianca already you may have to use the wharf to install your tools
    - alternatively let a Application Expert install the tool as a module.



## Packages and libraries to scripting programs

!!! info "Tip Python packages"

    - Try Conda first directly on Bianca. We have mirrored all major conda repositories directly on UPPMAX, on both Rackham and Bianca. These are updated every third day.
    - If you want to keep number of files down, use PyPI (pip), but then you need to use Rackham and the wharf.

### Conda

- We have mirrored all major conda repositories directly on UPPMAX, on both Rackham and Bianca. These are updated every third day.
    We have the following channels available:
    
    - bioconda
    - biocore
    - conda-forge
    - dranew
    - free
    - main
    - pro
    - qiime2
    - r
    - r2018.11
    - scilifelab-lts
    - [Conda user guide](https://www.uppmax.uu.se/support/user-guides/conda-user-guide/)
- https://uppmax.github.io/bianca_workshop/conda/



### Python packages with pip

!!! info "Principle"

    - install on Rackham
        - pip install --user <package>
        - python setup.py install --user or --prefix=<path>
    - sync to wharf
    -move the files on Bianca
    - you may have to update $PYTHONPATH
        
- https://uppmax.github.io/bianca_workshop/pip/
- [Python packages](https://uppmax.uu.se/support/user-guides/python-user-guide/)
- https://uppmax.github.io/R-python-julia-HPC/python/packages.html
- https://uppmax.github.io/R-python-julia-HPC/python/isolated.html


### R packages
- https://uppmax.github.io/bianca_workshop/rpackages/
- https://uppmax.github.io/R-python-julia-HPC/R/packagesR.html
- https://uppmax.github.io/R-python-julia-HPC/R/isolatedR.html

### Julia packages
- https://uppmax.github.io/bianca_workshop/julia/
- https://uppmax.github.io/R-python-julia-HPC/julia/isolatedJulia.html

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
