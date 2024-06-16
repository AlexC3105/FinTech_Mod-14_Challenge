# Trading Bot Analysis

This document details the process and results of tuning the baseline trading algorithm and evaluating new machine learning classifiers for the trading bot.

---

## Tune the Baseline Trading Algorithm

### Step 1: Tune the Training Algorithm by Adjusting the Size of the Training Dataset

**Experiment 1: Training Window of 3 Months**

- **Results**: (Provide the cumulative returns plot and performance metrics)
- **Impact**: (Describe the impact of this training window on the trading outcomes)

**Experiment 2: Training Window of 6 Months**

- **Results**: (Provide the cumulative returns plot and performance metrics)
- **Impact**: (Describe the impact of this training window on the trading outcomes)

**Conclusion**: (Summarize the findings and choose the best training window)

### Step 2: Tune the Trading Algorithm by Adjusting the SMA Input Features

**Experiment 1: SMA Fast = 4, SMA Slow = 100**

- **Results**: (Provide the cumulative returns plot and performance metrics)
- **Impact**: (Describe the impact of these SMA windows on the trading outcomes)

**Experiment 2: SMA Fast = 10, SMA Slow = 50**

- **Results**: (Provide the cumulative returns plot and performance metrics)
- **Impact**: (Describe the impact of these SMA windows on the trading outcomes)

**Conclusion**: (Summarize the findings and choose the best SMA parameters)

### Step 3: Choose the Set of Parameters that Best Improved the Trading Algorithm Returns

- **Final Parameters**: (List the best parameters chosen)
- **Results**: (Provide the cumulative returns plot for the best parameters)
- **Conclusion**: (Summarize why these parameters were chosen)

---

## Evaluate a New Machine Learning Classifier

### Step 1: Import a New Classifier

**Classifier Used**: AdaBoostClassifier

### Step 2: Train and Evaluate the New Classifier

#### Classification Report

```plaintext
               precision    recall  f1-score   support

         -1.0       0.44      0.08      0.13      1804
          1.0       0.56      0.92      0.70      2288

    accuracy                           0.55      4092
   macro avg       0.50      0.50      0.41      4092
weighted avg       0.51      0.55      0.45      4092
```

**Analysis:**

- The accuracy of the AdaBoost model is 55%.
- The model performs better in predicting the class `1.0` (buy signal) with a recall of 92% and an f1-score of 0.70.
- The model struggles with predicting the class `-1.0` (sell signal), achieving a recall of only 8% and an f1-score of 0.13.
- Overall, the model has a balanced precision and recall, with macro and weighted averages around 0.50.

### Predictions DataFrame

```plaintext
| Date                | Predicted | Actual Returns | Strategy Returns |
|---------------------|-----------|----------------|------------------|
| 2015-07-06 10:00:00 | 1.0       | -0.025715      | -0.025715        |
| 2015-07-06 10:45:00 | -1.0      | 0.007237       | -0.007237        |
| 2015-07-06 14:15:00 | -1.0      | -0.009721      | 0.009721         |
| 2015-07-06 14:30:00 | -1.0      | -0.003841      | 0.003841         |
| 2015-07-07 11:30:00 | -1.0      | -0.018423      | 0.018423         |
| ...                 | ...       | ...            | ...              |
| 2021-01-22 09:30:00 | 1.0       | -0.006866      | -0.006866        |
| 2021-01-22 11:30:00 | 1.0       | 0.002405       | 0.002405         |
| 2021-01-22 13:45:00 | 1.0       | 0.002099       | 0.002099         |
| 2021-01-22 14:30:00 | 1.0       | 0.001496       | 0.001496         |
| 2021-01-22 15:45:00 | 1.0       | -0.000896      | -0.000896        |
```

### Cumulative Returns Plot

**Analysis:**

- The cumulative returns plot shows the "Actual Returns" vs. "Strategy Returns" for both SVM and AdaBoost models.
- The strategy returns (orange line for SVM and green line for AdaBoost) closely follow the actual returns (blue line) for most of the period.
- Towards the end of the evaluation period, the strategy returns of the AdaBoost model significantly outperform the actual returns, indicating better performance in capturing profitable trades compared to the SVM model.

### Step 3: Conclusion

**Comparison with Baseline Model:**

- The AdaBoost model has a slightly higher accuracy compared to the baseline SVM model.
- The recall for the buy signal (class `1.0`) is significantly higher in the AdaBoost model.
- However, the precision for the sell signal (class `-1.0`) is lower in the AdaBoost model.

**Comparison with Tuned Trading Algorithm:**

- The AdaBoost model shows a balanced performance with an overall accuracy of 55%.
- The strategy returns of the AdaBoost model outperform the actual returns towards the end of the evaluation period, indicating better performance in capturing profitable trades.

**Final Thoughts:**

- The AdaBoost model demonstrates the potential for improved performance in algorithmic trading by leveraging ensemble learning techniques.
- Further tuning of the AdaBoost model's parameters and experimenting with other classifiers could yield even better results.
