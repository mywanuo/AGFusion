# Annotate Gene Fusion (AGFusion)
For a given gene fusion, AGFusion will predict the cDNA, CDS, and protein sequences resulting from fusion of all combinations of transcripts and save them to fasta files. AGFusion can also plot the protein domain architecture of the fusion transcripts. Currently, only PFAM domains are used to annotate gene fusions. CDS and protein sequences are only outputted for fusions that can form a protein.

Docs are at http://pythonhosted.org/agfusion/

## Table of Contents

- [Examples](#Examples)
  * [Basic Usage](#Basic-Usage)
  * [Plotting wild-type protein](#Plotting-wild-type-protein)
  * [Canonical gene isoforms](#Canonical-gene-isoforms)


## Examples

### Basic Usage

You just need to provide the two fusion gene partners (gene symbol, Ensembl ID, or Entrez gene ID), their predicted fusion junctions in genomic coordinates, and the genome build. You can also specify certain transcripts with Ensembl transcript ID or RefSeq ID

Example usage from the command line:

```
agfusion \
  --gene5prime ENSMUSG00000022770 \
  --gene3prime ENSMUSG00000002413 \
  --junction5prime 31684294 \
  --junction3prime 39648486 \
  --genome GRCm38 \
  --out DLG1-BRAF
```

The protein domain structure of the DLG1-BRAF fusion:

![alt tag](https://github.com/murphycj/AGFusion/blob/master/doc/ENSMUST00000064477-ENSMUST00000002487.png)

The exon structure of the DLG1-BRAF fusion:

![alt tag](https://github.com/murphycj/AGFusion/blob/master/doc/ENSMUST00000064477-ENSMUST00000002487.exon.png)

### Plotting wild-type protein

You can additionally plot the wild-type proteins for each gene with --WT flag.

```
agfusion \
  --gene5prime ENSMUSG00000022770 \
  --gene3prime ENSMUSG00000002413 \
  --junction5prime 31684294 \
  --junction3prime 39648486 \
  --genome GRCm38 \
  --out DLG1-BRAF \
  --WT
```

### Canonical gene isoforms

By default AGFusion only plots the [canonical](http://useast.ensembl.org/Help/Glossary?id=346) gene isoforms, but you can tell AGFusion to include non-canonical isoform with the --noncanonical flag.

```
agfusion \
  --gene5prime ENSMUSG00000022770 \
  --gene3prime ENSMUSG00000002413 \
  --junction5prime 31684294 \
  --junction3prime 39648486 \
  --genome GRCm38 \
  --out DLG1-BRAF \
  --noncanonical
```

### Domain names and colors

You can change domain names and colors:

```
agfusion \
  --gene5prime ENSMUSG00000022770 \
  --gene3prime ENSMUSG00000002413 \
  --junction5prime 31684294 \
  --junction3prime 39648486 \
  --genome GRCm38 \
  --out DLG1-BRAF \
  --colors "Serine-threonine/tyrosine-protein kinase catalytic domain;red" \
  --colors "L27_1;#00cc00" \
  --rename "Serine-threonine/tyrosine-protein kinase catalytic domain;Kinase" \
  --rename "L27_1;L27"
```

![alt tag](https://github.com/murphycj/AGFusion/blob/master/doc/ENSMUST00000064477-ENSMUST00000002487-recolorRename.png)

### Re-scaling protein length

You can rescale the protein length so that images of two different fusions have appropriate relative lengths when plotted side by side:

```
agfusion \
  --gene5prime ENSMUSG00000022770 \
  --gene3prime ENSMUSG00000002413 \
  --junction5prime 31684294 \
  --junction3prime 39648486 \
  --genome GRCm38 \
  --out DLG1-BRAF \
  --colors "Serine-threonine/tyrosine-protein kinase catalytic domain;red" \
  --colors "L27_1;blue" \
  --rename "Serine-threonine/tyrosine-protein kinase catalytic domain;Kinase" \
  --rename "L27_1;L27" \
  --scale 2000
agfusion \
  --gene5prime FGFR2 \
  --gene3prime DNM3 \
  --junction5prime 130167703 \
  --junction3prime 162019992 \
  --genome GRCm38 \
  --out FGFR2-DNM3 \
  --rename "Immunoglobulin I-set;I-set" \
  --rename "Dynamin GTPase effector;Dynamin" \
  --rename "Serine-threonine/tyrosine-protein kinase catalytic domain;Kinase" \
  --colors "Serine-threonine/tyrosine-protein kinase catalytic domain;red" \
  --scale 2000
```

![alt tag](https://github.com/murphycj/AGFusion/blob/master/doc/ENSMUST00000064477-ENSMUST00000002487-rescale.png)
![alt tag](https://github.com/murphycj/AGFusion/blob/master/doc/ENSMUST00000122054-ENSMUST00000070330-rescale.png)

# Advanced Usage

### Building your own database

You need to have mysql and the MySQLdb python package installed.

# Installation

First you need to install pyensembl (and the other dependencies listed at the bottom of this readme) and download the reference genome you will use by running one of the following.

For GRCh38:

```
pyensembl install --release 84 --species homo_sapiens
```

For GRCh37:

```
pyensembl install --release 75 --species homo_sapiens
```

For GRCm38:

```
pyensembl install --release 84 --species mus_musculus
```

Then you can install AGFusion via the following:

```
pip install agfusion
```

# Dependencies

- python 2.7.8
- pyensembl>=0.9.5
- matplotlib>=1.5.0
- biomart>=0.9.0
- pandas>=0.18.1
- biopython>=1.67
- jsonpickle>=0.9.

# License

MIT license

# Citing AGFusion

Manuscript under review. You can cite bioRxiv for now: http://dx.doi.org/10.1101/080903
