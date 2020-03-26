# Rule-based SIR models for CoViD-19

One of the simplest models to simulate an outbreak of diseases such as the flu or measles is the SIR model. It models the transition of a population from being susceptible (S) to a disease to being infectious (I) and finally recovered (R). The model was first published in 1927 (https://doi.org/10.1098/rspa.1927.0118).

All models in this repository have been implemented for the rule-based modeling language ML-Rules (see https://doi.org/10.1145/2998499).

## How to run the models

Please consult the ML-Rules quickstart project (https://git.informatik.uni-rostock.de/mosi/mlrules2-quickstart) and download everything needed to run the ML-Rules editor.
When the ML-Rules Sandbox is opened, you can simply load the model (*.mlrj), choose the end time for the simulation and click on "start simulation".

## Available models:

 * Rule-based general SIR model (See directory [directory SIRmodel](./SIRmodel) for more information)
 * Rule-based CoViD-19 model from the Neher Lab
 * Rule-based SIR model for for CoViD-19

## Parametrization for Germany and Mecklenburg-Western Pomerania

tbc.

## License

[GNU GPL v3.0](./LICENSE)