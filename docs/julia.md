# Using Julia packages on Bianca


!!! info "Objectives"
    - We'll ...

   - At UPPMAX there is a central library with installed packages.
   - This is good, especially when working on Bianca, since you don't need to install via the Wharf.
   - If you work on Rackham you can actually ignore it and do all installations by yourself. The reason is that you need some more steps.

## UPPMAX Central library

!!! info
   
    The Julia application at UPPMAX comes with several preinstalled packages.
	A selection of the Julia packages and libraries installed on UPPMAX are:
    
      - BenchmarkTools
      - CSV
      - CUDA
      - MPI
      - Distributed
      - IJulia
      - Plots
      - PyPlot
      - Gadfly
      - DataFrames
      - DistributedArrays
      - PlotlyJS


- You may control the present "central library" by typing ``ml help julia/<version>`` in the BASH shell.
- A possibly more up-to-date status can be found from the Julia shell:

``` julia 

    using Pkg
    Pkg.activate(DEPOT_PATH[2]*"/environments/v1.8");     #change version (1.8) accordingly if you have another main version of Julia
    Pkg.status()
    Pkg.activate(DEPOT_PATH[1]*"/environments/v1.8");     #to return to user library

```

## Install yourself

If you have started Julia once you will get the folders like this in the ~/.julia folder.

```bash
   $ tree .julia/ -d -L 1
   .
   ├── artifacts
   ├── bin
   ├── compiled
   ├── conda
   ├── environments
   ├── logs
   ├── packages
   ├── prefs
   ├── registries
   └── scratchspaces
```

**The plan is that what you install on Rackham should be moved here in the same manner**

- Make an installation of the package on Rackham in the Julia package manager
- Use a transfer method to move the package files to the wharf
    - To be certain to include all files, you may transfer the whole .julia dir. However, that can grow rather big with time.

!!! warning
    
    **Continue**



!!! abstract "keypoints"
    - bullet 1
    - bullet 2

