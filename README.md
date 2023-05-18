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

* Docker

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
### Importing the image

Execute the following command to load the docker image:

```
$ docker load -i gmutator.tar
Loaded image: gmutator-replication:json
```

### Bring up the virtual container

The following command will bring up the virtual container, and access the container.

```
$ docker run --name gmutator-rep -it gmutator-replication:json /bin/bash
```

### Reproducing json experiments

To run all learning tasks, run command:

```
$ cd home/gmutator/json
$ make
```

This will execute all: Generation scripts and evaluation scripts.
