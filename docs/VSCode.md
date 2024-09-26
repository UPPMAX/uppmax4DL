# Setting up VSCode for Rackham and Snowy

!!! info

    - You can run VSCode on your local and still be able to work with modules loaded or environment created on Rackham. 
    - Similarly it is possible to take advantage of Snowy GPUs meanwhile developing on your local computer. 

## 1. Connect your local VSCode to VSCode server running on Rackham

A step by step approach is available on UPPMAX [VSCode documentation](https://docs.uppmax.uu.se/software/vscode_on_rackham/). 

When you first establish the ssh connection to Rackham, your VSCode server directory `.vscode-server` will be created in your home folder `/home/[username]`. 

## 2. Install and manage Extensions on remote VSCode server

By default all the VSCode extensions will get installed on your home folder `/home/[username]`. Due to less storage quota on home folder `32 GB, 300k files`, can quickly fill up with extensions and other file operations. The default installtion path for VSCode extensions can however be changed to your project folder which have way more storage space and file count capacity, `1TB, 1M files`.

### 2.1. Manage Extensions

Go to Command Palette `Ctrl+Shift+P` or `F1`. Search for `Remote-SSH: Settings` and then go to `Remote.SSH: Server Install Path`. Add **Item** as remote host `rackham.uppmax.uu.se` and **Value** as folder in which you want to install all your data and extensions `/proj/uppmax202x-x-xx/nobackup` (without a trailing slash `/`). 

If you already had your `vscode-server` running and storing extensions in home directory. Make sure to kill the server by selecting `Remote-SSH: KIll VS Code Server on Host` on Command Palette and deleting the `.vscode-server` directory in your home folder. 

### 2.2. Install Extensions

You can sync all your local VSCode extensions to the remote server after you are connected with VSCode server on Rackham by searching for `Remote: Install Local Extensions in 'SSH: rackham.uppmax.uu.se'` in Command Palette. You can alternatively, go to Extensions tab and select each individually. 

### 2.3. Selecting Kernels

First you need to start the correct module on Rackham that you contains the interpret you want on your VSCode. For example in case you need ML packages and python interpreter, do `module load python_ML_packages` on Rackham. Check the file path for python interpreter by checking `which python` and copy this path. In case of jupyter server, you can check `jupyter kernelspec list`.
Go to Command Palette `Ctrl+Shift+P` or `F1` on your local VSCode. Search for "interpreter" for python or jupyter server, for example. Then paste the path of your interpreter/kernel. 

`venv` or `conda` environments are also visible on VSCode when you select interpreter/kernel for python or jupyter server. For jupyter, you need to start the server first, check Point 4.

## 3. Port forwarding to use Snowy gpus


## 4. Working with jupyter server on Rackham and snowy

### Solution 1:

### Solution 2:
