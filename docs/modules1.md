# Working with the modules on Bianca

!!! info "Objectives" 

    - Using module system commands
    - Use software in the module system for some typical workflows
       
- 800+ programs and packages are installed, with usually many versions of each.
- To avoid chaos and collisions, they are managed by a **module system** called [LMOD](https://lmod.readthedocs.io/en/latest/).
- By default, the only software available on Bianca and other UPPMAX clusters are standard Linux tools.
- **All other software** is made available by using the module system.
- This means users must explicitly request software, together with software versions, that they require.
- This turns out to be quite easy to do. It also improves readability and reproducibility.
- Nearly all software in the module system is available on all UPPMAX clusters.


!!! warning 
    - To access bioinformatics tools, load the **bioinfo-tools** module first.


### Modules

- [Software at UPPMAX](https://www.uppmax.uu.se/resources/software/)
- [Module system](https://www.uppmax.uu.se/resources/software/module-system/)

#### Some commands

The `module` command is the basic interface to the module system.
The `ml` shortcut command is also available.

- list all modules immediately available, or search for a specific available module
    - `module avail` or `ml av`
    - `module avail *tool*` or `ml av *tool*`

This command is not so smart, though, especially when searching for a specific tool, or a bioinformatics tool.
It only reports modules that are immediately available.

```
$ ml av R
```
outputs everything that has an `r` in the name... not useful.

```
$ ml av samtools
No module(s) or extension(s) found!
Use "module spider" to find all possible modules and extensions.
Use "module keyword key1 key2 ..." to search for all possible modules matching any of the "keys".
```

It is better to use `module spider` or `ml spider`.
If there is an exact match, it reports it first.

```
$ ml spider R

-------------------------------------------
  R:
-------------------------------------------
     Versions:
        R/3.0.2
        R/3.2.3
        R/3.3.2
        R/3.4.0
        R/3.4.3
        R/3.5.0
        R/3.5.2
        R/3.6.0-foss-2019a
        R/3.6.0
        R/3.6.1
        R/4.0.0
        R/4.0.4
        R/4.1.1
        R/4.2.1
     Other possible modules matches:
        454-dataprocessing  ADMIXTURE  ANTLR  ARCS  ARC_assembler  ARPACK-NG  ART  AdapterRemoval  AlienTrimmer  Amber  AnchorWave  Arlequin  Armadillo  ArrowGrid  Bamsurgeon  BclConverter  BioBakery  BioBakery_data  ...

-------------------------------------------
  To find other possible module matches execute:

      $ module -r spider '.*R.*'

-------------------------------------------
  For detailed information about a specific "R" package (including how to load the modules) use the module's full name.
  Note that names that have a trailing (E) are extensions provided by other modules.
  For example:

     $ module spider R/4.2.1
-------------------------------------------
```

```
$ ml spider samtools

-------------------------------------------
  samtools:
-------------------------------------------
     Versions:
        samtools/0.1.12-10
        samtools/0.1.19
        samtools/1.1
        samtools/1.2
        samtools/1.3
        samtools/1.4
        samtools/1.5_debug
        samtools/1.5
        samtools/1.6
        samtools/1.8
        samtools/1.9
        samtools/1.10
        samtools/1.12
        samtools/1.14
        samtools/1.16
        samtools/1.17
     Other possible modules matches:
        SAMtools

-------------------------------------------
  To find other possible module matches execute:

      $ module -r spider '.*samtools.*'

-------------------------------------------
  For detailed information about a specific "samtools" package (including how to load the modules) use the module's full name.
  Note that names that have a trailing (E) are extensions provided by other modules.
  For example:

     $ module spider samtools/1.17
-------------------------------------------
```

The final bit of output tells us more about a specific module version, including the special step required to access all bioinformatics modules.

```
$ ml spider samtools/1.17

-------------------------------------------
  samtools: samtools/1.17
-------------------------------------------

    You will need to load all module(s) on any one of the lines below before the "samtools/1.17" module is available to load.

      bioinfo-tools

    Help:
        samtools - use samtools 1.17

        Version 1.17
```

This reminds us that we need to load the `bioinfo-tools` module to be able to load `samtools/1.17`.
Again, this is required (just once) before loading bioinformatics software.

- Load a module 
    - `module load <module name>` or `ml <module name>`

To load the `samtools/1.17` module, which is a bioinformatics module.

```
$ ml bioinfo-tools
$ ml samtools/1.17
```

- List the loaded modules
    - `module list` or simply `ml`

```
$ ml

Currently Loaded Modules:
  1) uppmax   2) bioinfo-tools   3) samtools/1.17
```

Now to load `GATK/4.3.0.0`, `bioinfo-tools` is not required.
This also demonstrates that loading some modules produces messages that may be helpful for using the module at UPPMAX.

```
$ ml GATK/4.3.0.0
Note that all versions of GATK starting with 4.0.8.0 use a different wrapper
script (gatk) than previous versions of GATK.  You might need to update your
jobs accordingly.

The complete GATK resource bundle is in /sw/data/GATK

See 'module help GATK/4.3.0.0' for information on activating the GATK conda
environment for using DetermineGermlineContigPloidy and similar other tools.
```

This message references the command `module help GATK/4.3.0.0` for additional help with this module.
All modules have at least a brief help message. Some (such as GATK/4.3.0.0) have more extensive help that guides users using features of the modules at UPPMAX.
It is *not* general help for using the tool itself.

- Display a brief module-specific help.
    - `module help <module name>` or `ml help <module name>` 
 

```
$ ml help GATK/4.3.0.0

-------------- Module Specific Help for "GATK/4.3.0.0" ---------------
GATK - use GATK 4.3.0.0
Version 4.3.0.0

**GATK 4.3.0.0**

Usage:

    gatk --help     for general options, including how to pass java options

    gatk --list     to list available tools

    gatk ToolName -OPTION1 value1 -OPTION2 value2 ...
                  to run a specific tool, e.g., HaplotypeCaller, GenotypeGVCFs, ...

For more help getting started, see

    https://software.broadinstitute.org/gatk/documentation/article.php?id=9881

...
```

When we list the modules we see that `GATK/4.3.0.0` is also loaded, as is its prerequisite module `java/sun_jdk1.8.0_151`.

```
$ ml

Currently Loaded Modules:
  1) uppmax   2) bioinfo-tools   3) samtools/1.17   4) java/sun_jdk1.8.0_151   5) GATK/4.3.0.0
```

Modules can also be unloaded, which also unloads their prerequisites.

- Unload a module 
    - `module unload <module name>` or `ml -<module name>`

### Installed software
- You can also find (almost) all installed software at:
    - <https://www.uppmax.uu.se/resources/software/installed-software/>
  
### Installed databases
- [Installed databases at UPPMAX](https://www.uppmax.uu.se/resources/databases/)
    
## Workflows    

* Command-line workflow with human BAM file aligned to hg38.  Examine the BAM file and call variants with GATK.

* Use snpEff to annotate the variants.

* Print a plot using R_packages/4.1.1 within RStudio

**Change this example**    
???+ question "Hands on using a tool""

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
    - Matlab starts
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

### R

### GATK

### SNIPF

### Conda

- just loading procedure
- more in afternoon

### Common problems

- Conda environment clash with loaded python modules
- Forgotten environment variables defined in your `.bashrc` may give unexeptected errors when you run other programs or new versions of a program
- A full ``$HOME`` folder may cause unexpected errors
  - check with ``uquota``

### Jupyter

- ?? Not shown here but presented in [Extra material](https://uppmax.github.io/bianca_workshop/jupyter/)

## Summary

!!! info "``$HOME`` dir and project dir"

    **Quota**
    - Disk usage and number of files
    - check with `quota`
    - ``$HOME`` has always 32 GB and 300,000 files
    - Compute projects both have disk space (512 GB) and computing time attached to them

    **Core hours**
    - You  get core hours only from compute project
    - check with ``projinfo``
    - When they are used you can still get "BONUS" jobs if the resources allow.

- Use your disk spaces wisely
    - home folder just for general stuff and files needed by several projects
       - always read and write protected for others by default
    - otherside project folder which will more easily become public for other's
       - by default available for all project members.
- Use the computing resources wisely
    - low intensity work on login node
    - high intensity work on compute nodes (core hours are counted)
        - for development use the interactive sessions

!!! info
   
    More info about reaching the compute nodes in the afternoon!

## Common problems

- Conda environment clash with loaded python modules
- Forgotten environment variables defined in your `.bashrc` may give unexeptected errors when you run other programs or new versions of a program
- A full ``$HOME`` folder may cause unexpected errors
  - check with ``uquota``



**To extend**
!!! abstract "keypoints"
    
    - Centrally installed software are reached through the module system and available throughout all nodes. 
    - Your own installed software, scripts, python packages etcetera are available from their paths.
    
