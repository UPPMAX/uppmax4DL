# Install with pip to Bianca

## Check for packages 
   
- from the Python shell with the ``import`` command
- from BASH shell with the 
	
- ``pip list`` command 
- ``ml help python/3.9.5`` at UPPMAX

**Is it not there? Then proceed!

!!! info

    **Methods:**
    - You can either just download a python package, transfer to Wharf and Bianca and install there.
    - Install it on Rackham. Perhaps you need it here as well! Then transfer to Wharf and Bianca local python library.
    - Make a virtual environment with one or several packages on Rackham. Then transfer to Wharf and Bianca (any place).



## Just download on Rackham and install on Bianca

``` sh 
$ pip download <package-name>
``` 

Then move the package to the Wharf and install it (Yes, you can do it from this place) using the usual

``` sh 
$ pip install --user <path-to-package-name>
```

**Then the package ends up in ``~/.local/lib/python<version>/site-packages/`` .**


## Install on Rackham

!!! info

    **The package ends up on Rackham in ``~/.local/lib/python<version>/site-packages/`` .**

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
	

### Moving the files from Rackham to Bianca
    
    

