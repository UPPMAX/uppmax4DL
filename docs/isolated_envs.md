# Use isolated environments

!!! abstract "Learning objectives"
    - Practice using the documentation of your HPC cluster
    - Find out which isolated environment tool to use on your HPC cluster
    - Work (create, activate, work, deactivate) with isolated environments
      in the way recommended by your HPC cluster
    - (optional) work (create, activate, work, deactivate) with isolated environments
      in the other way (if any) possible on your HPC cluster
    - (optional) export and import a virtual
      environment

## Isolated environments

- As an example, maybe you have been using TensorFlow 1.x.x for your project and 
    - now you need to install a package that requires TensorFlow 2.x.x 
    - but you will still be needing the old version of TensorFlow for another package, for instance. 
- This is easily solved with isolated environments.

- Another example is when a reviewer want you to remake a figure. 
    - You have already started to use a newer Python version or newer packages and 
    - realise that your earlier script does not work anymore. 
- Having freezed the environment would have solved you from this issue!

!!! note
    Isolated/virtual environments solve a couple of problems:
    
    - You can install specific, also older, package versions into them.
    - You can create one for each project and no problem if the two projects require different versions.
    - You can remove the environment and create a new one, if not needed or with errors.
    - Good for reproducibility!

- Isolated environments let you create separate workspaces for different versions of Python and/or different versions of packages. 
- You can activate and deactivate them one at a time, and work as if the other workspace does not exist.

**The tools**

- Python's built-in `venv` module: uses pip       
- `virtualenv` (can be installed): uses pip   
- `conda`/`forge`: uses `conda`/`mamba`     

### What happens at activation?

- Python version is defined by the environment.
    - Check with `which python`, should show at path to the environment.
    - In conda you can define python version as well
    - Since `venv` is part of Python you will get the python version used when running the `venv` command.
- Packages are defined by the environent.
    - Check with `pip list`
    - Conda can only see what you installed for it.
    - venv and virtualenv also see other packages if you allowed for that when creating the environment (`--system-site-packages`). 
- You can work in a Python shell or IDE (coming session)
- You can run scripts dependent on packages now instaleld in your environment.


!!! tip
    - Try with `venv` first
    - If very troublesome, try with `conda`
    
    - To use self-installed Python packages in a batch script, you also need to load the above mentioned modules and activate the environment. An example of this will follow later in the course. 
    - To see which Python packages you, yourself, have installed, you can use `pip list --user` while the environment you have installed the packages in is active. To see all packages, use `pip list`. 

??? "Other tools perhaps covered in the future"
    - [pixi](https://pixi.sh/latest/): package management tool for developers 
        - It allows the developer to install libraries and applications in a reproducible way. Use pixi cross-platform, on Windows, Mac and Linux.
        - could replace conda/mamba
    
    - [uv](https://docs.astral.sh/uv/): An extremely fast Python package and project manager, written in Rust. 
        - A single tool to replace pip, pip-tools, pipx, poetry, pyenv, twine, virtualenv, and more

## Virtual environment - venv & virtualenv

With this tool you can download and install with `pip` from the [PyPI repository](https://pypi.org/)

??? "venv vs. virtualenv"
    - These are almost completely interchangeable
    - The difference being that **virtualenv supports older python versions** and has a few more minor unique features, while **venv is in the standard library**.
    - Step 1:
        - Virtualenv: `virtualenv --system-site-packages Example`
        - venv: `python -m venv --system-site-packages Example2`
    - Next steps are identical and involves "activating" and `pip installs`
    - We recommend `venv` in the course. Then we are just needing the Python module itself!

### Typical workflow

1. Start from a Python version you would like to use (load the module): 
    - This step are different at different clusters since the naming is different

2. Load the Python module you will be using, as well as any site-installed package modules (requires the `--system-site-packages` option later)
    - `module load <python module>`

The next points will be the same for all clusters

3. Create the isolated environment with something like `python -m venv <name-of-environment>` 
    - use the `--system-site-packages` to include all "non-base" packages
    - include the full path in the name if you want the environment to be stored other than in the "present working directory".

4. Activate the environment with `source <path to virtual environment>/bin activate`

!!! note
    - `source` can most often be replaced by `.`, like in `. Example/bin/activate`. Note the important <space> after `.`
    - For clarity we use the `source` style here.

5. Install (or update) the environment with the packages you need with the `pip install` command

    - Note that `--user` must be omitted: else the package will be installed in the global user folder.
    - The `--no-cache-dir"` option is required to avoid it from reusing earlier installations from the same user in a different environment. The `--no-build-isolation` is to make sure that it uses the loaded modules from the module system when building any Cython libraries.

6. Work in the isolated environment
   - When activated you can always continue to add packages!
7. Deactivate the environment after use with `deactivate`

!!! note
    To save space, you should load any other Python modules you will need that are system installed before installing your own packages! Remember to choose ones that are compatible with the Python version you picked! 
         `--system-site-packages` includes the packages already installed in the loaded python module.
    
    
    ```console
    $ module load python/3.11.5 
    $ python -m venv --system-site-packages Example_env
    ```

!!! warning
    Draw-backs
    
    - Only works for Python environments
    - Only works with Python versions already installed

??? "Example NSC"
    ```console
    ml buildtool-easybuild/4.8.0-hpce082752a2 GCC/13.2.0 Python/3.11.5 
    which python
    python -V
    cd /proj/hpc-python-spring-naiss/users/<username>
    python -m venv env-matplotlib
    source activate  env-matplotlib
    pip install matplotlib
    python
    ```
    
    ```python
    >>> import matplotlib
    ```

!!! note
    - You can use "pip list" on the command line (after loading the python module) to see which packages are available and which versions. 
    - Some packaegs may be inhereted from the moduels yopu have loaded
    - You can do `pip list --local` to see what is installed by you in the environment.
    - Some IDE:s like Spyder may only find those "local" packages

## Conda

- [Conda](https://anaconda.org/anaconda/conda) is an installer of packages but also bigger toolkits and is useful also for R packages and C/C++ installations.

- Conda creates isolated environments not clashing with other installations of python and other versions of packages.
- Conda environment requires that you install all packages needed by yourself. 
    - That is,  you cannot load the python module and use the packages therein inside you Conda environment.

??? "Conda channels"
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
     
    You reach them all by loading the conda module. You don't have to state the specific channel when using UPPMAX. Otherwise you do with `conda -c <channel> ...`

!!! warning
    Drawbacks
    
    - Conda cannot use already install packages from the Python modules and libraries already installed, and hence installs them anyway
    - Conda is therefore known for creating **many** *small* files. Your diskspace is not only limited in GB, but also in number of files (typically `300000` in $HOME). 
    - Check your disk usage and quota limit
        - Do a `conda clean -a` once in a while to remove unused and unnecessary files

!!! tip
    - The conda environemnts inclusing many small files are by default stored in `~/.conda` folder that is in your $HOME directory with limited storage.
    - Move your `.conda` directory to your project folder and make a soft link to it from `$HOME`
    - Do the following (`mkdir -p` ignores error output and will not recfreate anothe folder if it already exists):
         - (replace what is inside `<>` with relevant path)
    
    - Solution 1
    
       This works nicely if you have several projects. Then you can change these varables according to what you are currently working with.
    
       ```bash
       export CONDA_ENVS_PATH="path/to/your/project/(subdir)"
       export CONDA_PKG_DIRS="path/to/your/project/(subdir)"
       ```
    
    - Solution 2 
    
       - This may not be a good idea if you have several projects.
    
       ```bash
       $ mkdir -p ~/.conda
       $ mv ~/.conda /<path-to-project-folder>/<username>/
       $ ln -s /<path-to-project-folder>/<username>/.conda ~/.conda
       ```

### Typical workflow

The first 2 steps are cluster dependent and will therefore be slightly different.

1. Make conda available from a software module, like `ml load conda` or similar, or use own installation of miniconda or miniforge.
2. First time

??? "First time"
    - The variables CONDA_ENVS_PATH and CONDA_PKG_DIRS contains the location of your environments. Set it to your project's environments folder, if you have one, instead of the $HOME folder.
    - Otherwise, the default is `~/.conda/envs`. 
    - Example:
    
    ```console
    $ export CONDA_ENVS_PATH="path/to/your/project/(subdir)"
    $ export CONDA_PKG_DIRS="path/to/your/project/(subdir)"
    ```

Next steps are the same for all clusters

3. Create the conda environment `conda create -n <name-of-env>`
4. Activate the conda environment by: `source activate <conda-env-name>`

    - You can define the packages to be installed here already.
    - If you want another Python version, you have to define it here, like: `conda ... python=3.6.8`

5. Install the packages with `conda install ...` or `pip install ...`
6. Now do your work!

    - When activated you can always continue to add packages!

7. Deactivate

```bash
(python-36-env) $ conda deactivate
```

??? "Comments"
    - When pinning with Conda, use single `=` instead of double (as used by pip)

??? "Conda base env"
    - When conda is loaded you will by default be in the base environment, which works in the same way as other conda environments. It includes a Python installation and some core system libraries and dependencies of Conda. It is a "best practice" to avoid installing additional packages into your base software environment.

??? "Conda cheat sheet"
    - List packages in present environment:	`conda list`
    - List all environments:			`conda info -e` or `conda env list`
    - Install a package: `conda install somepackage`
    - Install from certain channel (conda-forge): `conda install -c conda-forge somepackage`
    - Install a specific version: `conda install somepackage=1.2.3`
    - Create a new environment: `conda create --name myenvironment`
    - Create a new environment from requirements.txt: `conda create --name myenvironment --file requirements.txt`
    - On e.g. HPC systems where you don't have write access to central installation directory: conda create --prefix /some/path/to/env`
    - Activate a specific environment: `conda activate myenvironment`
    - Deactivate current environment: `conda deactivate`

??? "Conda vs mamba etc..."
    - [what-is-the-difference-with-conda-mamba-poetry-pip](https://pixi.sh/latest/misc/FAQ/#what-is-the-difference-with-conda-mamba-poetry-pip)

??? "What to do when a problem arises?"
    - If you experience unexpected problems with the conda provided by the module system on Rackham or anaconda3 on Dardel, you can easily install your own and maintain it yourself.
    - Read more at [Pavlin Mitev's page about conda on Rackham/Dardel](https://hackmd.io/@pmitev/conda_on_Rackham) and change paths to relevant one for your system.
    - Or [Conda - "best practices" - UPPMAX](https://hackmd.io/@pmitev/module_conda_Rackham)

## Install from file

- All centers has had different approaches in what is included in the module system and not.
- Therefore the solution to complete the necessary packages needed for the course lessons, different approaches has to be made.
- This is left as exercise for you, see Exercise 4.

### venv

`pip install -r requirements.txt`

### conda

`conda env create -f environment.yaml`

## Exercises

!!! question "Exercise 0: Make a decision between `venv` or `conda`."
    - go with `venv` first as it is simpler to manage.

!!! question "Exercise 1: Cover the documentation for venvs or conda"
    First try to find it by navigating.
    

??? "Solution"
    #### venv
    
    - [Python venv](https://docs.uppmax.uu.se/software/python_venv/)
    - [Video By Richel](https://www.youtube.com/watch?v=lj_Q-5l0BqU)
    
    #### conda

    - https://docs.uppmax.uu.se/software/conda/
    

!!! question "Exercise 2: Prepare the course environment"
    install transformers and pytorch
