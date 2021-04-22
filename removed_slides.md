---

### SIMEX in the SGP package

The `SGP` package allows the user to specify the parameters of the SIMEX process.

- **`state`** two letter state abbreviation under which the test specific CSEMs are located in `SGPstateData` |
  + Assessment specific meta-data that identifies variables to use in the SIMEX process.  |
- Alternatively, one can use the following elements to identify the necessary components: |
	+ `variable` - the variable in the data to be perturbed (prior test scores). |
	+ `csem.data.vnames` - the CSEM variable

---
### SIMEX in the SGP package



###  SIMEX - the name says it all...

-  SIMulation/EXtrapolation |
-  Estimate the impact of ME through a series of SIMULATION experiments |
  + Increasing amounts of simulated ME are added to observed values to create error-prone "pseudo" data sets
    - A set of increasing small numbers.  Typically ${\lambda}$ = 0.5, 1, 1.5, 2
---
###  SIMEX - the name says it all...

- Parameter estimates of interest are calculated using perturbed data|
- Simulations are repeated a large number of times at each level ${\lambda}$. |

---
###  SIMEX - the name says it all...

-  EXTRAPOLATE |
  + Average the parameter estimates at each level of ${\lambda}$. |
  + Averaged "pseudo" parameter estimates and the "naive" estimates are regressed on ${\lambda}$ |
  + Using this model, EXTRAPOLATE the predicted value at ${\lambda} = -1$ |
    - Voila! The SIMEX estimate of the error-free parameter. |

---
###  SIMEX - what is it good for?

- Does not make strong assumptions about variable distributions |
- Easier to implement for ME models that are less understood (e.g. nonparametric quantile regression) |
- Assumes the SEM is known or can be reasonably well estimated. |
