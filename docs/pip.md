# Install with pip to Bianca

You use ``pip`` this way, in a Linux shell OR a python shell: 

.. code-block:: sh 
    $ pip install --user <package>
    
Use ``pip3`` if you loaded python3.

**Then the package ends up in ``~/.local/lib/python<version>/site-packages/`` .**

Note that python<version> is omitting the last number (bug fix), like 3.8 for python-3.8.7.
We HIGHLY recommend using a virtual environment during installation, since this makes it easier to install for different versions of Python.  More information will follow later in this course (https://uppmax.github.io/HPC-python/isolated.html). 

       - You can check for packages 
   
   	- from the Python shell with the ``import`` command
	- from BASH shell with the 
	
		- ``pip list`` command at both centers
		- ``ml help python/3.9.5`` at UPPMAX
		
   - Installation of Python packages can be done either with **PYPI** or **Conda**
   - You install own packages with the ``pip install`` command (This is the recommended way on HPC2N)
   - At UPPMAX Conda is also available (See Conda section)

    ## virtual environments
    
    ## defined from files
    
    ## Using setup.py
    
    ## Moving the files from Rackham to Bianca
    
    
    To be filled
