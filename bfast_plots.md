# Do we need to / should we quantify how well our breakpoint detection techniques are working (Part 2)? If so, how?
We use the Breaks for Additive Season and Trend (BFAST) change detection approach to detect significant negative breakpoints in the mean NTL time series for each administrative unit while accounting for seasonality (NTL in both countries exhibit seasonality). Daniel got some questions about the technique when he was presenting at Oxford, which made us think that we should perhaps run a sensitivity analysis with another change detection approach. **We chose `BFAST` originally because it accounts for seasonality**. 

## Current methods and results

***Methods***: We used the Breaks for Additive Season and Trend (BFAST) change detection approach to detect significant negative breakpoints in the mean NTL time series for each administrative unit while accounting for seasonality [23]. BFAST decomposes time series into seasonal, trend, and remainder components while estimating the number, timing, magnitude, and direction of significant changes within them. Detection was considered successful if the onset of aerial attacks in the administrative unit fell within the 95% confidence window for a negative breakpoint (i.e., the break indicated a significant negative shift in the time series). This was done using the bfast package in R [39] (we also tested this using changepoint, see Tables S5 and S6).

***Results***: We used the Breaks for Additive Season and Trend (BFAST) change detection approach to detect significant negative breakpoints in the mean NTL of each administrative unit [23]. This approach evaluated whether the NTL time series captured attack onset at the country and administrative unit levels (i.e., a successful detection). The 95% confidence intervals of BFAST-detected negative breakpoints aligned with attack onset in 85.7% (n=18) of governorates and 51.9% (n=14) of oblasts (Figure 2). The three governorates where these did not align were those with the fewest attacks. In Kherson, Mykolayiv, Odesa, and Vinnytsya oblasts, significant breakpoints were not detected at attack onset because their NTL levels had already been steadily declining over the study period. Conversely, Crimea, Luhansk, Sevastopol, Rivne, and Volyn experienced steady increasing trends that were not notably affected by the full-scale invasion. Kirovograd had no noted change in mean NTL across the entire study period.

## What we've done since
We ran a sensitivity analysis with the `changepoint` package, which can detect changes in time series’ mean and variance (using the `cpt.meanvar` function). There were minor differences between the two methods, they aligned in the majority of administrative units.
	
![image](https://github.com/user-attachments/assets/679dbfc7-36f8-4fcd-84c1-b8d86c4a77fe)

**Table 1**: Comparison of results using two breakpoint estimating tools for Yemen. Changepoint does not give confidence intervals for the detected breakpoints, and thus we considered detection successful if the month detected by changepoint fell within the confidence interval of the BFAST detection. Green cells indicate a successful detection of attack onset and red cells indicate an unsuccessful detection. The “Aligned” column indicates whether the breakpoints detected by BFAST and changepoint aligned (i.e., were within the same confidence interval). The two methods aligned with each other in 86% (n = 19) of locations.


![image](https://github.com/user-attachments/assets/1ece5eb4-b92e-4fff-8908-0c1907f19b22)

**Table 2**: Comparison of results using two breakpoint estimating tools for Ukraine. Changepoint does not give confidence intervals for the detected breakpoints, and thus we considered detection successful if the month detected by changepoint fell within the confidence interval of the BFAST detection or ± 2 months of attack onset in areas where BFAST did not detect a breakpoint. Green cells indicate a successful detection of attack onset and red cells indicate an unsuccessful detection. The “Aligned” column indicates whether the breakpoints detected by BFAST and changepoint aligned (i.e., were within the same confidence interval). The two methods aligned with each other in 64% (n = 18) locations.

## Our question
**Do we need to quantify how well the `BFAST` technique (and/or `changepoint`, for that matter) works?** Daniel and I considered calculating something like a **sensitivity** and **specificity**, but we aren't able to do so because there are no instances in which attack onset doesn't happen (i.e., there are aerial attacks in all administrative units, so we can't calculate a True Negative or a False Positive). Here's where we got with that idea:

| | Yemen | | Ukraine | |
|---|---|---|---|---|
| | BFAST | Changepoint | BFAST | Changepoint |
| Successful detection (TP)
| Unsuccessful detection | 
| No detection (FN) |
