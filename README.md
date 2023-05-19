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

## Replicating json experiments

Before running experiments, we can edit the configuration variable in file `config`

```
$ cd home/gmutator
$ cat config
GEN_TIME = 3600 # in seconds
GEN_TIME_OG = 0 # Ratio of original grammar-based generation to the total mutation generation.
```

GEN_TIME sets the generation time.

GEN_TIME_OG sets the ration of the original-grammar-based generation time to the total Gmutator generation time. For example, if we want Gmutator to generate inputs using the orignal grammar for half of the time, and using mutant grammars for half of the time, then we set GEN_TIME_OG to 0.5


To run all json experiments, run:

```
$ cd json
$ make
```

This will execute all: Generation scripts and evaluation scripts.

### Reproducing json results

All results are stored in the directory `results`. Which contains two subfolders: `org` and `mut`. Subfolder `org` contains all experiment results related to Grammarinator generated inputs. While subfolder `mut` contains all experiment results related to Gmutator generated inputs.

#### Branch coverage

To show branch coverage results for cJSON program with Grammarinator generated inputs, do:

```
$ cat results/org/cov/report-cjson.txt
------------------------------------------------------------------------------
                           GCC Code Coverage Report
Directory: ../../bench/json/cjson
------------------------------------------------------------------------------
File                                    Branches   Taken  Cover   Missing
------------------------------------------------------------------------------
cJSON.c                                      854     203    23%   76,99,104,109,111,154,161,172,182,188,195,205,220,224,228,274,282,315,345,349,378,383,389,396,401,406,409,423,427,440,448,464,484,490,500,508,515,522,524,548,552,556,587,624,654,660,706,715,720,730,738,756,761,813,818,836,842,845,855,857,870,881,887,900,902,911,965,970,975,986,991,1009,1020,1032,1035,1040,1048,1053,1059,1063,1068,1100,1106,1113,1116,1124,1138,1143,1166,1172,1183,1196,1214,1221,1228,1235,1243,1248,1253,1258,1271,1276,1280,1289,1298,1311,1318,1346,1352,1360,1367,1380,1408,1410,1426,1441,1449,1458,1460,1465,1467,1469,1474,1485,1502,1508,1515,1521,1534,1566,1580,1582,1597,1612,1618,1620,1627,1633,1635,1639,1643,1651,1657,1659,1664,1671,1678,1680,1684,1689,1699,1700,1704,1707,1725,1732,1747,1753,1764,1776,1782,1784,1791,1826,1832,1848,1855,1863,1900,1905,1913,1921,1945,1955,1966,1978,1990,2002,2014,2026,2038,2050,2062,2073,2078,2083,2089,2103,2145,2151,2160,2172,2177,2185,2189,2193,2207,2217,2223,2249,2260,2271,2282,2284,2293,2299,2303,2319,2323,2336,2348,2358,2369,2373,2386,2397,2413,2419,2422,2427,2448,2455,2458,2463,2484,2491,2494,2499,2520,2527,2530,2535,2558,2564,2572,2575,2580,2582,2583,2589,2595,2598,2602,2621,2633,2638,2640,2644,2649,2653,2657,2660,2665,2668,2674,2678,2680,2701,2711,2721,2732,2741,2751,2761,2771,2781,2791,2801,2807,2824,2829,2838,2846,2850,2862,2864,2874,2885,2889,2894,2902,2905,2910,2944,2951
------------------------------------------------------------------------------
TOTAL                                        854     203    23%
------------------------------------------------------------------------------
```

#### Program crashes

To show AddressSanitizer report for parson program after running Gmutator generated inputs, run:

```
$ cat results/mut/asan/parson/report.txt
ASAN Report - 7 : parson
Total inputs: 0
Issues found: 0

ASAN Report - 8 : parson
Total inputs: 0
Issues found: 0

ASAN Report - 9 : parson
Total inputs: 0
Issues found: 0

ASAN Report - 1 : parson
Total inputs: 40
Issues found: 0

ASAN Report - 4 : parson
Total inputs: 40
Issues found: 0

ASAN Report - 5 : parson
Total inputs: 16
Issues found: 0

ASAN Report - 6 : parson
Total inputs: 0
Issues found: 0

ASAN Report - 2 : parson
Total inputs: 40
Issues found: 0

ASAN Report - 3 : parson
Total inputs: 40
Issues found: 0
```

The report is partitioned into 9 parts. This is because inputs are grouped into 9 sets, where each set is evaluated independently.

#### Differential testing between the SUT and the parser generated from the original grammar

This shows number of inputs accepted by the original grammar, and number of inputs accepted by SUT `cJSON`:

```
$ cat results/mut/diff-test-g/cjson/report.txt

Differential testing between grammar-generated parser and cjson, when running Gmutator generated inputs:
Total inputs: 176
Issues found: 0
Inputs valid according to grammar: 149
Inputs valid according to cjson: 153
```

`Issues` here refers to the number of SUT crashes found.

#### Differential testing across SUTs

This shows number of inputs accepted by SUT `cJSON`, and number of inputs accepted by SUT `parson`, for Grammarinator generated inputs:

```
$ cat results/org/diff-test-p/report.txt

Differential testing between programs cJSON and parson:
Total inputs: 1440
Issues found: 0
Valid cJSON: 1308
Valid parson: 1231

```

`Issues` here refers to the number of SUT crashes found.
