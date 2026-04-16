# The Effect of Political Partisanship on Electric Vehicle Adoption in the US

**ECO475 Undergraduate Thesis** — University of Toronto, April 2023
**Supervisor:** Professor Ismael Mourifié
**Full paper:** [Writeups/ECO475_Paper-1.pdf](Writeups/ECO475_Paper-1.pdf)

## Summary

This thesis estimates the relationship between county-level political partisanship and electric vehicle (EV) adoption in the United States, using a monthly county-level panel spanning January 2017 to December 2022. Using panel OLS with state and year fixed effects, I find that a 1 percentage point increase in Republican vote share in the 2016 federal election is associated with a 0.55 percentage point decrease in the EV share of county vehicle populations, significant at the 1% level and robust to the inclusion of demographic, infrastructure, fuel price, and state-level political controls.

The paper is framed as an estimation of associations rather than causal effects: county vote share is treated as a proxy for underlying political, social, and economic beliefs that plausibly drive individual adoption decisions, and clean identification would require variation that is not available in this setting.

## Research Question

Transportation accounts for 27% of US greenhouse gas emissions, of which 57% comes from light-duty vehicles. EV adoption stands to reduce both emissions and the local air pollutants (particulate matter, nitrogen oxides, carbon monoxide) linked to adverse health outcomes. While the existing literature — largely from transportation, energy, and sustainability studies — identifies political ideology as correlated with green technology adoption, no prior economics paper that I could locate had explicitly estimated the effect size of federal-election partisanship on EV adoption at the population level. This thesis fills that gap.

## Data

The final dataset consists of 9,121 monthly county-level observations across six years, combining seven public sources:

| Variable | Source |
|---|---|
| Vehicle populations (passenger/truck × BEV/HEV/ICE) | Washington State Department of Licensing |
| County demographics (population, education, income, poverty) | USDA Economic Research Service |
| Monthly gasoline prices | US Energy Information Administration |
| County charging/fueling station counts | DOE Alternative Fuels Data Center |
| 2016 & 2020 federal election returns | MIT Election Data Lab |
| State governor partisanship | National Governors Association |
| State legislature partisanship | Ballotpedia |

Observations with fewer than 50 total vehicles per county-month are excluded to address a reporting artifact visible in Figures 8–9 of the paper. Coverage is biased toward more populated counties (150–200 counties per month, roughly 5–6% of US counties but 27–30% of US population) — the paper discusses the implications for external validity.

## Methodology

The specification is:

```
EV_Proportion[t,c] = α + β₁·FedPol2016[c] + β₂·ΔFedPol2020[c]
                   + θ·StatePol[t,s] + δ·Demog[c]
                   + κ·Infra[t,c] + ω·FuelPrice[t]
                   + γ[t] + τ[s] + ε
```

where β₁ and β₂ capture the effects of 2016 Republican vote share and the 2016→2020 change in vote share, respectively. State and year fixed effects (τ[s], γ[t]) absorb time-invariant state characteristics and national time trends, including unobserved factors identified in the literature (vehicle prices, ranges, charging times, state-level subsidy programs).

## Results

| Specification | β₁ (2016 vote share) | β₂ (Δ 2020) |
|---|---|---|
| Base (FE only) | −1.30*** | −0.90*** |
| + Demographic controls | −0.54*** | −0.03 |
| + All controls | **−0.55\*\*\* (SE 0.09)** | −0.12 |

*Full regression table in Section 5 of the paper.*

Key findings:

- The 2016 partisanship effect is statistically and economically significant and stable across specifications.
- The *change* in partisanship from 2016 to 2020 is not significant once controls are added — the relationship operates through persistent political composition rather than short-run shifts.
- Median household income, educational attainment, and charging infrastructure are positively associated with EV adoption; poverty rate is negatively associated. State-legislature controls show mixed and partially counterintuitive signs, discussed in the paper.

## Limitations and Framing

The paper explicitly does not claim causal identification. Vote share is a proxy for underlying ideology and correlated beliefs; there is no instrument or natural experiment here that would isolate the effect of partisanship itself from the bundle of values and economic conditions it represents. The estimates should be read as conditional associations within a reasonably rich set of controls, not as a causal effect of voting Republican on deciding to buy an EV.

Additional limitations: the vehicle-population panel covers only counties that report to the Washington DOL dataset (biased toward populated counties), and the 50-vehicle threshold for inclusion introduces a documented sample restriction.

## Repository Structure

```
.
├── README.md
├── Writeups/
│   └── ECO475_Paper-1.pdf       # Full thesis
├── Data/                         # Raw and cleaned data
└── Notebooks/                    # Data collection, cleaning, analysis
```

## Tools

Python (pandas, numpy, statsmodels, matplotlib) for data collection, cleaning, visualization, and panel regression.

