# Delay prediction
Date: 22.09.2025.

This is a README template describing the delay prediction project. The goal is to create a regression model that is able to **predict the departure delay** for every flight of Alaska Airline for the second half of 2018. Task is to analyze the data, find patterns, build models for continuous outcome (any type, such as regression, tree, NN or else).  
Additional hints:
- Any publicly available additional variables can be used.
- Solutions will be compared via RMSE and R2, business acumen, creativity and coding skills.
- Use the format in submission_sample file when creating predictions.

Solutions, explanations, all information can be found in the code/ folder in the form of notebooks. Final prediction is saved in output/.

## Data

The U.S. Department of Transportation's (DOT) Bureau of Transportation Statistics (BTS) tracks the on-time performance of domestic flights operated by large air carriers. Summary information on the number of on-time, delayed, canceled and diverted flights appears in DOT's monthly Air Travel Consumer Report, published about 30 days after the month's end, as well as in summary tables posted on this website. BTS began collecting details on the causes of flight delays in June 2003. Summary statistics and raw data are made available to the public at the time the Air Travel Consumer Report is released.
This dataset only contains flight operated by Alaska Airlines.

There are 5 data files provided:
* 2014_.csv
* 2015_.csv
* 2016_.cs
* 2017_.csv
* 2018_.csv

External data:
* airports.csv

For identifying domestic/international flights: list of US airports https://www.kaggle.com/datasets/aravindram11/list-of-us-airports (downloaded: 21.09.2025.)


## Folder structure
delay_prediction/
├── code/
│   ├── 1_clean.ipynb
│   ├── 2_analysis.ipynb
│   ├── 3_prediction.ipynb
│   └── main.ipynb
├── data/
│   ├── cleaned_df.parquet
│   └── raw/
│       ├── 2014_.csv
│       ├── 2015_.csv
│       ├── 2016_.csv
│       ├── 2017_.csv
│       └── 2018_.csv 
├── doc/
│   ├── readme.txt
│   └── submission_sample.csv
├── output/
│   ├── past_data_report
│   ├── predict_data_report
│   └── prediction.csv
├── environment.yml
├── requirements.txt
└── README.md


## Getting Started

The analysis can be run by code/main.ipynb, which sets the working directory, saves the requirements.txt (it might change during later analysis) and runs all relevant code in the appropriate order.

### Requirements

A step by step series of examples that tell you how to get a development/analysis env running

Option 1 (conda)
```
conda env create -f environment.yml
conda activate myenv310
```

Option 2 (pip)

```
pip install -r requirements.txt
```

### Main Dependencies

- **Python** 3.12
- **jupyter / ipykernel** – running notebooks
- **numpy** – numerical computations
- **pandas** – data manipulation and analysis
- **matplotlib** – plotting and visualization
- **sweetviz** – automated exploratory data analysis (EDA) reports
- **seaborn** – statistical data visualization
- **scikit-learn** – machine learning
- **lightgbm** - gradient boosting method optimized for speed and memory

## Notes

Further steps / precatuions:

1. Business Understanding
- **Clarify the samples**: Is it the complete population of flights or can any sampling bias be present? Which is the best comparable sample (eg just 2018)?  Does external validity of model estimated on past data hold for data in 2018 Q3, Q4?
- Look for **signs of possible concept drift or covariate shift**: any structural break in Alaska Airline operations? eg. merger, acquisition, change in dest/origin places?
- EDA: talk to the business and figure out/reassure the typical **patterns, causality map, intuition, etc.. based on domain knowledge**.
- Talk to business unit to reconcile the findings and outline next steps. If makes sense, define additional research question to scale up the possible effect of the findings (eg look **not only departure delay but arrival delay, carriage delay, cancelling**). Based on that can we define appropriate data (sampling), valiables and methods.
- Look at the **recent literature, models of other airlines** --> replicate findings?
- If feature importance is relevant: analyze **SHAP and coefficient table**.
- Think about **outliers**: are they present? If yes: what might they be? how can we clean them, what rule would make sense (eg. drop some too high delays, or airports with too low frequency). Until we don't do these, results can be misleading/biased due to oultiers or data error.

2. Further data cleaning/preparation
- Probably some more **feature engineering** would make sense where we create categories eg. use morning, afternoon instead of hours. This should be reconciled with the business. 
- What **other relevant varibles** should we collect/involve in analysis?
    - **Geographic factors** that influence flight delays: eg. (economic) events in origin/dest.
    - **Weather**: expected weather around the airports and on the routes.
    - We can access the ranking time trend, it can be also included in the analysis. It makes sense for this exercise, but in a real-life scenario it only make sense if we have access to predicted time trend, otherwise it is only **data leakage**. https://www.bts.gov/topics/airline-time-tables : ranking time trend
    - For visualizations, a map would be nice with coordinates and routes with color and width as information:
https://www.kaggle.com/datasets/sanjeetsinghnaik/world-airport-dataset
https://datahub.io/core/airport-codes
https://www.kaggle.com/datasets/joebeachcapital/airport-codes
- Deal with memory usage! Optimize the model for memory-efficiency (eg. train on random sub-sample), or get **more computing capacity** for proper calculation.
- Selection of variables (lasso, ridge, elasticnet).
- Fine-tuning of model(s).

3. More production-ready code
- Use Jupytext to create .py files for **version control** and use git to collaborate (or similar depending on the tech stack, collaborators, data security).
- Kaggle API for automated use of external data sources.

## Author

* **Imola Csóka** - [https://csokaimola.github.io/](https://csokaimola.github.io/); csokaimola@gmail.com