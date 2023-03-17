# Exercises

!!! info

    We put some exercises here for you, if you want to get some more hands-on.
    
## Working on Bianca


## Working with modules

???+ question "Assignment: View in IGV"

    
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

- Make a batch job to run the [demo](https://uppmax.github.io/bianca_workshop/modules1/#workflows) "Hands on: Processing a BAM file to a VCF using GATK, and annotating the variants with snpEff"

## Doing installations

### Rpackage installation

- Install Tidycmprsk
- 
### Conda installation

- Create a conda environment and install some packages

### Pip installation

### Singularity/apptainer

- gatk on bianca
