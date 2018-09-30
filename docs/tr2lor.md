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
first make sure you have `Data Version Control(DVC)`

easy setup by `pip install dvc`

also see [https://dvc.org/](https://dvc.org/) for setup,reference or tutorial.

prepare `raw data`(eg. simu3d0.npy) in gluster and `split.json` config file in
current directory .then run cmd:
```shell
>>>dvc run -d your_raw_data_dir -d split.json -o train.npy -o test.npy -o valid.npy incident data split -c split.json
```
prepare `composite.yml`config file in the same directory and the source code `composite.jl`(saving at
`/code/bin` by default) then run cmd:
```shell
>>>dvc run -d composite.yml -d train.npy -o train_com.h5 julia your_composite.jl_dir train.npy composite.yml train_com.h5
>>>dvc run -d composite.yml -d test.npy -o test_com.h5 julia your_composite.jl_dir test.npy composite.yml test_com.h5
>>>dvc run -d composite.yml -d valid.npy -o valid_com.h5 julia your_composite.jl_dir valid.npy composite.yml valid_com.h5
```
## Train
make sure you have `train_auto.py` and `train.sh` (if you want to train with your own new config try to modify
`train_auto.py.config`) then run cmd:
```shell
>>>python train_auto.py
```
## Evaluate and metric
```
>>>python train_auto.py
```
this cmd actually includes train,evaluate and metric and by run the cmd you will finally get several dirs like
`/model-1-2-3/`.for each dir there are respectively `/model/`, `evaluate results(start by evaluate_ ) `and `metric results(
start by apply_metric_results_)`.

## construct pipeline

### complete the pipeline graph
once you run the whole cmd above (start from experiment data processing) then the only thing left is
collecting all `model/` info  by one cmd for pipeline.make sure you have `produce_pipeline.py` and 
`produce.sh` then run cmd:
```shell
>>> python produce_pipeline.py
``` 
finally a file named `auto_pipeline.dvc` will produce.it also means a ML-pipeline has been
built.if any file in the pipeline modified ,then by run the cmd:
```shell
>>> dvc repro auto_pipeline.dvc
```
the whole pipeline will rerun until it produce the results we want.

### visualization of pipeline
run the cmd:(`-c` show the concrete cmd in the pipeline `--ascii` show a graph-like pipe)
```shell
dvc pipeline show auto_pipeline.dvc   
dvc pipeline show auto_pipeline.dvc -c
dvc pipeline show auto_pipeline.dvc --ascii

```

