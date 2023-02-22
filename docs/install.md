# Software installation without internet connection
    - Conda packages: installing/using [name=Jonas]
        - alternative: installing with pip
    - R package installation not included in R packages [name=Marcus]
    - Julia [name=Björn C]
    - running jupyter notebooks [name=Lars]
    - containers [name=Björn V]
    
    
## Install software yourself
- You can install in your home directory.
    - This is handy for personal needs, low numbers of files (i.e. not Conda).
- Usually better to install in project directory.
    - This way the project contains both data and software — good for reproducibility, collaboration, and everyone's general sanity.

### Python packages
- [Python packages](https://uppmax.uu.se/support/user-guides/python-user-guide/)

#### Conda
- [Conda user guide](https://www.uppmax.uu.se/support/user-guides/conda-user-guide/)

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



!!! abstract "Keypoints"
    - Centrally installed software are reached through the module system and available throughout all nodes.
    - Your own installed software, scripts, python packages etcetera are available from their paths.
