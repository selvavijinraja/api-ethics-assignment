# ML Workflow Assignment

## Problem Statement
You are a junior data analyst at a retail company. Your manager hands you a dataset of past customer orders and asks you to build a model that predicts whether a customer will make a repeat purchase within 30 days.

The dataset contains the following columns:

- **customer_id**: Unique customer identifier  
- **order_count_last_90d**: Number of orders placed in the last 90 days  
- **avg_order_value**: Average order value in INR  
- **days_since_last_order**: Days elapsed since the customer's most recent order  
- **repeat_purchase_flag**: 1 if the customer made a repeat purchase within 30 days, 0 otherwise  
- **discount_used_on_repeat_order**: Discount applied on the repeat purchase order  

---

## Task 1
**Identify which column in the dataset is the label, and which column, if included as a feature, would introduce data leakage. For each, write one sentence justifying your choice.**

- **Label:** `repeat_purchase_flag`  
  *Justification:* This column represents the target outcome we want to predict — whether a customer makes a repeat purchase within 30 days.  

- **Leaky Feature:** `discount_used_on_repeat_order`  
  *Justification:* This column contains information that is only available after the repeat purchase has already occurred, so including it would leak future knowledge into the model.  

---

## Task 2
**Your manager skips straight to training a gradient boosting model. Suggest two steps from the complete ML workflow that should have been completed first, and briefly explain why each step matters before jumping to a complex model.**

1. **Define Features and Label**  
   *Explanation:* Clearly identifying the target variable (`repeat_purchase_flag`) and the input features ensures the model is trained on the right data and avoids including leaky or irrelevant variables.  

2. **Split the Data into Training and Validation/Test Sets**  
   *Explanation:* Dividing the dataset allows us to evaluate how well the model generalizes to unseen data, preventing overfitting and ensuring reliable performance measurement.  

---
