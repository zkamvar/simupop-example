#simupop-example

## Update 2016-08-31

Over in https://github.com/BoPeng/simuPOP/issues/3, I had found the problem was the [order in which feather and simuPOP were loaded][0]:

```
git clone https://github.com/zkamvar/simupop-example
cd simupop-example/testpopp
# fails
python -c 'import feather;from simuPOP import *;loadPopulation("seed_0_sex_0.0000_gen_00000_rep_00.pop")'
# works
python -c 'from simuPOP import *;import feather;loadPopulation("seed_0_sex_0.0000_gen_00000_rep_00.pop")'
```

Commit 54080d0867a0ca31dd89864af1e4a095febcfdc8 fixed the error by placing feather after simuPOP in import order.

## Previously failing command:

A working example of a failing simuPOP script

This command fails on Ubuntu 14.04 but works on OSX 10.11.6 with python version 3.4 via conda:

```sh
python dir2feather.py --prefix testpop -z --group_by rep
```

On Ubuntu, it raises a ValueError: Failed to Load Population testpop/seed_0_sex_0.0000_gen_10000_rep_01.pop.

I'm trying to figure out why it would fail like this on ubuntu, but be fine on OSX

# Files

 - [dir2feather.py](dir2feather.py) will convert directories of population files to feather format and zip them up
 - [pop2feather.py](pop2feather.py) is a little mis-labeled, but it contains the utilities for dir2feather to create pandas DataFrames
 - [testpop](testpop) contains simuPOP population files.
 - [simupop_environment.yml](simupop_environment.yml) is the yaml file exported from conda describing the environment.

 
[0]: https://github.com/BoPeng/simuPOP/issues/3#issuecomment-243834067
