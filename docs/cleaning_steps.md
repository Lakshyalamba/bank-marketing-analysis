# Cleaning Steps

The cleaning process transformed the raw bank marketing data into a structured format suitable for analysis and Tableau dashboarding.

## 1. Column Renaming and Standardization

All column headers were renamed from technical or shorthand names to descriptive names for better readability.

| Raw Column | Cleaned Column |
| --- | --- |
| `age` | `Age` |
| `job` | `Job` |
| `marital` | `Marital_Status` |
| `education` | `Education` |
| `default` | `Has_Credit_Default` |
| `housing` | `Has_Housing_Loan` |
| `loan` | `Has_Personal_Loan` |
| `contact` | `Contact_Type` |
| `month` | `Contact_Month` |
| `day_of_week` | `Contact_Day` |
| `duration` | `Call_Duration_Seconds` |
| `campaign` | `Campaign_Contacts` |
| `pdays` | `Days_Since_Previous_Contact` |
| `previous` | `Previous_Contacts` |
| `poutcome` | `Previous_Campaign_Outcome` |
| `emp.var.rate` | `Employment_Variation_Rate` |
| `cons.price.idx` | `Consumer_Price_Index` |
| `cons.conf.idx` | `Consumer_Confidence_Index` |
| `euribor3m` | `Euribor_3_Month` |
| `nr.employed` | `Number_Employed` |
| `y` | `Subscribed_Term_Deposit` |

## 2. Data Value Standardization

Categorical values were cleaned and formatted for consistency.

- **Job titles:** Capitalized values and removed technical punctuation. For example, `admin.` became `Admin`, and `blue-collar` became `Blue Collar`.
- **Education levels:** Replaced shorthand values with readable descriptions. For example, `basic.4y` became `Basic 4 Years`, and `university.degree` became `University Degree`.
- **Boolean-like fields:** Standardized `yes`, `no`, and `unknown` values in default, housing loan, and personal loan columns to `Yes`, `No`, and `Unknown`.
- **Subscription outcome:** Replaced `yes` and `no` with `Subscribed` and `Not Subscribed`.

## 3. Feature Engineering

Several new columns were created to improve analysis and dashboard usability.

| New Column | Description |
| --- | --- |
| `Age_Group` | Binned `Age` into groups: `Below 25`, `25-34`, `35-44`, `45-54`, `55-64`, and `65+`. |
| `Call_Duration_Minutes` | Converted `Call_Duration_Seconds` into minutes by dividing seconds by 60. |
| `Campaign_Contact_Group` | Grouped campaign contact counts into categories such as `1 Contact`, `2-3 Contacts`, `4-6 Contacts`, and `7+ Contacts`. |
| `Previous_Contact_Status` | Labeled records as `Not Previously Contacted` when `Days_Since_Previous_Contact` was `999`; otherwise labeled them as `Previously Contacted`. |
| `Days_Since_Previous_Contact_Clean` | Created a numeric version of previous contact days where the placeholder value `999` was replaced with a blank/null value. |
| `Subscribed_Flag` | Added a binary indicator where `1` represents `Subscribed` and `0` represents `Not Subscribed`. |

## 4. Data Quality and Formatting

- **Numeric conversion:** Ensured financial and economic indicator columns, including `Euribor_3_Month`, `Consumer_Price_Index`, `Consumer_Confidence_Index`, `Employment_Variation_Rate`, and `Number_Employed`, are treated as numeric values.
- **Placeholder handling:** Addressed the `999` placeholder in the original `pdays` field, which indicates that a customer was not previously contacted.
- **Dashboard readiness:** Prepared the cleaned dataset with readable labels, grouped dimensions, and numeric analysis fields for use in Tableau.

## Output

The cleaned dataset is stored at:

```text
data/cleaned/bank_marketing_cleaned.csv
```
