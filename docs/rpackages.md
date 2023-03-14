# Installing R packages on Bianca

https://uppmax.github.io/R-python-julia-HPC/R/packagesR.html

## What is a package, really?

An R package is essentialy a contained folder and file structure containing R
code (and possibly C/C++ or other code) and other files relevant for the
package e.g. documentation(vignettes), licensing and configuration files. Let
us look at a very simple example 


``` sh

   $ git clone git@github.com:MatPiq/R_example.git

   $ cd R_example

   $ tree
   .
   ├── DESCRIPTION
   ├── NAMESPACE
   ├── R
   │   └── hello.R
   ├── man
   │   └── hello.Rd
   └── r_example.Rproj
   
```
   
## Installing your own packages

Sometimes you will need R packages that are not already installed. The solution
to this is to install your own packages. These packages will usually come from
CRAN (https://cran.r-project.org/) - the Comprehensive R Archive Network, or
sometimes from other places, like GitHub or R-Forge

Here we will look at installing R packages with automatic download and with
manual download. It is also possible to install from inside Rstudio. 

### Setup


We need to create a place for the own-installed packages to be and to tell R
where to find them. The initial setup only needs to be done once, but separate
package directories need to be created for each R version used. 

R reads the ``$HOME/.Renviron`` file to setup its environment. It should be
created by R on first run, or you can create it with the command: ``touch
$HOME/.Renviron``

**NOTE**: In this example we are going to assume you have chosen to place the R
packages in a directory under your home directory. As mentioned, you will need
separate ones for each R version.

If you have not yet installed any packages to R yourself, the environment file
should be empty and you can update it like this: 

.. code-block:: sh 

    echo R_LIBS_USER=\"$HOME/R-packages-%V\" > ~/.Renviron

If it is **not** empty, you can edit ``$HOME/.Renviron`` with your favorite
editor so that ``R_LIBS_USER`` contain the path to your chosen directory for
own-installed R packages. It should look something like this when you are done:

.. code-block:: sh 

    R_LIBS_USER="/home/u/user/R-packages-%V"


| NOTE: Replace ``/home/u/user`` with the value of ``$HOME``. Run ``echo $HOME`` to see its value.
| NOTE: The ``%V`` should be written as-is, it's substituted at runtime with the active R version.

For each version of R you are using, create a directory matching the pattern
used in ``.Renviron`` to store your packages in. This example is shown for R
version 4.0.4:

.. code-block:: sh 

    mkdir -p $HOME/R-packages-4.0.4


### Automatical download and install from CRAN


.. note:: 

    You find a list of packages in CRAN (https://cran.r-project.org/) and a list of repos here: https://cran.r-project.org/mirrors.html 

    Please choose a location close to you when picking a repo. 


.. tabs::

   .. tab:: From command line

      .. code-block:: sh 

          R --quiet --no-save --no-restore -e "install.packages('<r-package>', repos='<repo>')"
    
   .. tab:: From inside R

      .. code-block:: sh 

          install.packages('<r-package>', repos='<repo>')
       

In either case, the dependencies of the package will be downloaded and
installed as well. 

      
Example
*******

In this example, we will install the R package ``stringr`` and use the
repository http://ftp.acc.umu.se/mirror/CRAN/ 

.. tabs::

   .. tab:: From command line

      .. code-block:: sh 

          R --quiet --no-save --no-restore -e "install.packages('stringr', repos='http://ftp.acc.umu.se/mirror/CRAN/')"
       
   .. tab:: From inside R

      .. code-block:: sh 

          install.packages('stringr', repos='http://ftp.acc.umu.se/mirror/CRAN/')



### Automatic download and install from GitHub

If you want to install a package that is not on CRAN, but which do have a
GitHub page, then there is an automatic way of installing, but you need to
handle prerequsites yourself by installing those first. It can also be that the
package is not in as finished a state as those on CRAN, so be careful. 

To install packages from GitHub directly, from inside R, you first need to
install the devtools package. Note that you only need to install this **once**. 

This is how you install a package from GitHub, inside R:

 .. code-block:: R
 
    install.packages("devtools")   # ONLY ONCE
    devtools::install_github("DeveloperName/package")
    

Example
*******

In this example we want to install the package ``quantstrat``. It is not on
CRAN, so let's get it from the GitHub page for the project:
https://github.com/braverock/quantstrat 

We also need to install devtools so we can install packages from GitHub. In
addition, ``quantstrat`` has some prerequisites, some on CRAN, some on GitHub,
so we need to install those as well. 

.. code-block:: sh 

   install.packages("devtools") # ONLY ONCE
   install.packages("FinancialInstrument") 
   install.packages("PerformanceAnalytics") 
   
   devtools::install_github("braverock/blotter")
   devtools::install_github("braverock/quantstrat")

    
### Manual download and install

If the package is not on CRAN or you want the development version, or you for
other reason want to install a package you downloaded, then this is how to
install from the command line: 

.. code-block:: sh 

    R CMD INSTALL -l <path-to-R-package>/R-package.tar.gz
    

**NOTE** that if you install a package this way, you need to handle any
dependencies yourself. 

.. note:: 

   Places to look for R packages
   
   - CRAN (https://cran.r-project.org/)
   - R-Forge (https://r-forge.r-project.org/)
   - Project's own GitHub page
   - etc.

Install Tidycmprsk

Hi,

We are still perhaps a month away from having R_packages/4.2.1.

You can install this for yourself by beginning on rackham. Do

    module load R_packages/4.1.1

and then, within R, do

    install.packages('tidycmprsk')

You will see two questions to answer yes to:

    Warning in install.packages("tidycmprsk") :
      'lib = "/sw/apps/R_packages/4.1.1/rackham"' is not writable
    Would you like to use a personal library instead? (yes/No/cancel) yes

and

    Would you like to create a personal library
    '~/R/x86_64-pc-linux-gnu-library/4.1'
    to install packages into? (yes/No/cancel) yes

This will then to an extended installation process that also does some updates.  This creates a directory ~/R that contains the installations and updates of R packages.

After installation, the next step is to copy the contents of this directory over to bianca so that it is the same directory within your bianca home directory.

Make sure you are in your home directory. Then connect to the bianca wharf.  Replace my name and project with your bianca user name and project.

    sftp douglas-sens2017625@bianca-sftp

You log in here like you log into bianca: the first password is your password followed by the 6-digit authenticator code, the second password (if required for you) is only your password.

Once sftp has connected, the contentsf the current directory can be listed with

    dir

For me, this shows

    sftp> dir
    douglas-sens2017625

Now cd to this directory, which is your wharf directory within your project.

    sftp> cd douglas-sens2017625/
    sftp> dir
    sftp>

If you have not uploaded anything to your wharf, this will be empty. It might have a few things in it.

Now, upload your R directory here.

    sftp> put -r R

This will take a while to upload all the files. When it has completed, quit.

    sftp> quit

Now, log into bianca using the shell, or using the web interface and start a terminal. Once you have a bianca shell, change to your wharf directory within your project.  Replace my user and project with yours.

    cd /proj/sens2017625/nobackup/wharf/douglas/douglas-sens2017625

Within this directory should be your R directory.

    [douglas@sens2017625-bianca douglas-sens2017625]$ ls -l
    total 1892
    drwxrwxr-x  3 douglas douglas    4096 Mar  2 14:27 R

Now sync this to your home directory:

    [douglas@sens2017625-bianca douglas-sens2017625]$ rsync -Pa R ~/

To use R_packages/4.1.1 with these new installations/updates, change to the directory you want to work in, load the R_packages/4.1.1 module.  Substitute your directory for my example directory.

    [douglas@sens2017625-bianca douglas-sens2017625]$ cd /proj/sens2017625/nobackup/douglas/
    [douglas@sens2017625-bianca douglas]$ module load R_packages/4.1.1

Then start R, and load the new package.

    [douglas@sens2017625-bianca douglas]$ R

    R version 4.1.1 (2021-08-10) -- "Kick Things"
    Copyright (C) 2021 The R Foundation for Statistical Computing
    ....
    Type 'demo()' for some demos, 'help()' for on-line help, or
    'help.start()' for an HTML browser interface to help.
    Type 'q()' to quit R.

    > library(tidycmprsk)
    >


