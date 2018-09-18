POEM is a pipeline which can predict operons and core operons from metagenomic genome/assembly or short reads.

## Requirement
==============

Make sure that you have the following installed

1.  Python2.7 (Recommend [Anaconda](https://www.anaconda.com/ "https://www.anaconda.com/")) and Packages:
    1. Networkx
    2. Biopython (version >=1.68)
    3. Numpy (version >= 1.11.2)
    4. Keras (version >= 2.2.2)
2.  [Diamond](https://github.com/bbuchfink/diamond "https://github.com/bbuchfink/diamond") (version >= 0.8.18)
3.  [MetaGeneMark](http://exon.gatech.edu/GeneMark/ "http://exon.gatech.edu/GeneMark/"):

        make sure to add path of gmhmmp to $PATH environment variable

4.  [CD-hit](http://weizhongli-lab.org/cd-hit/ "http://weizhongli-lab.org/cd-hit/")
5.  [IDBA-UD](https://github.com/loneknightpy/idba, "https://github.com/loneknightpy/idba")


## Installation
===============

$ git clone https://github.com/Rinoahu/POEM

$ cd ./POEM

$ bash ./install.sh

## Example
===============

example directory contain a genome fasta file of E.coli, run the script named runme.sh to test the pipeline

$ cd ./example

$ bash ./runme.sh genome



## Usage
===============

For short reads:

    $ bash ./bin/run_poem.sh -f reads.fsa -a y

    reads.fsa is single fasta file. If the reads are paired-end files in fastq or fasta format, 
    use the fq2fa of IDBA_UD to convert them to  a single fasta file.

For genome/assembly:

    $ bash ./bin/run_poem.sh -f genome.fsa -a n

    genome.fsa is the genome/assembly fasta file.


## Output
===============

POEM will create a directory named read.fasta_output to save the results. The results include serveral file:

    1.  input.fsa:
        The contigs or saffolds of IDBA-UD output in fasta format

    2.  input.fsa_gmk_aa.fsa and input.fsa.gff:
        The fasta file of protein sequence and gff file generated by prediction of MetaGeneMark on input.fsa from step 1

    3.  input.fsa.cdhit and input.fsa.cdhit.clstr:
        The cd-hit clustering results of input.fsa_gmk_aa.fsa from step 2

    4.  input.fsa_aa.fsa:
        Filtered input.fsa_gmk_aa.fasta according to the clustering result of step 3

    5.  input.fsa.flt.blast8:
        Blastp results in -m 8 tabular format of input.fsa_aa.fsa from step 4 against COG database

    6.  input.fsa.flt.blast8.flt:
        Filtered blastp output of step 5. The hits with identity < 80% are removed

    7.  input.fsa.cog:
        COG annotation for protein sequence of step 4

    8.  input.fsa.locus:
        The file records the gene's locus on genome

    9.  input.fsa.adjacency and input.fsa.operon:
        Predicted operonic adjacency and full operon of step 8

    10. input.fsa.cog_adjacency:
        This file contain two part:
        1). The COG adjacency of operonic adjacency
        2). Operon's core COG and its closest real operon

    11. input.fsa.core_cog_adjacency:
        The core COG adjacency

    12. input.fsa.core_network.sif, input.fsa.core_node.attrs and input.fsa.core_edge.attrs:
        Network, node attribute and edge attribute extracted from step 11 for cytoscape visualization





