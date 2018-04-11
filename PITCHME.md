##  SIMEX Measurement Error Correction in Student Growth Percentiles

---

### Presentation Roadmap

- Review the measurement error problem |
- Introduce the SIMEX Method of correcting for ME bias |
- SIMEX implementation in Student Growth Percentiles (SGP) |
- Ranking SIMEX SGPs in the SGP package for R |
- Provide evidence of effectiveness from an example state's analyses |
- Relationship between different SGP estimates with prior student achievement |

---

###  Additional Resources
- [Full SIMEX Report](https://github.com/adamvi/NCME_Ranked_SIMEX_SGP/blob/master/PDF/Ranked_SIMEX_SGP.pdf),
- *Code Examples*
  + [SIMEX with Toy Data Set](https://gist.github.com/adamvi/5169922)
  + [SIMEX with Simulated Data Set](https://gist.github.com/adamvi/5169922)
  + [SIMEX Monte Carlo](https://gist.github.com/adamvi/5169922)
- [General SGP Resources](https://github.com/CenterForAssessment/SGP_Resources)

---

###  Measurement error (ME)

-  Inherent component of all standardized tests |
-  Additional uncertainty in growth estimates (e.g. SGPs) |
-  Produces biased estimates |
  + disadvantages students with lower prior achievement and vice versa |
  + transferred to aggregate measures of educator effectiveness when students with low/high prior achievement are concentrated in a classroom or school |
---

###  SIMEX Method of ME Correction

-  Simulation/Extrapolation (SIMEX) techniques eliminate bias SGPs (Shang, VanIwaarden and Betebenner, 2015) |
-  This method is available in the SGP package for R |
-  Several states use the SIMEX measures in accountability and evaluation policies. |
---

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

---
###  SIMEX Method and SGPs

- Straightforward when interested in a model parameter (e.g. regression model coefficient) |
- Not what we want to correct for in the SGP model |
- Estimating ${\widehat{SGP}_ X}$, and these quantities are derived from the fitted values of the model |
  + predicted test scores at 100 percentiles |
- Create a SIMEX corrected lookup-table of predicted scores to derive SGPs. |

---
###  SIMEX Method and SGPs

- Unfortunately ... |
  - SIMEX corrected SGPs also have technical limitations. |

- Student level SIMEX SGPs have larger errors than the uncorrected ones |
  + SIMEX preferred for aggregated SGP results (mean or median SGPs) |
  + Uncorrected preferred for student level reporting |

---
###  Ranked SIMEX SGPs

- Castellano and McCaffrey (2017) proposed ranking SIMEX SGP estimates to address: |
  - excess variance from the SIMEX estimation process |
  - uniform distribution of SGPs |
- Best of both worlds for aggregated and individual SGPs |
- Ranked SIMEX values added to SGP computation in 2017 (version 1.7-0.2) |

---
###  Ranked SIMEX SGPs

Unlike SGP/SIMEX calculation in SGP package Castellano and McCaffrey:
- Used closed-form equations to estimate SIMEX SGPs |
  + No simulation/extrapolation, quantile regression, etc. |
  + Make assumptions about data and ME structures that we don't |
- Produces continuous SIMEX SGP values |
  + Re-ranking integer values from the SGP calculations ... not impressive |

---
###  Ranked SIMEX SGPs

*Adaptations to the SGP/SIMEX framework:*          
- Need continuous values of SIMEX SGPs |
  - Add 10X more percentile values |
    + *At least* 10X longer - not tenable |
  - Calculate arithmetic midpoints (8) between the SIMEX estimates of the predicted scores |
    + Much faster and similar results

---
###  Ranked SIMEX SGPs - Results

Marginal distributions - 8<sup>th</sup> Grade Math SGPs (single prior score)

![Image-Absolute](./img/Math_G8_Marginal_Distributions-1_Prior.png)

---
###  Ranked SIMEX SGPs - Results

Goodness of Fit Plots - conditional distributions

(Scroll Down)

+++

@title[Uncorrected]

####  Uncorrected

<img src="./img/Goodness_of_Fit/MATHEMATICS.2017/gofSGP_Grade_8.png" alt="Uncorrected" width="500" height="500">

+++
@title[SIMEX Corrected]

####  SIMEX

<img src="./img/Goodness_of_Fit/MATHEMATICS.2017.SIMEX/gofSGP_Grade_8.png" alt="SIMEX" width="500" height="500">

+++
@title[Ranked SIMEX]

####  Ranked SIMEX

<img src="./img/Goodness_of_Fit/MATHEMATICS.2017.RANKED_SIMEX/gofSGP_Grade_8.png" alt="Ranked SIMEX" width="500" height="500">

---
###  Correlation Tables

<!-- HTML_Start -->
<table class="gmisc_table breakboth" style="border-collapse: collapse; margin-top: 1em; margin-bottom: 1em;">
<thead>
<tr>
<td colspan="6" style="text-align: left;">
<strong>Table 1:</strong> Student Level Correlations between Prior Standardized Scale Score and 1) Current Scale Score, 2) SGP, 3) SIMEX SGP and 4) Ranked SIMEX SGP.
</td>
</tr>
<tr>
<th style="border-bottom: 1px solid grey; border-top: 2px solid grey; text-align: center;">
Content Area
</th>
<th style="border-bottom: 1px solid grey; border-top: 2px solid grey; text-align: center;">
Grade
</th>
<th style="border-bottom: 1px solid grey; border-top: 2px solid grey; text-align: center;">
<span class="math">$\
r_ { Test Scores}$</span>
</th>
<th style="border-bottom: 1px solid grey; border-top: 2px solid grey; text-align: center;">
<span class="math">$\
r_ { SGP}$</span>
</th>
<th style="border-bottom: 1px solid grey; border-top: 2px solid grey; text-align: center;">
<span SIMEX SGP </span>
</th>
<th style="border-bottom: 1px solid grey; border-top: 2px solid grey; text-align: center;">
Ranked SIMEX
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align: right;">
Language Arts
</td>
<td style="text-align: right;">
4
</td>
<td style="text-align: right;">
0.830
</td>
<td style="text-align: right;">
0.000
</td>
<td style="text-align: right;">
-0.121
</td>
<td style="text-align: right;">
-0.122
</td>
</tr>
<tr>
<td style="text-align: right;">
</td>
<td style="text-align: right;">
5
</td>
<td style="text-align: right;">
0.843
</td>
<td style="text-align: right;">
0.000
</td>
<td style="text-align: right;">
-0.090
</td>
<td style="text-align: right;">
-0.090
</td>
</tr>
<tr>
<td style="text-align: right;">
</td>
<td style="text-align: right;">
6
</td>
<td style="text-align: right;">
0.839
</td>
<td style="text-align: right;">
0.000
</td>
<td style="text-align: right;">
-0.086
</td>
<td style="text-align: right;">
-0.086
</td>
</tr>
<tr>
<td style="text-align: right;">
</td>
<td style="text-align: right;">
7
</td>
<td style="text-align: right;">
0.839
</td>
<td style="text-align: right;">
-0.001
</td>
<td style="text-align: right;">
-0.086
</td>
<td style="text-align: right;">
-0.086
</td>
</tr>
<tr>
<td style="text-align: right;">
</td>
<td style="text-align: right;">
8
</td>
<td style="text-align: right;">
0.846
</td>
<td style="text-align: right;">
0.001
</td>
<td style="text-align: right;">
-0.087
</td>
<td style="text-align: right;">
-0.088
</td>
</tr>
<tr>
<td style="text-align: right;">
Mathematics
</td>
<td style="text-align: right;">
4
</td>
<td style="text-align: right;">
0.843
</td>
<td style="text-align: right;">
-0.001
</td>
<td style="text-align: right;">
-0.096
</td>
<td style="text-align: right;">
-0.096
</td>
</tr>
<tr>
<td style="text-align: right;">
</td>
<td style="text-align: right;">
5
</td>
<td style="text-align: right;">
0.856
</td>
<td style="text-align: right;">
-0.001
</td>
<td style="text-align: right;">
-0.071
</td>
<td style="text-align: right;">
-0.071
</td>
</tr>
<tr>
<td style="text-align: right;">
</td>
<td style="text-align: right;">
6
</td>
<td style="text-align: right;">
0.842
</td>
<td style="text-align: right;">
-0.001
</td>
<td style="text-align: right;">
-0.068
</td>
<td style="text-align: right;">
-0.069
</td>
</tr>
<tr>
<td style="text-align: right;">
</td>
<td style="text-align: right;">
7
</td>
<td style="text-align: right;">
0.866
</td>
<td style="text-align: right;">
0.000
</td>
<td style="text-align: right;">
-0.073
</td>
<td style="text-align: right;">
-0.073
</td>
</tr>
<tr>
<td style="border-bottom: 2px solid grey; text-align: right;">
</td>
<td style="border-bottom: 2px solid grey; text-align: right;">
8
</td>
<td style="border-bottom: 2px solid grey; text-align: right;">
0.819
</td>
<td style="border-bottom: 2px solid grey; text-align: right;">
0.003
</td>
<td style="border-bottom: 2px solid grey; text-align: right;">
-0.064
</td>
<td style="border-bottom: 2px solid grey; text-align: right;">
-0.064
</td>
</tr>
</tbody>
</table>

---
## Questions?
