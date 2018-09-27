# Instructions of tr2lor project related code

## Data

### Simulation data processing

Simulated data is only single gamma, which requires composite to become events.

Useage `julia $INCIDENT_ROOT/code/bin/composite source.npy config.yml taret.h5`

#### Environments

Add path of Incident project as environment variable `INCIDENT_ROOT`.
```shell
export INCIDENT_ROOT=<path_of_cloned_directory>
```

#### Install of julia

download julia from [julia official site](https://julialang.org/downloads/)

following instructions of official site.

add environment variable `JULIA_LOAD_PATH` by adding the following line to 
`~/.bashrc` or any other related files.

```shell
export JULIA_LOAD_PATH=$INCIDENT_ROOT/Incident:$JULIA_LOAD_PATH
```

enter julia REPL by entering `julia<enter>` in shell, then add packages by:
```julia
>>>using Pkg
>>>Pkg.Add("NPZ")
>>>Pkg.Add("StaticArrays")
>>>Pkg.Add("Statistics")
>>>Pkg.Add("JLD2")
```
etc, add all packages required, test by run composite command.

### Experiment data processing

## Train

## Evaluate and metric

