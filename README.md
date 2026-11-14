# Telco Customer Churn: Exploratory Data Analysis

An end-to-end exploratory data analysis of customer churn for a telecom provider, using Python (Pandas, NumPy, SciPy, Matplotlib, Seaborn). The project covers dataset selection, data exploration, cleaning, statistical EDA, visualization and business recommendations.

## Business question
Which customers are most likely to leave, and what can the company do about it?

## Dataset
IBM Telco Customer Churn sample dataset: 7,043 customers, 21 variables (demographics, account details, subscribed services, charges, and the `Churn` target).
Source: <https://github.com/IBM/telco-customer-churn-on-icp4d>. Check the source repository for its licence terms before reusing the data.

## Key findings
| Finding | Evidence |
|---|---|
| Overall churn is 26.5%, about 30% of monthly recurring revenue | 1,869 of 7,043 customers |
| Contract type is the strongest driver | Month-to-month 42.7% vs 1-year 11.3% vs 2-year 2.8% |
| The first year is the danger zone | 47.4% churn at 0-12 months tenure vs 9.5% at 49-72 months |
| Fiber-optic customers churn at twice the DSL rate | 41.9% vs 19.0% |
| Electronic-check payers are the least stable | 45.3% vs 15-17% for automatic payments |
| Support add-ons are associated with lower churn | Among internet customers, about 15% with Online Security or Tech Support vs about 42% without |
| Gender has no meaningful effect | 26.9% vs 26.2%, not significant |
| Highest-risk segment: month-to-month, first year | 51.4% churn; about 55% of all churners from about 28% of customers |

The data is a single snapshot, so results show associations, not causes.

## Data issues found and fixed
- `TotalCharges` was stored as text with 11 blank values; all belong to customers with tenure 0, so they were set to 0.
- Inconsistent labels ("No internet service", "No phone service") merged into "No" for add-on columns.
- `SeniorCitizen` recoded from 0/1 to No/Yes.
- No duplicates and no outliers (IQR and Z-score checks) were found.

## Repository structure
```
telco-churn-eda/
├── data/raw/Telco-Customer-Churn.csv   # original dataset
├── notebooks/Telco_Churn_EDA.ipynb     # full analysis (executed, outputs included)
├── reports/
│   ├── Telco_Churn_EDA_Report.docx     # the whole analysis as a Word report
│   └── Telco_Churn_EDA.html            # HTML export of the notebook
├── images/                             # all charts as PNG
├── requirements.txt
├── LICENSE
└── README.md
```

## How to run
```bash
git clone https://github.com/<your-username>/telco-churn-eda.git
cd telco-churn-eda
python -m venv .venv && source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook notebooks/Telco_Churn_EDA.ipynb
```
The notebook downloads the data from IBM's GitHub and falls back to the local copy in `data/raw/` if offline.

## Visualizations
![Churn distribution](images/01_churn_distribution.png)
![Churn by contract, internet service and payment method](images/04_churn_by_contract_internet_payment.png)
![Churn by tenure](images/05_churn_by_tenure.png)
![Customer segments](images/10_customer_segments.png)

## Recommendations
1. Convert month-to-month customers to annual contracts, especially in months 3-12.
2. Build a first-year onboarding and check-in programme.
3. Bundle or trial Online Security and Tech Support for new internet customers.
4. Investigate fiber-optic service quality and pricing.
5. Move customers to automatic payment.
6. Target retention spend by value and risk.

## Next steps
Build a predictive model (logistic regression / gradient boosting) with class-imbalance handling, then A/B test the retention offers.
