# Software and package installation on Bianca


!!! warning "ToDos"

    - formatting

    - add
        - link to compilers
        - hardware info
    
  
    
    


!!! info "Objectives" 

    - We'll go through the methods to work with the modules
    - We'll go through some typical workflows   

## The module system

- As we have seen this morning, there is a lot of programs and tools installed as tools on Bianca.
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

- Python, R and Julia all have some centrally installed packages that are available from the modules. 
- R has a special module called ``R_packages``, and some Machine Learning python packages are included in the ``python_ml_packages`` module.
- If not found there you can try to install those by yourself.


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

!!! info "More info"

    - [Conda user guide](https://www.uppmax.uu.se/support/user-guides/conda-user-guide/)
    - https://uppmax.github.io/bianca_workshop/conda/



### Python packages with pip

!!! info "Principle"

    - install on Rackham
        - pip install --user <package>
        - python setup.py install --user or --prefix=<path>
    - sync to wharf
    - move the files on Bianca
    - you may have to update $PYTHONPATH

!!! info "More info"

    - https://uppmax.github.io/bianca_workshop/pip/
    - [Python packages](https://uppmax.uu.se/support/user-guides/python-user-guide/)
    - https://uppmax.github.io/R-python-julia-HPC/python/packages.html
    - https://uppmax.github.io/R-python-julia-HPC/python/isolated.html


### R packages

- On UPPMAX the module R_packages is a package library containing almost all packages in the
  - CRAN and BioConductor repositories. 
  - As of 2021-11-11 there are a total of 21659 R packages installed in R_packages/4.1.1. A total of 21740 packages are available in CRAN and BioConductor.

- You can quickly check if your package is there by:

``$ ml R_packages/4.1.1``

Then grep for some package, in this case "glmnet".

```bash
$ ls -l $R_LIBS_SITE | grep glmnet
dr-xr-sr-x  9 douglas sw  4096 Sep  6  2021 EBglmnet
dr-xr-sr-x 11 douglas sw  4096 Nov 11  2021 glmnet
dr-xr-sr-x  8 douglas sw  4096 Sep  7  2021 glmnetcr
dr-xr-sr-x  7 douglas sw  4096 Sep  7  2021 glmnetUtils
```

!!! info "More info"

    - https://uppmax.github.io/bianca_workshop/rpackages/
    - https://uppmax.github.io/R-python-julia-HPC/R/packagesR.html
    - https://uppmax.github.io/R-python-julia-HPC/R/isolatedR.html

### Julia packages

- At UPPMAX there is a central library with installed packages.
- This is good, especially when working on Bianca, since you then do not need to install via the Wharf.
- A selection of the Julia packages and libraries installed on UPPMAX are:

        BenchmarkTools
        CSV
        CUDA
        MPI
        Distributed
        IJulia
        Plots
        PyPlot
        Gadfly
        DataFrames
        DistributedArrays
        PlotlyJS

!!! info "More info"

    - https://uppmax.github.io/bianca_workshop/julia/
    - https://uppmax.github.io/R-python-julia-HPC/julia/isolatedJulia.html

## "Containers"
### Singularity
- [Singularity user guide](https://www.uppmax.uu.se/support/user-guides/singularity-user-guide/)

### Docker
- Docker will unfortunately not work on the clusters, since it requires root permission.
- However, Singularity may use Docker images.

## Build from source
- We have several compiler versions from GNU and INTEL
- The safest way is to transfer the source code to Bianca via the wharf.
- [Guide for compiling serial and parallel programs](https://www.uppmax.uu.se/support/user-guides/mpi-and-openmp-user-guide/)


!!! abstract "Keypoints"
    - You have got an overview of the procedures to install packages/libraries and tools on Bianca through the wharf
    - If you feel uncomfortable or think that many users would benefit from the software, ask the support to install it.
