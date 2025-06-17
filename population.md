# ❓ Do we need to worry about endogeneity in our population model?
We learned (from Andy Tatem, Director of WorldPop) that WorldPop uses NTL to inform their population estimates. He said that newer estimates don't rely on NTL as much, but it's still baked in. This made us wonder whether we need to be concerned with endogeneity in our population models:

```r
yem_pop.gam <- gam(pop ~ s(mos, bs="cc",k=-1) + s(built_perc_log,k=-1) + 
                     s(ntl_mean_const_log, k=-1) + s(recovery_ratio_log,k=-1) + 
                     attacksCAT + s(lon,lat,bs="sos",k=15), family = gaussian, 
                   select=T, gamma=1.5, data=ntl_data_yem, method="REML")

ukr_pop.gam <- gam(pop ~ s(mos, bs="cc",k=-1) + s(ntl_mean_log,k=-1) + 
                     s(recovery_ratio_log,k=-1) + attacksCAT + 
                     s(lon,lat,bs="sos",k=24), family = gaussian, select=T, 
                   gamma=1.5, data=ntl_data_ukr, method="REML")
```

## 📄 Current methods and results (from paper)
***Methods***: We also extracted population size estimates and data on the built environment for each administrative unit. WorldPop provides annual unconstrained UN-adjusted population estimates at 100m through 2020 [37). Years 2021 and 2022 were linearly extrapolated. 

***Results***: We ran similar models to measure the association between mean NTL and population size (as the response variable) in each administrative unit; these also included light recovery. NTL was positively associated with governorate and oblast population size (Figure S6). In both countries, administrative units with more attacks had higher population levels, indicating that highly populated areas were more likely to be attacked (Table S1). Conversely, recovery had a near-linear negative association with population size in both countries (Figure S6). Together, this reflects that areas with higher population were unable to recover as strongly because they experienced more attacks.

## 🤓 What we've done since
We ran a sensitivity analysis using Gridded Population of the World (GPW), which provides non-modeled population estimates (available adjusted and unadjusted for UN estimates) that are based on historical census data and **do not use NTL data**; estimates are available every five years between 2000 and 2015. To create annual measurements, I used two techniques: 1) applying the growth rate between 2015 – 2020 to all years between 2015 – 2022, and 2) applying the mean growth rate of the entire 2000 – 2015 period to all years between 2015 – 2022. This resulted in four population estimates for sensitivity analyses. We did the sensitivity analyses for the population models (above) and the GAM for NTL ~ aerial attacks in Yemen, as it also included population as a covariate (the model for Ukraine does not include population because it had high concurvity with built environment). It's a lot of tables, so I've just included the ones for the population model. Importantly, **nothing meaningful changes in any of our results**. This includes the kind of confusing result that light recovery and population size have an inverse association (i.e., places with more population have weaker recoveries). 

<img width="1035" alt="Screenshot 2025-06-17 at 1 24 54 PM" src="https://github.com/user-attachments/assets/98903f62-6527-411e-98e8-989e2680e92d" />

**Table 1**: Linear results for the population model sensitivity analyses.

<img width="1248" alt="Screenshot 2025-06-17 at 1 26 13 PM" src="https://github.com/user-attachments/assets/164b2d25-20d4-45af-bdb5-735e5feea8f4" />

**Figure 1**: Spline results for the population model sensitivity analyses.


## ❓ Our question
**Do we have any lingering concerns over endogeneity in our model despite having run this sensitivity analysis?** Moreover, **do we retain the population models as part of the main text, or move them to supplemental material**? We had discussed the second question before we ran the sensitivity analysis. We also need to consider whether **it makes more sense to have the final model use WorldPop data or GPW data.** There are other available population estimates, but GPW was the only one I could find that was not at all informed by NTL.

| WorldPop | | GPW | |
|---|---|---|---|
| **Pro** | **Con** | **Pro** | **Con** |
| Annual estimates until 2020 | Informed by NTL | Not informed by NTL | Only available every 5 years, which led to *a lot* of interpolation |






