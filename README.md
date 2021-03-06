# Unsupervised anomaly detection (fraud) for New York housing

# Data Quality Report(DQR)
  The Data Quality Report has 3 main Components:
  1. High-level description of the data
  2. Two field summary tables
     Numeric fields( %populated, min, max, mean, standard deviation, # zeros
     Categorical fields ( # populated, # unique values, most common field value
  3. The distribution of each fields

For more details, please see the "NY housing DQR.docx" file.

# Detail Steps and Methodology 
I am doing a forensic-type analysis, looking for anomalies in a dataset. We first do some data cleaning (exclusions, imputation), then build variables that are designed to look for the kinds of anomalies we are interested in, in this case, unusual property valuations.

After we build the variables we know we have lots of correlations and too high dimensionality so we need to remove correlations and reduce dimensionality. Since we don't have a dependent variable the easiest useful thing to do is PCA. We z scale, do PCA, keep the top PCs, then z scale again in order to make each retained PC equally important (optional step).

We use two different anamaly detection (fraud) algorithms. The first just looks for outliers in the final scaled PC space using a Minkowski distance from the origin. The second method makes a simple autoencoder and the fraud score is then the reproduction error. It's important to note that each/either of these two methods would be a fine fraud score by itself.

Since we have two score and we don't really know which one is better we just average the two scores. To do this we replace the score with its rank order and then average the rank-ordered scores for our final score.

Finally we sort all the records by this final score and explore the top n records. To help the investigation we show which of the variables are driving these top scoring records with a heat map of the variable zscores, which can point the investigators to what's making the high score for these top scoring records.

The data can be found here: https://data.cityofnewyork.us/Housing-Development/Property-Valuation-and-Assessment-Data/rgy2-tti8

For more details, please see the "NY unsupervised fraud.ipynb" file.

# Discover the possible fraud

After doing all the steps I have metioned above, I output a excel file with 1000 records which have the highest final score and investigate the anomalies in this excel files. Please open "NY_top_with_zs.xlsx" for more details.

After reviewing all the record in the excel files, I write a report for 5 suspicous record in a docs file and the reaason why they are being reported.
Please open "Possible Fraud Report.docx" for more details.
