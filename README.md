# Replication for "Registered Report: Grammar Mutation for Testing Input Parsers"

##  Overview

This is the virtual container replication package for
 "Grammar Mutation for Testing Input Parsers"
 which was submitted as a registered report.

The container containes all scripts and tools necessary to reproduce the preliminary results shown in the registered report.

The Replication package is provided as Zenodo DOI is

```
https://doi.org/10.5281/zenodo.7947814
```

### Time for Evaluation

The generation time for json inputs is set to 2 hours: 1 hour for Grammarinator, and 1 hour for Gmutator.
The evaluation time estimated is 10 hours.
The complete run may take up to 12 hours.

## Prerequisites

### RAM
Experiments were done in an Ubuntu machine with 4GB of RAM. And 4 CPU cores.

##  Getting started

Install the following software:

* Docker version 23.0.1

Next, download the following files from the Zenodo DOI
to the directory `replication`

* gmutator.tar

**Check:** change to `replication`, and ensure that the following files are
present:

```
$ cd replication
$ ls
gmutator.tar

$ du -ksh gmutator.tar
2.7G    gmutator.tar

$ md5sum gmutator.tar
995d0f1626ed347126bf293d7606d8b6  gmutator.tar
```
