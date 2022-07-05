# peptide-mutation-finder
This notebook automates the process of figuring out changes in protein sequences as a result of mutations found from genome sequencing. Written by Hunter King (https://github.com/retnuh-k/) under the guidance of Dr. Songtao Jia and Yimeng Fang as part of the Jia Lab (http://jia.biology.columbia.edu/).

Colab link (might need LionMail to access): https://colab.research.google.com/drive/19hQxIFA3o0Rh4LYsh3U-HaHrO3-TvdqY?usp=sharing

**Required input files:**
*   mutation_comparison_tsv_file - file describing the differences in two vcf files outputted by vcftools --gzdiff function (see http://vcftools.sourceforge.net/man_latest.html)
*   geneome_tsv_file - a tsv file of the organism's feature coordinates in gff3 file format (can create by removing header starting with '#' from gff3 file and saving as tsv)
*   genome_fasta_file - a fasta file with each chromosome sequence headers written as ">[chromosome name]"

**Full pipeline steps**
1.   Obtain sequencing data of strain of interest and wild type
2.   Download reference genome fasta file
3.   Run freebayes variant detector (see https://github.com/freebayes/freebayes) on both strain and wild type .bam files against the reference genome to get a vcf (variant call file) for each
4.   Filter each vcf file by quality (recommended between 10 and 30) and (optionally) depth using vcffilter or equivalent (https://github.com/vcflib/vcflib)
5.   gzip filtered vcf files
6.   Compare vcf files using vcftools (http://vcftools.sourceforge.net/man_latest.html), run "vcftools --gzvcf test_strain.vcf.gz --gzdiff wild_time.vcf.gz --diff-site --out comparison_output_file". This step ensures that only mutations not shared with the wild type are analyzed.
7.   Rename comparison output file to have .tsv file extension
8.   Download genome fasta file and reformat per the above specifications
9.   Download genome coordinate gff3 file, remove header and save as .tsv file
10.  Upload required files to notebook, specify filenames in code block below, and run notebook 

**Sample input files**
* TT_v_WT_DP10QU20.tsv - Mutation comparison tsv file for S. Pombe test strain versus wild type with filters Quality > 20 and Depth > 10
* Schizosaccharomyces_pombe_all_chromosomes.tsv - Genome tsv file for Schizosaccharomyces pombe
* pombe_genome.fasta - Genome fasta file for Schizosaccharomyces pombe downloaded and modified from pombase.org
