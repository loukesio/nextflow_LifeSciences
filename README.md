<h1 align="center"><b>Nextflow  for Life Sciences</span></b></h1>

[![Nextflow](https://img.shields.io/badge/nextflow-%E2%89%A50.27.6-brightgreen.svg)](https://www.nextflow.io/)
![Twitter Follow](https://img.shields.io/twitter/follow/loukesio)
![Javascript](https://img.shields.io/badge/logo-javascript-blue?logo=javascript)

<h2><b>Nextflow for RNA-seq</span></b></h2>

### 1. Check the quality of the fastq.gz files  

```
#!/usr/bin/env nextflow

nextflow.enable.dsl=2

// Input/output paths
params.input = '/netscratch/dep_tsiantis/grp_tsiantis/1_CURRENT_LAB_MEMBERS/LTheodosiou/Projects/GROseq/RNAseq/raw_data'
params.output = '/netscratch/dep_tsiantis/grp_tsiantis/1_CURRENT_LAB_MEMBERS/LTheodosiou/Projects/GROseq/RNAseq/test_nextflow'

process fastqc {

    input:
    path reads

    output:
    path("${params.output}/fastqc_raw/*") into ch_fastqc

    script:
    """
    . "/netscratch/dep_tsiantis/grp_tsiantis/1_CURRENT_LAB_MEMBERS/LTheodosiou/Software/Anaconda3/etc/profile.d/conda.sh"
    conda activate fastqc
    mkdir -p ${params.output}/fastqc_raw
    fastqc $reads -o ${params.output}/fastqc_raw/
    """

}

workflow {
    readsChannel = Channel.fromPath("${params.input}/*.fastq")
    fastqc(readsChannel)
}

```


### References 
Here are some key links that can help you build your own Nextflow pipelines <br>
**1.** [Carpentries material from Physalia courses](https://carpentries-incubator.github.io/workflows-nextflow/index.html) <br>
**2.** [Bioinformatics workflow by Andrew Severin](https://bioinformaticsworkbook.org/dataAnalysis/nextflow/02_creatingAworkflow.html) <br>
**3.** [Nextflow, official site](https://training.nextflow.io/hands_on/04_implementation/#process-4-gatk-recalibrate) <br>
**4.** [Nextflow training, Seqera labs](https://training.seqera.io/#_gitpod)
