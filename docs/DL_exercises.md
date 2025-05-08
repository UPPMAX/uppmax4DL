# DL Exercises

!!! info

    We put some exercises here for you, if you want to get some more hands-on.
    

## Prepare your project folder

???+ question "Make arrangements for the new project"

   
    - Find your way into your project uppmax2025-3-5 by logging in to Rackham by ThinLinc/ssh/VSCode.
    - Go to private folder and make an empty folder with your name under `private` or `nobackup/private`

        ??? tip "Answer"
            `ssh jayan@rackham.uppmax.uu.se`  
            `ssh -X jayan@rackham.uppmax.uu.se`
            `cd /proj/uppmax2025-3-5`
            `mkdir`  
    
    - Copy contents from `uppmax_workshop` to your private folder. 


## Create environment

???+ question "Use venv or conda to prepare your environment"

    - Module load python and use venv to create a environment with pytorch, transformers and jupyter.

        ??? tip "Answer"
            
            ```console
            module load python/3.12.7
            which python
            python -V
            python -m venv torch_env
            ```

            If using conda, follow instructions from "Use isolated environments" section.

    - Activate your env and install desired packages.

            

## Using the compute nodes

???+ question "Submit a Slurm job"

    - Close the [cifar10 resnet repository](https://github.com/akamaster/pytorch_resnet_cifar10?tab=readme-ov-file) and edit the run.sh by adding appropriate slurm sbatch commands.
    
    ??? tip "Answer"
        - edit a file using you prefered editor, named `my_bio_worksflow.sh`, for example, with the content
        
        ```bash
            #!/bin/bash -l

            #SBATCH -A uppmax2025-3-5
            #SBATCH -p node
            #SBATCH -N 1
            #SBATCH -t 01:00:00
            #SBATCH -J cifar_demo
            #SBATCH -M snowy
            #SBATCH --gres=gpu:1

            module load python_ML_packages/3.9.5-gpu

            python -c "import torch; print(torch.__version__); print(torch.version.cuda); print(torch.cuda.get_device_properties(0)); print(torch.randn(1).cuda())"

            #for model in resnet20 resnet32 resnet44 resnet56 resnet110 resnet1202
            for model in resnet20 resnet110
            do
                echo "python -u trainer.py  --arch=$model  --save-dir=save_$model |& tee -a log_$model"
                python -u trainer.py  --arch=$model  --save-dir=save_$model |& tee -a log_$model
            done

        ```

        - make the job script executable
        ```bash
        $ chmod a+x run.sh
        ```
        
        - submit the job
        ```bash
        $ sbatch run.sh
        ```
        
<!-- ## Doing installations


### Conda installation

???+ question "Install with Conda directly on Rackham"

    - Install ``python>3.11``, transformers, torch, torchvision, notebook (using pip), pytorch-cuda=12.4, ipython, pillow -->


