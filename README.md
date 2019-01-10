# lumpyR2sh
## Purpose
This is an execuetable R file (intended to run from the command line) that takes a directory of bams and outputs two different bash wrapper scripts (`_lumpysetup.sh` and `_lumpycall.sh`) corresponding to the [lumpy-sv](https://github.com/arq5x/lumpy-sv) pipeline. 

## Usage
### Lumpy Setup
From the command line, you would run the script as follows:   

> Rscript  lumpyR2sh -A lumpysetup -I \<path\_input\_dir\> -O \<path\_output\_dir\> -M \<name\_master\_bash\> -R \<library\_read\_size\>


The outputted master bash script will be placed in your specified output directory. The setup function must be called first in order to create the "empirical insert size statistics on each library in the BAM file" (from `pairend_distro .py`) for `lumpy-sv` to run. **Note: you must run the bash script to generate the files.** 

### Lumpy Call
From the command line, you would run the script as follows:   

> Rscript lumpyR2sh -A lumpycall -I \<path\_input\_dir\> -O \<path\_output\_dir\> -M \<name\_master\_bash\> -R \<library\_read\_size\>

**Note: you must run the bash script to generate the files.** 



### Details
Both master bash script will expect that samtools, scripts/extractSplitReads_BwaMem, scripts/pairend_distro.py (from lumpy) and lumpy are execuetable from your environment. 