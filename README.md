# Matching Customers with the Right Products During Targeted Emails

This repository presents a machine learning approach to optimizing promotional email campaigns for a large **sports retailer**. The objective is to identify the best email message or no message at all for each customer in order to maximize purchase probability and expected profit.

## Project Context

In high-frequency marketing environments, sending too many irrelevant emails can overwhelm customers and lead to higher unsubscribe rates, reducing long-term customer value. This project uses a historical dataset of customer interactions to:

- Predict the likelihood of purchase following different promotional emails
- Estimate the profit from those purchases (based on order size and cost of goods)
- Recommend the most profitable message per customer, including the option of sending no email

The goal is to personalize marketing messages based on customer characteristics and behavior to improve conversion and profitability across large-scale campaigns.

## Dataset Description

The dataset contains **600,000 customer–email interaction records**, with each row representing the last promotional email received by a customer. It includes:

### 1. Demographics
- `age`: Categorized into four brackets: `<30`, `30–44`, `45–59`, `60+`
- `female`: Binary indicator of gender
- `income`: Customer’s income (rounded to nearest €5,000)
- `education`: Percentage of college graduates in the customer’s neighborhood (0–100)
- `children`: Average number of children in the customer’s neighborhood

### 2. Purchase History
- Department-specific purchase frequencies over the past year:
  - `freq_endurance`
  - `freq_strength`
  - `freq_water`
  - `freq_team`
  - `freq_backcountry`
  - `freq_racquet`

### 3. Email Treatment
- `message_type`: One of six promotional categories:
  - Endurance, Strength, Water, Team, Backcountry, Racquet
  - Or `no-message` (control group that received no promotional email)

### 4. Response Variables
- `buyer`: Whether the customer made a purchase within 2 days (`yes`/`no`)
- `total_os`: Order size in Euros (if a purchase was made)

The data is randomly split into a **70% training set** and **30% test set**.

## Modeling Approach

The project involves two core predictive tasks:

### Task 1: Classification (Predicting Purchase Probability)
Models predict the likelihood that a customer will make a purchase after receiving a particular email message:

- Logistic Regression
- Random Forest Classifier
- XGBoost Classifier
- Neural Network Classifier

### Task 2: Regression (Predicting Order Size)
For customers predicted to make a purchase, models estimate their likely order size:

- Random Forest Regressor
- XGBoost Regressor
- Neural Network Regressor

**Expected profit** is calculated as:

```
expected_profit = purchase_probability * order_size * 0.40
```

*(Assuming 60% cost of goods sold)*

## Evaluation Metrics

To assess model performance:

- **Classification:** AUC (Area Under Curve), Gains curves
- **Regression:** R², RMSE (Root Mean Squared Error)
- **Business Simulation:** Expected profit per customer across different email strategies

## Strategy Comparison

We compare performance under multiple strategies:

1. **Personalized Assignment:** Select the best message (or no-message) for each customer individually.
2. **Single Message to All:** Send the same message to all customers.
3. **Random Assignment:** Randomly assign each customer to one message or the control group.
4. **No Messaging:** Use no promotional emails.

## Key Findings

- Personalized targeting outperforms all other strategies in expected profit.
- Some customer segments are more responsive to specific messages, while others are better left uncontacted.
- Random or uniform email strategies lead to lower engagement and profit.


## Technologies Used

- Python
- Jupyter Notebook
- Scikit-learn
- XGBoost
- TensorFlow / Keras
- Pandas, NumPy
- Matplotlib, Seaborn


