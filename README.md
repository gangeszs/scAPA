ScAPA
================

This is a package and a shell script for alternative polyadenylation analysis of single-cell RNA-seq data. The shall script "scAPAscript.R" take as an input bam files generated by tenx 3' RNA seq and the results of cell clustering.

Prerequisites
=============

1.  Fasta and chromosome length files for Human (hg19) or (and) Mouse (mm10). Can be downloaded from [UCSC website](http://hgdownload.cse.ucsc.edu/goldenPath/mm10/bigZips/)
2.  [Samtools](http://www.htslib.org/download/) version 0.1.19-96b5f2294a or above.
3.  [Bedtools](https://bedtools.readthedocs.io/en/latest/content/installation.html) version v2.27.1-17-gf59480f or above.
4.  [Homer](http://homer.ucsd.edu/homer/introduction/install.html) version v4.8.3 or above. Uses homer's "MakeTagdirectory" and "findPeaks".
5.  [UMI\_tools](https://github.com/CGATOxford/UMI-tools/blob/master/doc/QUICK_START.md) test with version
6.  [Drop-seq\_tools-2.2.0](https://github.com/broadinstitute/Drop-seq/releases/tag/v2.2.0)
7.  R version 3.5.3, and above.
8.  Optional: [ChangePoint](https://sourceforge.net/projects/utr/files/), version 0.1.1

Installing
==========

-   Install all the above.
-   Install the R packege devtools. In R:

<!-- -->

    ## install.packages("devtools")

-   Download scRNAscript folder.
-   Open configfile.txt. Fill in the paths to the fasta files, chromosome length files, and all the softwere as instructed in the file. Leave "PATH" if the tool is in your PATH environment variable. Save your changes.

Using scAPA shell script
========================

Preparing the files
-------------------

Put in one directory the following files (and only those files):

**1. Single-cell RNA seq BAM files**

BAM files aligned using cell ranger counts. Cell barcode is CB, and the molecular barcode is UB. The name of each BAM file should be of the following format: sample.name.BAM. Avoid underscores in the names.

**2. Cluster annotations**

Tab-delimited two column files with no header. The first column is the cell barcodes (CB). The second is the cluster assigned to the cell. Each file corresponds to a sample (BAM). Notice that the cell barcodes are the same as in the BAM. For example, if the end of the barcode in the BAM file is "-1", it should be the same in the text file. The names of the files should be of the following format: clusters\_sample.name.txt, where the sample names matches those of the BAM file.

Usage
-----

Run the script as follow:

    ## path.to.R/bin/Rscript path.to.scAPAshellscript/scAPA.shell.script.R -p <path.to.files> -org <organism> [options]

&lt;path.to.files&gt; is the path to the directory with BAM and cluster anotations tex files. Do not add / in the end of the path. -org The organism is either Mm for a mouse (mm10) or Hs for human (hg19). For a list of options, type:

    ## path.to.R/bin/Rscript path.to.scAPAshellscript/scAPA.shell.script.R --help

Output
------

For a full list of outputs and explanation of the outputs, see the file "Output.html" In the files directory, The script creates the directory scAPA and in it a directory called outputs. The output of the analysis includes, among others, a table of p-values for dynamical APA events. A file with p-values per peak for 3'UTRs with multiple peaks, and a file with a mean proximal (or intronic) PUI for each cell from the cluster annotations file.

Inside, the script creates a log file "scAPA.script.log" logging the script's progress. The directory scAPA/Log.files contains Logs from the tools being used (such as UMI tools). The directory scAPA/temp contains temporary files created. This directory is deleted when the script finishes. At the end of the script the directory wi

Authors
-------

-   Eldad Shulman
-   Dr. Ran Elkon

License
-------

This project is licensed under the BSD 3 License - see the LICENSE.md file for details
