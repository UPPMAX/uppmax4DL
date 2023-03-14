# Install with pip to Bianca

## Check for packages 
   
- from the Python shell with the ``import`` command
- from BASH shell with the 
	
- ``pip list`` command 
- ``ml help python/3.9.5`` at UPPMAX

## Install on Rackham

- You use ``pip`` this way, in a Linux shell OR a python shell: 

```bash 
    $ pip install --user <package>
```    

Use ``pip3`` if you loaded python3.

!!! info

    **Then the package ends up in ``~/.local/lib/python<version>/site-packages/`` .**

    - Note that python<version> is omitting the last number (bug fix), like 3.8 for python-3.8.7.
    
    - We HIGHLY recommend using a virtual environment during installation, since this makes it easier to install for different versions of Python.  
    - More information [here](https://uppmax.github.io/HPC-python/isolated.html). 

	
## Isolated/virtual environments

[Python on UPPMAX course](https://uppmax.github.io/R-python-julia-HPC/python/isolated.html)

!!! note
   
    Isolated environments solve a couple of problems:
   
    - You can install specific package, also older, versions into them.
    - You can create one for each project and no problem if the two projects require different versions.
    - You can remove the environment and create a new one, if not needed or with errors.
    
Example:

$ module load python/3.6.8
$ python -m venv --system-site-packages <proj-dir>/projectB
	
“projectB” is the name of the virtual environment. The directory “projectB” is created in the present working directory. The ``-m`` flag makes sure that you use the libraries from the python version you are using.	

- Virtual environments can be saved easily anywhere
	

## Moving the files from Rackham to Bianca
    
    
    To be filled
