# Weather and the Way NYC Rides: Project Proposal

## The concept
**Looking at how weather changes the way people commute in New York, with a focus on citi bikes, it predicts people's choice of using citi bike dependent on the next day's weather prediction**

This project joins Citi Bike trip records with daily Central Park weather to predict people's bike usage, then designs a Citi Bike app feature from the results.

Factors in consideration:
- How much rain, heat, cold and wind reduce daily rides
- Whether members and casual riders, and e-bike and classic riders, react differently
- Which stations lose the most riders in bad weather
- How well a model predicts daily rides compared with a simple guess

## Relevance

Lyft reported about 45 million Citi Bike trips in 2025, and e-bike ridership doubled from 2023 to 2025 ([amNY](https://www.amny.com/nyc-transit/citi-bike-in-nyc-boroughs-ridership)). Meanwhile, about 500 New Yorkers die early each summer because of hot weather ([NYC Health, 2026](https://a816-dohbesp.nyc.gov/IndicatorPublic/data-features/heat-report/)). Knowing how weather shapes riding helps Citi Bike put bikes where they're needed and helps riders stay safe on hot days.

## Data

Two public datasets for 2024–2025, joined by date.

[Citi Bike trip histories](https://citibikenyc.com/system-data), one ride, about 45 million rides a year 
[NOAA daily weather (GHCN-Daily)](https://www.ncei.noaa.gov/products/land-based-station/global-historical-climatology-network-daily), Central Park station USW00094728, one day, about 730 rows 

**Key decision variables:** the full trip history is about 320 million rows ([Raschke, 2026](https://kurtraschke.com/2026/07/citibike-extractor)), too big for Colab, so I'll load one month at a time, keep only daily ride counts, and discard the raw rows.

## Method

1. **Collect** the 24 monthly Citi Bike files and the matching daily weather.
2. **Shrink** each month to daily ride counts (total, member/casual, e-bike/classic, per station).
3. **Join** counts and weather into one table, one row per day, and add weekday, weekend, month and holiday.
4. **Explore** rides against temperature, rain and wind, and compare rider and bike types.
5. **Model** daily rides: train on 2024, test on 2025, and compare with two baselines (the average day, and the average for that weekday and month).
6. **Review** the days the model missed most, then turn the findings into the app concept.

## Deliverables

**Final**:

- The full 2024–2025 analysis notebook- with organised data
- The prediction model, tested on 2025 and compared with both baselines
- A station map of where riding drops most in heat and rain
- A failure analysis of the days the model got most wrong
- **A product concept for the Citi Bike app**: 3–4 screens that use the model, for example a heat-aware ride suggestion and an operations view showing where e-bikes should go before a hot day. Design of it will be on figma and I could prototype it on claude to make it a working prototype. 

## How I'll use an LLM and show understanding

I'll use an LLM for code, with permission, and show my understanding through:

- **A criteria notebook** written before any code: question, data rules, features and success measures, quoted in every LLM request.
- **A decision log** of what the LLM suggested, what I kept or rejected, and why.
- **Hand checks**, such as matching a month's total to Citi Bike's published figure.

## Sources

- [Citi Bike System Data](https://citibikenyc.com/system-data): official trip history downloads and cleaning notes
- [NOAA Global Historical Climatology Network Daily](https://www.ncei.noaa.gov/products/land-based-station/global-historical-climatology-network-daily): daily weather data, downloadable through NOAA Climate Data Online
- [Transforming Citi Bike trip history data into an easy-to-use dataset for analysis](https://kurtraschke.com/2026/07/citibike-extractor) (Kurt Raschke, July 2026): total size and data quirks
- [Citi Bike surge: ridership increases](https://www.amny.com/nyc-transit/citi-bike-in-nyc-boroughs-ridership) (amNY, Nov 2025): 2025 ridership and e-bike growth
- [2026 NYC Heat-Related Mortality Report](https://a816-dohbesp.nyc.gov/IndicatorPublic/data-features/heat-report/) (NYC Health Department)
