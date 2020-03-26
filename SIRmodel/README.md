# Rule-based general SIR model

See [directory SIRmodel](./SIRmodel) for more information. The model is based upon the ODE model shown in https://en.wikipedia.org/wiki/Compartmental_models_in_epidemiology#The_SIR_model.

## General ODE-based SIR model
The most general model for an epidemic or pandemic is the SIR model with the following three equations:

$$\frac{dS(t)}{dt} = - \frac{\beta}{N} S(t) I(t)$$
$$\frac{dI(t)}{dt} =   \frac{\beta}{N} S(t) I(t) - \gamma I(t)$$
$$\frac{dR(t)}{dt} =   \gamma I(t)$$

with the entire population

$$ N_\text{total} = S(t) + I(t) + R(t) =  const$$

and the kinetic parameters

$$ \beta = \frac{1}{\tau_C}$$

and

$$ \gamma = \frac{1}{\tau_R}$$

where

$$$ \tau_C $$$

is the typical time between contacts and

$$$ \tau_R $$$

is the typical time until recovery when infected.


We call
$$R_0 = \frac{\beta}{\gamma}$$

the basic reproduction number or basic reproduction ratio. It shows how many people may be infected by one person.

## General rule-based SIR model

### Conversion of ODEs to rules
In order to have all rules (the number of rules equals the number of kinetic parameters in the ODEs), we must write all rules of every equation and then combine those that share the same kinetic parameter.

1. The first equation as a rule (in ML-Rules syntax):
``` S:s + I:i -> I @ (beta / nTotal) * #s * #i;```

2. The second equation as rules (in ML-Rules syntax):
``` S:s + I:i -> S + I + I @ (beta / nTotal) * #s * #i;```
``` I:i ->  @ gamma * #i;```

3. The third equation as a rule (in ML-Rules syntax):
``` I:i -> R + I @ gamma * #i;```

We now combine all rules with ```(beta / nTotal) * #s * #i``` as reaction rate and then all rules with ```gamma * #i``` as reaction rate.

1. First rule (infection of susceptible person):
``` S:s + I:i -> 2 I @ (beta / nTotal) * #s * #i; ```

2. Second rules (recovery of infected person):
``` I:i -> R @ gamma * #i;```


### ML-Rules model version of general SIR model
Together with the two rules, we can now build a ML-Rules version of the general SIR model. It can be found in [SIR.mlrj](.SIR.mlrj).



