# data-sharing-abm-model
Agent Based Model looking at the effect of openness on data sharing and innovation by companies

## Documentation

You can find a full description of the model in the `model_document` folder.

To create the `pdf` from the `md`, you can use pandoc: `pandoc model_document.md -f markdown --pdf-engine=xelatex -o model_document.pdf`

## Accompanying demo

A Dash app is available on [data-sharing-abm-demo](https://github.com/theodi/data-sharing-abm-demo). This app allows you to explore the model without having to run it yourself.

## How to run the model

To ensure you have the right python libraries to run the simulation, make a conda environment using the `environment_simulation.yaml`. A detailed instruction can be found below.

Activate the environment in the terminal by using `conda activate odi`.

A python programme, `run_simulation.py`, can be used to execute one rep of the simulation in the command line. It takes two arguments:
```
-i Path to a yaml with the parameters for the simulation
-o Output directory
```
and the command looks as follows:

`python run_simulation.py -o ./test -i model_parameters.yaml`.

We have provided a yaml with input values and their meaning, but the user can use any yaml that has all the parameters (except for the scenario parameters).

Currently, the output is visualised a set of figures, but users can change that easily to save the raw data.


## Relevant files for the model

* `simulation.py`: has the main function `run` to run the model
* `setup_sim.py`: sets up categories, needs, capital, privacy score, privacy concern, porting, ...
* `needs.py`: wraps the functions used to draw from need profiles
* `beta_distr`: functions that derive the parameters $\alpha, \beta$ for the beta distribution based on the mode and variance provided by the user
* `data_handling.py`: mostly implemented in numba for speed gains, this module deals with data requests and porting data
* `figures.py`: definition of the figures that are generated by `run_simluation.py`
* `innovation.py`: all functions to do with innovation
* `privacy_scenario.py`: contains the function needed to delete data in the scenario
* `tracking.py`:  an object to keep track of what happens during the simulation. Needs to be created before the tick loop starts, and ingests data at the end of every tick. Flushes at the end of the simulation to give the outputs of the model.
* `utility.py`: functions regarding consumer choices
* `utils.py`: contains some helper functions


## Installing conda and creating environments

In order to use conda environments, install [Miniconda](https://conda.io/miniconda.html) or Anaconda if you don't have it yet.

To create the correct environment to run the app locally, use `conda env create -f /path/to/environment_simulation.yaml`. This will create an environment named `odi`.  
