# Using Julia packages on Bianca


!!! info "Objectives"
    - We'll ...

   - At UPPMAX there is a central library with installed packages.
   - This is good, especially when working on Bianca, since you don't need to install via the Wharf.
   - If you work on Rackham you can actually ignore it and do all installations by yourself. The reason is that you need some more steps.

## UPPMAX Central library

!!! info
   
    A selection of

      - BenchmarkT
      - CSV
      - CUDA
      - MPI
      - Distribute
      - IJulia
      - Plots
      - PyPlot
      - Gadfly
      - DataFrames
      - Distribute
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

The julia lkical library directory looks like this:

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

...


!!! abstract "keypoints"
    - bullet 1
    - bullet 2

