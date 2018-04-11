##  The SIMEX Method for Measurement Error Correction in Student Growth Percentiles

---

## Presentation Roadmap

- Review the measurement error problem |
- Introduce the SIMEX Method of correcting for ME bias |
- SIMEX implementation in Student Growth Percentiles (SGP) |
- Ranking SIMEX SGPs in the SGP package for R |
- Provide evidence of effectiveness from an example state's analyses |
- Relationship between different SGP estimates with prior student achievement |

---

##  Additional Resources
- [Full SIMEX Report](https://github.com/adamvi/NCME_Ranked_SIMEX_SGP/blob/master/PDF/Ranked_SIMEX_SGP.pdf),
- *Code Examples*
  + [SIMEX with Toy Data Set](https://gist.github.com/adamvi/5169922)
  + [SIMEX with Simulated Data Set](https://gist.github.com/adamvi/5169922)
  + [SIMEX Monte Carlo](https://gist.github.com/adamvi/5169922)
- [General SGP Resources](https://github.com/CenterForAssessment/SGP_Resources)

---

##  Measurement error (ME)

-  Inherent component of all standardized tests |
-  Additional uncertainty in growth estimates (e.g. SGPs) |
-  Produces biased estimates |
  + disadvantages students with lower prior achievement and vice versa |
  + transferred to aggregate measures of educator effectiveness when students with low/high prior achievement are concentrated in a classroom or school |
---

##  SIMEX Method of ME Correction

-  Simulation/Extrapolation (SIMEX) techniques eliminate bias SGPs (Shang, VanIwaarden and Betebenner, 2015) |
-  This method is available in the [SGP package](https://github.com/CenterForAssessment/SGP) for [R](http://www.r-project.org/). |
-  Several states use the SIMEX measures in accountability and evaluation policies. |
---

###  SIMEX Method - the name says it all...

-  Simulation/Extrapolation |
-  Estimate the impact of ME through a series of SIMULATION experiments |
  + Increasing amounts of simulated ME are added to observed values to create error-prone "pseudo" data sets
    - A set of increasing small numbers.  Typically ${\lambda}$ = 0.5, 1, 1.5, 2
---
###  SIMEX Method - the name says it all...
- Parameter estimates of interest are calculated using perturbed data|
- Simulations are repeated a large number of times at each level ${\lambda}$. |

---
###  SIMEX Method - the name says it all...
-  EXTRAPOLATE |
  + Average the parameter estimates at each level of ME. |
  + Averaged "pseudo" parameter estimates and the "naive" estimates are regressed on ${\lambda}$ |
  + Using this model, EXTRAPOLATE the predicted value at ${\lambda} = -1$ |
    - Voila! The SIMEX estimate of the error-free parameter.

---
###  SIMEX Method - what is it good for?

- Does not make strong assumptions about variable distributions |
- Easier to implement for ME models that are less understood (e.g. nonparametric quantile regression) |
- Assumes the SEM is known or can be reasonably well estimated. |

---
##  SIMEX Method and SGPs

- Straightforward when interested in a model parameter (e.g. coefficient in a linear regression model) |
- Not what we want to correct for in the SGP model |
- Estimating ${\widehat{SGP}_ X}$, and these quantities are derived from the fitted values of the model |
  + i.e. predicted test scores at 100 percentile values |
- Create a SIMEX corrected lookup-table of predicted scores to derive SGPs.

---
##  SIMEX Method and SGPs

Unfortunately ... |
SIMEX corrected SGPs also have technical limitations. |

- Student level SIMEX SGPs have larger errors than the uncorrected ones |
  + SIMEX preferred for aggregated SGP results (mean or median SGPs) |
  + Uncorrected preferred for student level reporting |

---
##  SIMEX Method and SGPs


---
## Questions?
