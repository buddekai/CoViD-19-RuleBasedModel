# Rule-based implementation of CoViD-19 model by Neher Lab

This model is based upon the ODE model implemented by Richard Neher et al. The equations can be seen at https://neherlab.org/covid19/about, the implementation at https://neherlab.org/covid19/ and the repository at https://github.com/neherlab/covid19_scenarios.

## ODE-based CoVid-19 model by Neherl Lab
The ordinary differential equations (ODEs) used by the Neher Lab for their CoViD-19 model are:

<p align="center">
1. The change in number of susceptible people for every age group
<!-- $$$\frac{dS_a(t)}{dt} = - \frac{\beta_a(t)}{N_\text{total}} S_a(t) \sum_b I_b(t)$$$ -->
<img src="https://latex.codecogs.com/gif.latex?%5Cfrac%7Bd%20S_a%28t%29%7D%7Bdt%7D%20%3D%20-%20%5Cfrac%7B%5Cbeta_a%28t%29%7D%7BN_%5Ctext%7Btotal%7D%7D%20S_a%28t%29%20%5Csum_b%20I_b%28t%29">

2. The change in number of exposed people for every age group (infected people without yet showing symptoms)
<!-- $$$\frac{dE_a(t)}{dt} = \frac{\beta_a(t)}{N_\text{total}} S_a(t) \sum_b I_b(t) - \frac{E_a(t)}{t_l}$$$ -->
<img src="https://latex.codecogs.com/gif.latex?%5Cfrac%7BdE_a%28t%29%7D%7Bdt%7D%20%3D%20%5Cfrac%7B%5Cbeta_a%28t%29%7D%7BN_%5Ctext%7Btotal%7D%7D%20S_a%28t%29%20%5Csum_b%20I_b%28t%29%20-%20%5Cfrac%7BE_a%28t%29%7D%7Bt_l%7D">

3. The change in number of infected people for every age group
<!-- $$$\\frac{dI_a(t)}{dt} = \frac{E_a(t)}{t_l} - \frac{I_a(t)}{t_i}$$$ -->
<img src="https://latex.codecogs.com/gif.latex?%5Cfrac%7BdI_a%28t%29%7D%7Bdt%7D%20%3D%20%5Cfrac%7BE_a%28t%29%7D%7Bt_l%7D%20-%20%5Cfrac%7BI_a%28t%29%7D%7Bt_i%7D">

4. The change in number of hospitalized people for every age group
<!-- $$$\frac{dH_a(t)}{dt} = (1-m_a) \frac{I_a(t)}{t_i} + (1-f_a) \frac{C_a(t)}{t_c} - \frac{H_a}{t_h}$$$ -->
<img src="https://latex.codecogs.com/gif.latex?%5Cfrac%7BdH_a%28t%29%7D%7Bdt%7D%20%3D%20%281-m_a%29%20%5Cfrac%7BI_a%28t%29%7D%7Bt_i%7D%20&plus;%20%281-f_a%29%20%5Cfrac%7BC_a%28t%29%7D%7Bt_c%7D%20-%20%5Cfrac%7BH_a%7D%7Bt_h%7D">

5. The change in number of critically ill people in intesive care units of hospitals people for every age group
<!-- $$$\frac{dC_a(t)}{dt} = c_a \frac{H_a}{t_h} - \frac{C_a(t)}{t_C}$$$ -->
<img src="https://latex.codecogs.com/gif.latex?%5Cfrac%7BdC_a%28t%29%7D%7Bdt%7D%20%3D%20c_a%20%5Cfrac%7BH_a%7D%7Bt_h%7D%20-%20%5Cfrac%7BC_a%28t%29%7D%7Bt_C%7D">

6. The change in number of recovered people (being immune) for every age group
<!-- $$$\frac{dR_a(t)}{dt} = m_a \frac{I_a(t)}{t_i} + (1-c_a) \frac{H_a(t)}{t_h}$$$ -->
<img src="https://latex.codecogs.com/gif.latex?%5Cfrac%7BdR_a%28t%29%7D%7Bdt%7D%20%3D%20m_a%20%5Cfrac%7BI_a%28t%29%7D%7Bt_i%7D%20&plus;%20%281-c_a%29%20%5Cfrac%7BH_a%28t%29%7D%7Bt_h%7D">

7. The change in number of recovered people for every age group
<!-- $$$\frac{dD_a(t)}{dt} = f_a \frac{C_a(t)}{t_c}$$$ -->
<img src="https://latex.codecogs.com/gif.latex?%5Cfrac%7BdD_a%28t%29%7D%7Bdt%7D%20%3D%20f_a%20%5Cfrac%7BC_a%28t%29%7D%7Bt_c%7D">
</p>

with the entire population
<p align="center">
<!--  $$$N_\text{total} = \sum_a \left(S_a(t) + E_a(t) + I_a(t) + H_a(t) + C_a(t) + R_a(t) + D_a(t) \right) = const$$$  -->
<img src="https://latex.codecogs.com/gif.latex?N_%5Ctext%7Btotal%7D%20%3D%20%5Csum_a%20%5Cleft%28S_a%28t%29%20&plus;%20E_a%28t%29%20&plus;%20I_a%28t%29%20&plus;%20H_a%28t%29%20&plus;%20C_a%28t%29%20&plus;%20R_a%28t%29%20&plus;%20D_a%28t%29%20%5Cright%29%20%3D%20const">
</p>

where

<p align="center">
<!-- $$$a$$$  -->
<img src="https://latex.codecogs.com/gif.latex?a">
</p>

is the index for a specific age group.

One kinetic parameter is the time dependent infection rate (transmission rate)
<p align="center">
<!-- $$$\beta_a(t) = R_0 I_a M(t)(1+\varepsilon \cos(2\pi(t-t_\text{max})))/t_i$$$ -->
<img src="https://latex.codecogs.com/gif.latex?%24%24%24%5Cbeta_a%28t%29%20%3D%20R_0%20I_a%20M%28t%29%281&plus;%5Cvarepsilon%20%5Ccos%282%5Cpi%28t-t_%5Ctext%7Bmax%7D%29%29%29/t_i%24%24%24">
</p>

with the basic reproduction number ("expected number of secondary cases produced by a single (typical) infection in a completely susceptible population", James H. Jones 2007)

<p align="center">
<!-- $$$R_0$$$ -->
<img src="https://latex.codecogs.com/gif.latex?R_0">
</p>

and the isolation of a particular age group

<p align="center">
<!-- $$$I_a$$$ -->
<img src="https://latex.codecogs.com/gif.latex?I_a">
</p>

and the mitigation measures

<p align="center">
<!-- $$$M(t)$$$ -->
<img src="https://latex.codecogs.com/gif.latex?M(t)">
</p>

as well as the amplitude of seasonal variation in transmissibility

<p align="center">
<!-- $$$\varepsilon$$$ -->
<img src="https://latex.codecogs.com/gif.latex?%5Cvarepsilon">
</p>

and the time of the year of peak transmission

<p align="center">
<!-- $$$t_\text{max}$$$ -->
<img src="https://latex.codecogs.com/gif.latex?t_%5Ctext%7Bmax%7D.">
</p>


The remaining parameters are time scales of transition to a different subpopulation (e.g., infected, hospitalized, dead), where

<p align="center">
<!-- $$$t_l$$$ -->
<img src="https://latex.codecogs.com/gif.latex?t_l">
</p>

is the mean time for a transition between exposed and infected state,

<p align="center">
<!-- $$$t_i$$$ -->
<img src="https://latex.codecogs.com/gif.latex?t_i">
</p>

is the mean time for a transition between infected and recovered / hospitalized state (in combination with m_a / (1-m_a), respectively),

<p align="center">
<!-- $$$t_h$$$ -->
<img src="https://latex.codecogs.com/gif.latex?t_h">
</p>

is the mean time for a transition between hopitalized and recovered / critical state (in combination with (1-c_a) / c_a, respectively),

<p align="center">
<!--  $$$t_c$$$ -->
<img src="https://latex.codecogs.com/gif.latex?t_c">
</p>

is the mean time for a transition between critical and hospitalized / dead state (in combination with (1-f_a) / f_a, respectively). The parameters

<p align="center">
<!-- $$$m_a, \quad c_a, \quad f_a$$$ -->
<img src="https://latex.codecogs.com/gif.latex?m_a%2C%20%5Cquad%20c_a%2C%20%5Cquad%20f_a">
</p>

are age-specific paramters that represent fraction of mild cases when infected, fraction of severe cases when hospitalized, and fraction of fatal cases when critical, respectively.

## Rule-based CoVid-19 model by Neherl Lab

### Conversion of ODEs to rules
In order to have all rules (the number of rules equals the number of kinetic parameters in the ODEs), we must write all rules of every equation and then combine those that share the same kinetic parameter.

(Since some kinetic parameters are also time dependent, we are including them as variables that might change from time to time. -> This is not possible, because when counted the values are always converted to intergers, so we wouldn't have real numbers as parameter values. Instead, we need to include a function to change the parameter values in the reaction rates.)

1. The first equation as a rule (in ML-Rules syntax):
``` S('a'):s + I(x):i + Time():t -> I(x) + Time() @ (beta_a / nTotal) * #s * #i;```

2. The second equation as rules (in ML-Rules syntax):
``` S('a'):s + I(x):i + Time():t -> S('a') + I(x) + E('a') + Time() @ (beta_a / nTotal) * #s * #i;```
``` E('a'):e ->  @ (1/t_l) * #e;```

3. The third equation as rules (in ML-Rules syntax):
``` E('a'):e -> E('a') + I('a') @ (1/t_l) * #e;```
``` I('a'):i -> @ (1/t_i) * #i;```

4. The forth  equation as rules (in ML-Rules syntax):
TODO: Kann 1-m und 1-f jemals < 0 sein? wenn ja, benötigen wir noch die Gegenregel.
Frage: m und f und k sind ja Werte kleiner 1, macht es sinn, diese als Spezies aufzunehmen?
``` I('a'):i -> I('a') + H('a') @ (1/t_i) * (1-m_a) * #i;```
``` C('a'):c -> C('a') + H('a') @ (1/t_c) * (1-f_a) * #c;```
``` H('a'):h -> @ (1/t_h) * #h;```

5. The fifth equation as rules (in ML-Rules syntax):
``` H('a'):h -> H('a') + C('a') @ (1/t_h) * c_a * #h;```
``` C('a'):c -> @ (1/t_c) * #c;```

6. The sixth equation as rules (in ML-Rules syntax):
``` I('a'):i -> I('a') + R('a') @ (1/t_i) * m_a * #i;```
``` H('a'):h -> H('a') + R('a') @ (1/t_h) * (1-c_a) * #h;```

7. The seventh equation as a rule (in ML-Rules syntax):
``` C('a'):c -> C('a') + D('a') @ (1/t_c) * f_a * #c;```



We now combine all rules with ```(beta / nTotal) * #s * #i``` as reaction rate and then all rules with ```gamma * #i``` as reaction rate.

1. First rule (infection of susceptible person but without symptoms at first):
``` S('a'):s + I(x):i + Time():t -> E('a') + I(x) + Time() @ (beta_a / nTotal) * #s * #i;```

2. Second rule (infected person shows symptons and is infectious):
``` E('a'):e ->  I('a') @ (1/t_l) * #e;```

3. Third rule (hospitalization of infected person)
``` I('a'):i -> H('a') @ (1/t_i) * (1-m_a) * #i;```

4. Forth rule (recovery of infected person)
``` I('a'):i -> R('a') @ (1/t_i) * m_a * #i;```

5. Fifth rule (recovery of hospitalized person)
``` H('a'):h -> R('a') @ (1/t_h) * (1-c_a) * #h;```

6. Sixth rule (hospitalized person moves into critical state)
``` H('a'):h -> C('a') @ (1/t_h) * c_a * #h;```

7. Seventh rule (hospitalized person moves out of critical state)
``` C('a'):c -> H('a') @ (1/t_c) * (1-f_a) * #c;```

8. Eightth rule (hospitalized person dies)
``` C('a'):c -> D('a') @ (1/t_c) * f_a * #c;```


### ML-Rules model version of general SIR model
Together with the two rules, we can now build a ML-Rules version of the general SIR model. It can be found in [CoViD19_NeherLab.mlrj](./CoViD19_NeherLab.mlrj).

A sample simulation can be seen in the following screenshot of the plot by the ML-Rules editor.
![SIR Model Simulation](./CoViD19_NeherLabSimulation.png)

