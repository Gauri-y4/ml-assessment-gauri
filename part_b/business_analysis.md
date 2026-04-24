# PART B: BUSINESS CASE ANALYSIS

# B1. Problem Formulation
(a)
The target variable is 'items_sold'.

Input features can include:
- Promotion type
- Store size
- Location type
- Competition density
- Customer activity (visits, basket size)
- Time features (month, weekend, festival)

This is a 'supervised regression problem' because we are predicting a continuous value (items sold) using past data.

(b)
- Revenue can be misleading because it depends on price and discounts. A promotion might increase the number of items sold but reduce revenue.
- Items sold directly shows how customers respond to promotions, so it is more reliable.
- This shows that the target variable should match the business goal and should not be affected by external factors.

(c)
- Instead of one global model, we can use **separate models for different store types** (urban, semi-urban, rural).\
- This is better because customer behavior and promotion effectiveness vary by location, so separate models can give more accurate results.

# B2. Data and EDA Strategy
(a)

The tables would be joined using:
- store_id (for store data)
- transaction_date (for calendar data)
- promotion type or ID (for promotion data)

The final dataset will be at a 'monthly store level', meaning one row represents one store for one month.

Aggregations include:
- Total items sold
- Total visits
- Average basket size
- Promotion used

(b)
1. Distribution of items_sold
   To check outliers and skewness
2. Boxplot of items_sold by promotion
   To compare promotion performance
3. Correlation heatmap
   To understand relationships between features
4. Time series plot of sales
   To identify trends and seasonality

These help improve feature engineering and model selection.

(c)
If 80% of data has no promotion, the model may focus too much on non-promotion cases.

To fix this:
- Use balanced data or weighting
- Ensure promotion data is properly represented
- Evaluate model separately for promotion cases

# B3. Model Evaluation and Deployment
(a)
Use a 'time-based split', where older data is training data and recent data is test data.
Random split is not suitable because it mixes past and future data.

Metrics:
- RMSE → shows error size
- MAE → shows average error
- R² → shows how well model explains data
  
(b)
- Feature importance helps identify which factors influenced the model.
- For example, in December, festivals may make loyalty promotions more effective. In March, discounts may work better.
- These insights can be shared with the marketing team to explain different recommendations.

(c)
The model can be saved using tools like joblib.
Each month, new data is processed using the same pipeline and passed to the model for predictions.

Monitoring includes:
- Checking prediction errors
- Comparing actual vs predicted values
- Retraining when performance drops
