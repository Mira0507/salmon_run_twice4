## Q: Do two Salmon (ver. 1.4.0) runs in a row give exactly the same counts? 

### Conda environment 

```yml

name: salmon
channels:
  - conda-forge
  - bioconda 
  - defaults 
dependencies:
  - salmon 
  - r-base =4.0.2
  - bedtools 
  - gawk 
  - r-tidyverse
  - r-data.table
  - r-ggplot2
  - r-markdown
  - r-upsetr
  - r-ggrepel
  - r-ggplotify
  - r-gridextra
  - r-pheatmap
  - bioconductor-deseq2
  - bioconductor-annotationhub
  - bioconductor-tximport

```

### Index files 
Recipe: https://github.com/Mira0507/salmon_indexing/blob/master/README.md



### 1. with --gcBias & --seqBias 

1st run: 

```bash

#!/bin/bash

samples=(Mock_72hpi_S{1..3} SARS-CoV-2_72hpi_S{7..9})

rawdir=../rawdata

prefix=gc-seq-quant1  # Change


for read in ${samples[*]} 
do
    salmon quant -i ../salmon_sa_index_hg19 -l A --gcBias --seqBias -r $rawdir/$read.fastq.gz -p 8 --validateMappings -o $prefix/${read}.quant
done

```

2nd run: 

```bash

#!/bin/bash

samples=(Mock_72hpi_S{1..3} SARS-CoV-2_72hpi_S{7..9})

rawdir=../rawdata

prefix=gc-seq-quant2  # Change


for read in ${samples[*]} 
do
    salmon quant -i ../salmon_sa_index_hg19 -l A --gcBias --seqBias -r $rawdir/$read.fastq.gz -p 8 --validateMappings -o $prefix/${read}.quant
done
```



### 2. with --gcBias 

1st run:

```bash

#!/bin/bash

samples=(Mock_72hpi_S{1..3} SARS-CoV-2_72hpi_S{7..9})

rawdir=../rawdata

prefix=gc-quant1  # Change


for read in ${samples[*]} 
do
    salmon quant -i ../salmon_sa_index_hg19 -l A --gcBias -r $rawdir/$read.fastq.gz -p 8 --validateMappings -o $prefix/${read}.quant
done
```

2nd run:

```bash

#!/bin/bash

samples=(Mock_72hpi_S{1..3} SARS-CoV-2_72hpi_S{7..9})

rawdir=../rawdata

prefix=gc-quant2


for read in ${samples[*]} 
do
    salmon quant -i ../salmon_sa_index_hg19 -l A --gcBias -r $rawdir/$read.fastq.gz -p 8 --validateMappings -o $prefix/${read}.quant
done
```




### 3. with --seqBias

1st run: 

```bash
#!/bin/bash

samples=(Mock_72hpi_S{1..3} SARS-CoV-2_72hpi_S{7..9})

rawdir=../rawdata

prefix=seq-quant1   # Change 


for read in ${samples[*]} 
do
    salmon quant -i ../salmon_sa_index_hg19 -l A --seqBias -r $rawdir/$read.fastq.gz -p 8 --validateMappings -o $prefix/${read}.quant
done
```

2nd run: 

```bash

#!/bin/bash

samples=(Mock_72hpi_S{1..3} SARS-CoV-2_72hpi_S{7..9})

rawdir=../rawdata

prefix=seq-quant2   # Change 


for read in ${samples[*]} 
do
    salmon quant -i ../salmon_sa_index_hg19 -l A --seqBias -r $rawdir/$read.fastq.gz -p 8 --validateMappings -o $prefix/${read}.quant
done

```


### 4. without --gcBias & --seqBias 

1st run:

```bash

#!/bin/bash

samples=(Mock_72hpi_S{1..3} SARS-CoV-2_72hpi_S{7..9})

rawdir=../rawdata

prefix=default-quant1


for read in ${samples[*]} 
do
    salmon quant -i ../salmon_sa_index_hg19 -l A -r $rawdir/$read.fastq.gz -p 8 --validateMappings -o $prefix/${read}.quant
done
```

2nd run:

```bash
#!/bin/bash

samples=(Mock_72hpi_S{1..3} SARS-CoV-2_72hpi_S{7..9})

rawdir=../rawdata

prefix=default-quant2


for read in ${samples[*]} 
do
    salmon quant -i ../salmon_sa_index_hg19 -l A -r $rawdir/$read.fastq.gz -p 8 --validateMappings -o $prefix/${read}.quant
done
```

