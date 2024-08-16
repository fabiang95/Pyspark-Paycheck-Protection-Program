# Pyspark-Paycheck-Protection-Program
This project builds a binary classification ML model using the available borrower, lender and loan information to predict LoanStatus. Due to the size of the training dataset, bid data strategies are adopted and pyspark is used with the script being ran on databricks. 

# Project objective
In the spring of 2020, the US government announced a loan program, called Paycheck Protection Program (PPP), to help stabilize the American economy in the face of job losses related to the COVID-19 pandemic. 

The objective is to create a binary classification model such that when a loan program is required, we can use this model to predict whether the borrower will pay back the loan in full or not. 
Since the dataset contains close to a million rows and we have to consider approaches that allows it to be computed via a multi-node approach. 

# Dataset 
The dataset name is public_150k_plus_230930.csv
You may download it from this link: https://data.sba.gov/dataset/ppp-foia

As the objective is for future predictions, it is important to consider columns that are available at at the point of borrowing. 

| Field Name | Available at the time of Loan Application? |
|----------|----------|
| LoanNumber	| No |
| DateApproved	| No |
| SBAOfficeCode	| No |
| ProcessingMethod	| No |
| BorrowerName	| Yes |
| BorrowerAddress	| Yes |
| BorrowerCity	| Yes |
| BorrowerState	| Yes |
| BorrowerZip	| Yes |
| LoanStatusDate	| No |
| LoanStatus	| No |
| Term	| Yes |
| SBAGuarantyPercentage	| No |
| InitialApprovalAmount	| Yes |
| CurrentApprovalAmount	| No |
| UndisbursedAmount	| No |
| FranchiseName	| Yes |
| ServicingLenderLocationID	| No |
| ServicingLenderName	| No |
| ServicingLenderAddress	| No |
| ServicingLenderCity	| No |
| ServicingLenderState	| No |
| ServicingLenderZip	| No |
| RuralUrbanIndicator	| Yes |
| HubzoneIndicator	| Yes |
| LMIIndicator	| Yes |
| BusinessAgeDescription	| Yes |
| ProjectCity	| Yes |
| ProjectCountyName	| Yes |
| ProjectState	| Yes |
| ProjectZip	| Yes |
| CD	| Yes |
| JobsReported	| Yes |
| NAICSCode	| Yes |
| Race	| Yes |
| Ethnicity	| Yes |
| UTILITIES_PROCEED	| Yes |
| PAYROLL_PROCEED	| Yes |
| MORTGAGE_INTEREST_PROCEED	| Yes |
| RENT_PROCEED	| Yes |
| REFINANCE_EIDL_PROCEED	| Yes |
| HEALTH_CARE_PROCEED	| Yes |
| DEBT_INTEREST_PROCEED	| Yes |
| BusinessType	| Yes |
| OriginatingLenderLocationID	| Yes |
| OriginatingLender	| Yes |
| OriginatingLenderCity	| Yes |
| OriginatingLenderState	| Yes |
| Gender	| Yes |
| Veteran	| Yes |
| NonProfit	| Yes |
| ForgivenessAmount	| No |
| ForgivenessDate	| No |

# Main Approach
## creating training dataset 
1. To ensure balance of datasets, use sampling to ensure that "Paid in Full" has approximately same number of rows as "Charged off" + "Exemption"
2. change label to boolean such that {"Paid in Full": 1, "Charged Off": 0, "Exemption": 0}

## data pre-processing 
### feature engineering 
Ensure that only columns available at time of loan application is used.
### performing EDA 
1. inspect which are categorical columns and which are numerical columns
2. inspect cardinality of categorical columns, drop if necessary

## Build ML pipeline 
1. encode categorical columns and vectorize
2. vectorize and scale numerical columns
3. train binary classification model (random forest was used) using training data dataset

## Evaluate 
1. Evaluate training accuracy
2. Evaluate test accuracy 
