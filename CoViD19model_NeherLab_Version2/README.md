# Rule-based implementation of CoViD-19 model by Neher Lab

This model is a translation of Version 2 of the ODE model implemented by Richard Neher et al. to the modelling language `mlrules`. The equations can be seen at https://covid19-scenarios.org/about, the implementation at https://covid19-scenarios.org/ and the repository at https://github.com/neherlab/covid19_scenarios.

## Integrity of the Translation

Although attention was payed to reproducibility, there is no warranty that the translation is complete nor that the results are the same as in the original.
Right now, the following parameters are missing:

- imports per day

## Simulate the model

To simulate the model, the easyest way is to use the [mlrules quickstart project](https://git.informatik.uni-rostock.de/mosi/mlrules2-quickstart). Keep in mind, that the mlrules sandbox is for demonstration purposes only. To properly simulate mlrules models, use [SESSL](https://git.informatik.uni-rostock.de/mosi/sessl/-/wikis/home).
