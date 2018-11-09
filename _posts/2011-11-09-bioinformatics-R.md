---
layout: post
title: "How to plot length distribution of RNA-seq reads"
date: 2018-11-09
category: ["computer", "R", "genomics", "bioinformatics"]
author: "Sung-Cheol Kim"

---

# How to plot a length ditribution of RNA-seq reads?

One of the basic steps in RNA-seq analysis is to plot a length ditribution. There are several ways of doing it.

## Using unix commands

[link in Biostars](https://www.biostars.org/p/72433/)

```
awk 'NR%4 == 2 {lengths[length($0)]++} END {for (l in lengths) {print l, lengths[l]}}' file.fastq
```

First part of awk commands tell the program to pick up the second line group by each 4 lines. And second part saves length of that line as a component of lengths matrix. And the last part is that at the end of the process, print lengths matrix showing length and count.

```
cat reads.fastq | awk '{if(NR%4==2) print length($1)}' | sort -n | uniq -c > read_length.txt
```

With this command, you can save lengths matrix as a file. This time you can put `sort` and `uniq` to make sure that the list are sorted and has only unique lengths.

## Using BBMap utilities

```
readlength.sh in=reads.fq out=histogram.txt
```

This is really fast and this program can handle multiple formats of read files such as fastq, fastq.gz, fasta, sam, bam


