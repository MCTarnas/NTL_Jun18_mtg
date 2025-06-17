# Committee meeting: June 18

Check in on manuscript: **Nighttime lights as a proxy for conflict intensity, population displacement, and infrastructure recovery in Yemen and Ukraine**

As a reminder, we are using Black Marble (NASA) nighttime lights (NTL) to measure conflict dynamics, population size, and infrastructure recovery in Yemen and Ukraine. The analysis has four parts: 
- Association between NTL (outcome) and aerial attacks (GAMs) 
- Detection of attack onset in the mean NTL time series using significant breakpoints
- Association between estimated population size (outcome) and NTL (GAMs)
- Application of NTL to existing model on the association between cholera and conflict in Yemen (from [this paper](https://www.thelancet.com/journals/langlo/article/PIIS2214-109X(23)00272-3/fulltext))

Daniel and have been noodling on two questions:
- Do we need to / should we quantify how well our breakpoint detection techniques are working? If so, how?
- Do we need to worry about endogeneity in our population model?

**We'd like to get this resubmitted to *Scientific Reports* by end of June**

----
💡 Markdowns with background for each question:
- BFAST quantification: [`bfast`](bfast.md)
- Population and endogeneity: [`population`](population.md)
