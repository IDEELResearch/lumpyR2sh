# lumpyR2sh

## Installation
git clone <https://github.com/IDEELResearch/lumpyR2sh.git>   
OR  
If you are on the longleaf server, the function is execeutable by:     
`proj/ideel/bin/lumpyR2shpkg/lumpyR2sh`

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

### SVTyper Call
This is the post-processing option provided by [`SVTyper`](https://github.com/hall-lab/svtyper) and recommended by `lumpy`. 

From the command line, you would run the script as follows:   

> Rscript lumpyR2sh -A svtypercall -I \<path\_input\_dir\> -O \<path\_output\_dir\> -M \<name\_master\_bash\> -R \<library\_read\_size\>

**Note: you must run the bash script to generate the files.** 



### Details
Both master bash script will expect that `samtools`, `extractSplitReads_BwaMem` (from `lumpy`), `pairend_distro.py` (from `lumpy`), `lumpy`, and `SVTyper` are execuetable from your environment. 

## Example

> `# step 1`  
> Rscript lumpyR2sh -A lumpysetup -I "\<mydir/aln/\>" -O "\<mydir/lumpyout/\>" -M "{Proj\_Name}\_lumpy2Rsh\_wrapper" -R 75  
>  
> bash {Proj\_Name}\_lumpy2Rsh\_wrapper\_lumpysetup.sh
>  
> `# step 2`
>  
> Rscript lumpyR2sh -A lumpycall -I "\<mydir/aln/\>" -O "\<mydir/lumpyout/\>" -M "{Proj\_Name}\_lumpy2Rsh\_wrapper" -R 75 
>   
> bash {Proj\_Name}\_lumpy2Rsh\_wrapper\_lumpycall.sh
>  
> `# step 3`
>  
> Rscript lumpyR2sh -A svtypercall -I "\<mydir/aln/\>" -O "\<mydir/lumpyout/\>" -M "{Proj\_Name}\_lumpy2Rsh\_wrapper" -R 75 
>   
> bash {Proj\_Name}\_lumpy2Rsh\_wrapper\_svtypercall.sh