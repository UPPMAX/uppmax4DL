# Exercises

!!! info

    We put some exercises here for you, if you want to get some more hands-on.
    
## Working on Bianca


## Working with modules

???+ question "View in IGV"

    
    1. Load the genome, the bam file, and the annotated vcf that we got from the [demo](https://uppmax.github.io/bianca_workshop/modules1/#workflows) into IGV for viewing

        ??? tip "Answer"
            For this small example we use igv-core. Good is also to be on a compute node.
            
            ``` bash
            $ ml bioinfo-tools IGV
            $ igv-core --genome genome.fa ERR1252289.subset.bam ERR1252289.subset.snpEff.vcf.gz
            ```


## Transfering files

- Use the Transit server to copy a file from the the Bianca workshop project to another project, if you belong to one. 


## Using the compute nodes

???+ question "Submit a Slurm job"

    1. Make a batch job to run the [demo](https://uppmax.github.io/bianca_workshop/modules1/#workflows) "Hands on: Processing a BAM file to a VCF using GATK, and annotating the variants with snpEff". Ask for 2 cores for 1h.
    
    ???+ tip "Answer"
        - edit a file using you prefered editor, named `my_bio_worksflow.sh`, for example, with the content
        
        ```bash
        #!/bin/bash
        #SBATCH -A sens2023531
        #SBATCH -J workflow
        #SBATCH -t 01:00:00
        #SBATCH -p core
        #SBATCH -n 2


        cd /proj/sens2023531/workshop/slurm/

        module load bioinfo-tools

        # load samtools
        module load samtools/1.17

        # copy and example BAM file
        cp -a /proj/sens2023531/workshop/data/ERR1252289.subset.bam .

        # index the BAM file
        samtools index ERR1252289.subset.bam

        # load the GATK module
        module load GATK/4.3.0.0

        # make symbolic links to the hg38 genomes
        ln -s /sw/data/iGenomes/Homo_sapiens/UCSC/hg38/Sequence/WholeGenomeFasta/genome.* .

        # create a VCF containing inferred variants
        gatk HaplotypeCaller --reference genome.fa --input ERR1252289.subset.bam --intervals chr1:100300000-100800000 --output ERR1252289.subset.vcf

        # use snpEFF to annotate variants
        module load snpEff/5.1
        java -jar $SNPEFF_ROOT/snpEff.jar eff hg38 ERR1252289.subset.vcf > ERR1252289.subset.snpEff.vcf

        # compress the annotated VCF and index it
        bgzip ERR1252289.subset.snpEff.vcf
        tabix -p vcf ERR1252289.subset.snpEff.vcf.gz
        ```

        - make the file executable
        ```bash
        $ chmoad a+x my_bio_workflow.sh
        ```
        
        - submit the job
        ```bash
        $ sbatch my_bio_workflow.sh
        ```
        
## Doing installations

### Rpackage installation

???+ question "Install Tidycmprsk"

     ??? tip "Answer"
         <https://uppmax.github.io/bianca_workshop/rpackages/#example-install-tidycmprsk>
- 
### Conda installation

???+ question "Create a conda environment and install some packages"

     ??? tip "Answer"
         <https://uppmax.github.io/bianca_workshop/conda/#exercises>



### Pip installation

### Singularity/apptainer

???+ question "Install gatk on bianca"

     ??? tip "Answer"
         <https://uppmax.github.io/bianca_workshop/containers/#example-i-want-gatk-on-bianca>
