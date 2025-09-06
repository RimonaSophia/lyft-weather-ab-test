# Lyft Ride Volume A/B Test: Good vs. Bad Weather

This project simulates an A/B test to see if ride volume per hour changes during bad weather. I used a real-world dataset that combines Lyft/Uber rides and hourly weather data in the Boston area.

## Project Goal

Test if **bad weather increases ride demand**, using hourly ride data as our unit of analysis. This is done using both:
- Frequentist (t-test)
- Bayesian (conversion rate comparison)

## Dataset

The data came from a public Kaggle dataset that tracks Uber and Lyft rides with hourly weather information (temperature, precipitation probability, short summary, etc). I didn't collect the data, just used it to build out a testing framework.

## Key Steps

1. Cleaned and extracted features (hour, day, weather conditions)
2. Defined bad weather using rules:
   - Precipitation probability > 30%
   - Temperature < 5°C
   - Summary contains rain/snow
3. Balanced the dataset by **downsampling good weather hours** to match bad weather hours
4. Grouped rides by hour and weather condition
5. Ran a t-test and a Bayesian simulation to compare ride volumes

## Assumptions I Made

- Hourly ride data can be used like sessions in an A/B test
- Weather isn't randomized, so I manually balanced the groups
- Didn't control for external factors (like price changes, events, etc)
- Each hour is treated as independent (realistically, some correlation exists)

## Results

- **T-test** showed a statistically significant increase in ride volume during bad weather (t = 2.63, p = 0.0104)
- **Bayesian** test did not show strong evidence that bad weather leads to higher volume (P = 0.419)

## Insights

- Hourly ride volume was **higher on average in bad weather**, but the difference isn’t massive
- Significance depends on how you sample and define your groups
- Good example of how A/B testing frameworks can be adapted for observational data

## Next Steps

- Add other features like surge pricing or location
- Try causal inference methods instead of standard A/B
- Explore weather severity (light vs heavy rain/snow)

## Tools Used

- Python (pandas, numpy, seaborn, matplotlib)
- `scipy.stats` for the t-test
- `scikit-learn` for resampling
- `scipy.stats.beta` for Bayesian comparison
