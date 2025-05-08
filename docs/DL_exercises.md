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

    - Submit `sentiment_analysis.py` with appropriate flags for its slurm job.
    
    ??? tip "Answer"
        - edit a file using you prefered editor, named `sentiment_analysis_batch.sh`, for example, with the content
        
        ```bash
            #!/bin/bash -l

            #SBATCH -A uppmax2025-3-5
            #SBATCH -p node
            #SBATCH -N 1
            #SBATCH -t 01:00:00
            #SBATCH -J sentiment_analysis
            #SBATCH -M snowy
            #SBATCH --gres=gpu:1

            source .....

            python -c "import torch; print(torch.__version__); print(torch.version.cuda); print(torch.cuda.get_device_properties(0)); print(torch.randn(1).cuda())"

            echo "running sentiment_analysis.py"

            python .....sentiment_analysis.py
        ```

        - make the job script executable, if not already.
        ```bash
        $ chmod a+x sentiment_analysis_batch.sh
        ```
        
        - submit the job
        ```bash
        $ sbatch sentiment_analysis_batch.sh
        ```

    - Similarly run `sentiment_analysis.ipynb` jupyter notebook. Add matplotblib and seaborn to your environment. Start a jupyter server on snowy compute node and then tunnel to the host from your local.

        ??? tip "Answer"
                
                * Install matplotlib and seaborn and start an interactive snowy session:  

                ```console
                source torch_env/bin/acivate
                pip install matplotlib seaborn
                interactive -A uppmax2025-3-5 -M snowy -p node -N 1 -t 1:01:00 --gres=gpu:1
                source torch_env/bin/acivate
                jupyter notebook --ip 0.0.0.0 --no-browser
                ```
                * Then tunnel:  
                `ssh -L 8888:s123:8888 username@rackham.uppmax.uu.se`
                
                * Copy the localhost url and paste it in your browser


### Cache management

* By default HF will install the models and temp files to yur `$HOME` folde which is rather limited to 32 GB and 300k files. 
* To avoid that, you can set `HF_HOME` and `HF_HUB_CACHE` variables to your project folder. Follow instructions on https://huggingface.co/docs/transformers/en/installation?cpu-only=PyTorch#cache-directory. 

<!-- ## Doing installations


### Conda installation

???+ question "Install with Conda directly on Rackham"

    - Install ``python>3.11``, transformers, torch, torchvision, notebook (using pip), pytorch-cuda=12.4, ipython, pillow -->


