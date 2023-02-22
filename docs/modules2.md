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



```{keypoints}
- Centrally installed software are reached through the module system and available throughout all nodes.
- Your own installed software, scripts, python packages etcetera are available from their paths.
```
