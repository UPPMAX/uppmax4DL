# Installing R packages on Bianca

## First check if package is already in R_packages/X.Y.0

- You can quickly check if your package is there by:

``$ ml R_packages/4.1.1``

Then grep for some package, in this case "glmnet".

```bash
$ ls -l $R_LIBS_SITE | grep glmnet
dr-xr-sr-x  9 douglas sw  4096 Sep  6  2021 EBglmnet
dr-xr-sr-x 11 douglas sw  4096 Nov 11  2021 glmnet
dr-xr-sr-x  8 douglas sw  4096 Sep  7  2021 glmnetcr
dr-xr-sr-x  7 douglas sw  4096 Sep  7  2021 glmnetUtils
```

## Install steps

### Install on Rackham

- [R on UPPMAX course](https://uppmax.github.io/R-python-julia-HPC/R/packagesR.html)
- **note** First decide on wich R version it should be based on and load that R_packages module.
- If not stated otherwise, your installation will end up in your ``~/R`` directory

#### Methods

- automatic download and install from CRAN
    - <https://uppmax.github.io/bianca_workshop/rpackages/#automatical-download-and-install-from-cran>

- automatic download and install from GitHub
    - <https://uppmax.github.io/bianca_workshop/rpackages/#automatic-download-and-install-from-github>

- manual download and install
    - <https://uppmax.github.io/bianca_workshop/rpackages/#manual-download-and-install>
    - **NOTE** that if you install a package this way, you need to handle any dependencies yourself.
        - For instance you might get use of our modules  

### Transfer to wharf

- You may transfer the whole R library (in you home folder)  
- or select the directory(-ies) related to you new installation
    - **note** there may be more than one directory

### Move package to local Bianca R package path 

- Sync or move the R directory or the specific folders to ~/R 

### Test your installation

- Start an R session and load the new package



## Example — Install Tidycmprsk

[tidycmprsk on GitHub](https://mskcc-epi-bio.github.io/tidycmprsk/)

!!! info
   
    The tidycmprsk package provides an intuitive interface for working with the competing risk endpoints. The package wraps the cmprsk package, and exports functions for univariate cumulative incidence estimates with cuminc() and competing risk regression with crr().


### Install on Rackham

You can install this for yourself by beginning on rackham. Do

``` bash
module load R_packages/4.1.1
```
and then, within R, do

``` R
install.packages('tidycmprsk')
```

You will see two questions to answer yes to:

``` R
Warning in install.packages("tidycmprsk") :
      'lib = "/sw/apps/R_packages/4.1.1/rackham"' is not writable
    Would you like to use a personal library instead? (yes/No/cancel) yes
```

and

``` R
Would you like to create a personal library
    '~/R/x86_64-pc-linux-gnu-library/4.1'
    to install packages into? (yes/No/cancel) yes
```

This will then to an extended installation process that also does some updates.  This creates a directory ~/R that contains the installations and updates of R packages.

### Transfer to the Wharf

After installation, the next step is to copy the contents of this directory over to bianca so that it is the same directory within your bianca home directory.

Make sure you are in your **home directory**. Then connect to the bianca wharf.  Replace the name and project with your bianca user name and project.

``` bash
sftp douglas-sens2017625@bianca-sftp
```

You log in here like you log into bianca: the first password is your **password followed by the 6-digit authenticator code**, the second password (if required for you) is only your password.

Once sftp has connected, the contents of the current directory can be listed with

``` bash
dir
```

It should look like this:

    sftp> dir
    douglas-sens2017625

Now ``cd`` to this directory, which is your wharf directory within your project.

``` bash
sftp> cd douglas-sens2017625/
sftp> dir
sftp>
```

If you have not uploaded anything to your wharf, this will be empty. It might have a few things in it.

Now, upload your (whole) ``R`` directory here.

``` bash
sftp> put -r R
```

This will take a while to upload all the files. When it has completed, quit.

``` bash
sftp> quit
```

- Now, **log into bianca** using the shell, or using the web interface and start a terminal. 
- Once you have a bianca shell, **change to your wharf directory** within your project.  Replace my user and project with yours.

``` bash
cd /proj/sens2017625/nobackup/wharf/douglas/douglas-sens2017625
```

Within this directory should be your R directory.

``` bash
[douglas@sens2017625-bianca douglas-sens2017625]$ ls -l
total 1892
drwxrwxr-x  3 douglas douglas    4096 Mar  2 14:27 R
```

### Sync from Wharf to Home directory

- Now sync this to your home directory:

``` bash
[douglas@sens2017625-bianca douglas-sens2017625]$ rsync -Pa R ~/
```

### Start an R session and load the new package

To use R_packages/4.1.1 with these new installations/updates, change to the directory you want to work in, load the R_packages/4.1.1 module.  Substitute your directory for my example directory.

``` bash
[douglas@sens2017625-bianca douglas-sens2017625]$ cd /proj/sens2017625/nobackup/douglas/
    [douglas@sens2017625-bianca douglas]$ module load R_packages/4.1.1
```

Then start R, and load the new package.

``` bash
[douglas@sens2017625-bianca douglas]$ R
```

``` R
    R version 4.1.1 (2021-08-10) -- "Kick Things"
    Copyright (C) 2021 The R Foundation for Statistical Computing
    ....
    Type 'demo()' for some demos, 'help()' for on-line help, or
    'help.start()' for an HTML browser interface to help.
    Type 'q()' to quit R.

    > library(tidycmprsk)
    >
```

