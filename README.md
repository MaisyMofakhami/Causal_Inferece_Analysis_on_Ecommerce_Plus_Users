# Causal Inference Analysis: JD Ecommerce

## Problem Formulation
JD.com is China’s largest retailer, boasting a net revenue of US$67.2 billion in 2018 and over 320 million annual active customers. JD.com offers a **PLUS membership program**, which provides benefits like loyalty points, exclusive offers, and discounts. 

This study aims to analyze the **causal impact of PLUS membership on customer spending behavior**. Specifically, we seek to answer the question:

> *How valuable would it be for JD.com to encourage more users to subscribe to PLUS membership in terms of increasing spending?*

Understanding this relationship will help JD.com refine its marketing strategies, pricing models, and customer engagement tactics.

## Dataset Overview
The dataset, provided by JD.com, captures a **full customer experience cycle** from browsing to purchase. Key statistics include:
- **2.5 million customers** (457,298 of whom made purchases)
- **30,000 SKUs** from a single product category
- Data timeframe: **March 2018**
- Source: [JD.com Research Paper](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3511861)


## **Causal Inference Model Description**

**Treatment Variable:** Whether a user is a PLUS member (plus).

**Outcome Variable:** Total spending (final_unit_price * quantity).

**Control Variables:** User attributes (user_level, purchase_power, education, marital_status, gender)

![image](https://github.com/user-attachments/assets/8cb97c4e-a291-473c-80e5-14a455d92d1a)


## Methodology and Models
To establish causality, we employed **Causal Inference techniques**, specifically:

### 1. **Exploratory Data Analysis (EDA)**
- Examined customer behaviors based on PLUS membership status
- Compared spending patterns and product preferences
- Identified key features affecting purchase amounts

### 2. **Propensity Score Matching (PSM)**
- Matched PLUS and non-PLUS members based on similarities in pre-membership characteristics
- Balanced covariates to reduce bias

### 3. **Meta-Learners (Causal ML)**
- Implemented:
  - Backdoor (DoWhy) 
  - LRSRegressor (S-Learner)
  - XGBTRegressor (T-Learner)

### 4. **Regression Analysis**
- Applied **Linear Regression and XGBoost Regression** to validate causal relationships
- Controlled for potential confounders

## Libraries Used
- dowhy
- causalml
- numpy
- pandas
- matplotlib
- statsmodels

## Results
The key findings from our analysis:
- **PLUS membership has a significant positive impact on customer spending.**
- Customers with PLUS membership tend to spend **X% more** than non-PLUS members (exact numbers depend on model specifications).
- The effect persists even after controlling for selection bias and other confounders using causal inference methods.
- Here is the feature importance chart that compares how different factors influence total spending for PLUS vs. Non-PLUS users
  
![image](https://github.com/user-attachments/assets/44b636a9-8d7b-460f-8d34-b1656ebffc03)


## Conclusion

### **Causal Inference Results: Effect of PLUS Membership on Spending**

| **Analysis Type** | **Estimated Causal Effect** | **Interpretation** |
|------------------|--------------------------|-------------------|
| **All Users (Including Non-Purchasers)** | **+25** | PLUS membership is associated with higher spending when considering all users, even those who didn’t purchase. |
| **Only Users Who Made a Purchase in That Month** | **Negative Effect (~ -8)** | Among active buyers, PLUS members actually spend less compared to active non-PLUS users. |

## *Possible Explanations for the Negative Effect:*

1. There might be hidden confounders (e.g., income level, shopping frequency) that were not included in the model.
If high-income shoppers tend to not subscribe to PLUS but spend more, this could bias the results.

2. This data is only for one month, so if the regular frequency of purchasing from JD.com is more than 30 months, we are losing important data by only looking at one month.

## *Possible Explanation for the Positive Effect on all Users:*

PLUS users may tend to purchase in smaller baskets but with higher frequency. Since delivery costs are not an issue for them and they have access to exclusive deals, their shopping behavior might shift—they no longer wait to reach a minimum order value before making a purchase. Instead, they may place more frequent, smaller orders.

However, we cannot confirm this hypothesis with just one month of data. A more extended analysis is needed to evaluate whether PLUS members make more purchases over time and to assess the potential additional costs these smaller basket sizes may impose on JD.com’s logistics and fulfillment operations.

---

## Acknowledgments
- JD.com for providing the dataset
- Causal inference literature and methodologies used in the analysis
- This project was done for Course INSY 695 - Advanced Topics in IS
  
---

## References

- [JD.com Dataset Paper](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3511861)
- [Causal Inference Methods](https://www.causalinferencebook.com/)

