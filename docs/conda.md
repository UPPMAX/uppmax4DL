# Conda

!!! info "Objectives"
    - We'll ...

!!! abstract "keypoints"
    - bullet 1
    - bullet 2

This is a brief description of the necessary steps to use the local Conda repository at UPPMAX, and install things for yourself or your project using Conda. 

To use conda on UPPMAX Bianca you could use the following steps:

1. Run: module load conda
This loads the module conda and grants you access to the latest version of conda and all major repositories on all UPPMAX systems.

2. Run: export CONDA_ENVS_PATH=/a/path/to/a/place/in/your/project/
The variable CONDA_ENVS_PATH contains the location of your environments. As long as all members of a project set the variable CONDA_ENVS_PATH to the same place, you can all use the same environments. Set it to your project's environments folder. Otherwise, the default is ~/.conda/envs (warning: installing conda environments in your home directory like this can quickly consume all your space and/or files).

3: Run: conda create ... etc
This where you use conda as you normally would. On Bianca this is equal to running conda with --offline on Rackham since there is no internet. 

Customising
    - You may run 'source conda_init.sh' to initialise your shell to be able to run 'conda activate' and 'conda deactivate' etc. Just remember that this command ADDS STUFF TO YOUR SHELL outside the scope of the module system.
