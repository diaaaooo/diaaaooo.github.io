---
title: "Data Science Basics"
date: 2020-01-01T00:00:00+00:00
# weight: 1
# aliases: ["/first"]
tags: ["tag"]
author: "Diao"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
# description: "Desc Text."
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: false
ShowRssButtonInSectionTermList: true
UseHugoToc: true
# menu:
#   main:
#     identifier: "posts"
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
# editPost:
#     URL: "https://github.com/<path_to_repo>/content"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

## Model Performance Diagnose and Treatment
### Explain bias and variance
- What they are:
    - Bias: the incapability of the model, measurement of underfitting. 
    - Variance: the sensitivity of the model on training data, measurement of overfitting.
- How to measure:
    - Bias: the difference between the average model prediction and the true value, sum(y_true - y_pred_mean).
    - Variance: the difference between the model prediction and the true value, sum(y_true - y_pred).
- Practical guide:
    - Control bias: start with simple model (low variance, potentially high bias) and progressively increase its complexity.
    - Control variance: use cross-validation to estimate model performance on unseen data.
    - Manage trade-off: use L1, L2 regularization to help manage the trade-off. 

### Explain L1 (Lasso) and L2 (Ridge) regularization
- What they are:
    - L1 and L2 regularization are techniques to help manage bias-variance trade-off. They help prevent overfitting by penalizing large coefficients, which also introduce more bias to the model to help generalization. 
- How they work:
    - L1 regularization: add absolute values of coefficients to the loss function.
    - L2 regularization: add squared values of coefficients to the loss function.
    - lambda parameter: both have a lambda parameter to help control the strength of the penalty. Large lambda makes the model simpler, whereas small lambda remains the model complexity.
- What's the difference:
    - L1 regularization: it can drive some coefficients to zero, which leads to some features not being used by the model.
    - L2 regularization: it shrinks coefficients but not necessarily drive them to zero, which reduces the importance of less important features.
- Practical guide:
    - Use cross-validation to find the optimal lambda.
    - Use Elastic Net regularization (combination of L1 and L2) to find the optimal balance between L1 and L2. 
    - Different types of model has different types of regularization techniques. 
        - Tree-based models can use control tree depth, sample split, leafs, max features. 
        - NN-based models can use L1 and L2 regularization at kernel level to control weight decay, which will add a penalty to the loss function based on weights. NN-based models can also use dropout to randomly drop out units during training to prevent overfitting. NN-based models can also use early stopping to stop training when the performance on a validation set starts to degrade.

### Explain evaluation metrics
- Classification:
    - [Confusion matrix](https://www.evidentlyai.com/classification-metrics/confusion-matrix)
    - [Accuracy, Precision, Recall](https://www.evidentlyai.com/classification-metrics/accuracy-precision-recall)
    - [F-score](https://en.wikipedia.org/wiki/F-score)
    - [ROC, AUC](https://www.evidentlyai.com/classification-metrics/explain-roc-curve)
- Regression:
    - ...
- Recommendation System:
    - [Predictive Quality Metrics](https://www.evidentlyai.com/ranking-metrics/evaluating-recommender-systems#predictive-quality-metrics):
        - [Precision at K](https://www.evidentlyai.com/ranking-metrics/evaluating-recommender-systems#precision-at-k)
        - [Recall at K](https://www.evidentlyai.com/ranking-metrics/evaluating-recommender-systems#recall-at-k)
        - [F-score at K](https://www.evidentlyai.com/ranking-metrics/evaluating-recommender-systems#f-score)
        - [Precision, Recall and F-score at K](https://www.evidentlyai.com/ranking-metrics/precision-recall-at-k)
    - [Ranking Quality Metrics](https://www.evidentlyai.com/ranking-metrics/evaluating-recommender-systems#ranking-quality-metrics):
        - [Mean Reciprocal Rank (MRR)](https://www.evidentlyai.com/ranking-metrics/mean-reciprocal-rank-mrr)
        - [Mean Average Precision (MAP)](https://www.evidentlyai.com/ranking-metrics/mean-average-precision-map)
        - [Hit Rate](https://www.evidentlyai.com/ranking-metrics/evaluating-recommender-systems#hit-rate)
        - [Normalized Discounted Cumulative Gain](https://www.evidentlyai.com/ranking-metrics/ndcg-metric)
    - [Behavioral Metrics](https://www.evidentlyai.com/ranking-metrics/evaluating-recommender-systems#behavioral-metrics):
        - [Diversity](https://www.evidentlyai.com/ranking-metrics/evaluating-recommender-systems#diversity)
        - [Novelty](https://www.evidentlyai.com/ranking-metrics/evaluating-recommender-systems#novelty)
        - [Serendipity](https://www.evidentlyai.com/ranking-metrics/evaluating-recommender-systems#serendipity)
        - [Popularity Bias](https://www.evidentlyai.com/ranking-metrics/evaluating-recommender-systems#popularity-bias)
    - [Business Metrics](https://www.evidentlyai.com/ranking-metrics/evaluating-recommender-systems#business-metrics):
        - Revenue
        - Click-through Rate (CTR)
        - Conversion Rate
        - User Engagement Metrics

### Explain cross validation
- Why use it:
    - Prevent overfitting: verify model performance on unseen data
    - Model evaludation: evaluate model performance on generalization
    - Parameter tuning: assist in selecting best hyperparameters for the model
- Different types:
    - K-fold: split dataset into k folds evenly, train on k-1 folds and test on k fold, average metrics.
    - Stratified K-fold: ensure each fold has approximately the same distribution of class labels. Good for imbalanced data.
    - Rolling/Time-series: split dataset into k folds evenly, train on k1 and test on k2, then train on k1+ k2 and test on k3, keep rolling.
    - Leave One Out: use all data for training, only leave one sample out for testing, do it for iteratively until all samples have been left out once. Good for tiny datasets.
- How it works:
    - Split dataset based on chosen cross-validation method
    - Train on training set, test on test test
    - Repeat the process for all folds
    - Average metrics
- Practical guide:
    - Computation expensive
    - Reasonable choice of K, 5-10
    - Set random seed to ensure reproducible 

### What is selection bias?
- Different types:
    - Sample bias: training data is not representative enough of the real-world distribution.
    - Label bias: labels is not representative enough of the real-world distribution, for example: biased imbalanced labels.
    - Survivorship bias: only considering "survivied" samples, for example: only "succeed" cases.
    - Systematic bias: systermatically ignored or removed certain group of samples from training data
    - Nonreponse bias: only collected responsed data, forgot about non-responded data
- What it leads to:
    - Poor generalization
    - Skewed performance metrics/false sense of model performance
    - Unfair predictions, for example: hiring

### Explain correlation and causality
- What they are:
    - Correlation: help understand relationships (trend, directional) between variables, but doesn't explain why those relationship exists.
    - Causality: help understand cause-effect relationships between variables, and explain why those correlation exists.
- What they do:
    - Correlation: 
        - Guide feature selection and engineering
        - Indicate dimension reduction. High correlation among features can also inform dimensionality reduction techniques.
        - May highlight biased relationships that need correction.
    - Causality: 
        - Provides deeper insights into the model decisions
        - Understanding causal pathways helps in designing fairer algorithms by addressing root causes of bias.

### Explain confidence interval and uncertainty window
- Concept:
    - Confidence interval: Quantify an estimated range [X_min, X_max] and how confident you are (90%, 95%, 99%) that parameter X lies within that range.
    - Uncertainty Window: Represents a general range of possible values or outcomes, considering multiple sources of uncertainty.
- Probability and Interpretation:
    - Confidence Intervals: Associated with a specific confidence level (e.g., 95%), providing a probabilistic interpretation.
    - Uncertainty Window: Does not necessarily provide a probabilistic interpretation; it’s more about expressing the range of potential variability.
 - When to use it:
    - Confidence Intervals:
        - Estimate population parameters, like mean, proportion, difference between means.
        - Assess precision of estimations. Narrower intervals means more precise estimate, wider intervals indicates more uncertainty.
        - Hypothesis testing
    - Uncertainty Window: Used in predictive modeling and forecasting to communicate the range of potential future outcomes. 
- How to use it:
    - Confidence Intervals:
        - Must-know values: sample mean, sample size
        - If population standard deviation is known, use z-score; if unknown, use t-score with sample standard deviation.
    - Uncertainty Window:
        - Quantile regression: 
        Quantile regression estimates the conditional median or other quantiles of the response variable. This can be used to directly predict the lower and upper bounds of the prediction interval.
    - Boostrapping:
        Bootstrapping involves repeatedly sampling from the training data with replacement and training a model on each sample to build a distribution of predictions.
    - Bayesian Methods:
        Bayesian approaches provide a probabilistic framework for model predictions, naturally incorporating uncertainty. Gaussian Process Regression (GPR) is one such method.
    - Ensemble Methods:
        Ensemble methods like Random Forests can also be used to estimate prediction intervals by leveraging the variability in predictions from different trees.

### Explain prediction interval
- Definition:
A prediction interval provides a range within which future observations are expected to fall with a certain level of confidence. It accounts for both the variability in the data and the uncertainty in the prediction.
- Example:
If you predict the price of a house to be 300k with a 95% prediction interval of [280k, 320k], you are 95% confident that the actual price will fall within this range.
- How to use it:
    - Point Estimate: The predicted value (e.g., the mean prediction from a model).
    - Variance: The variability in the prediction due to the randomness in the data and the model.
    - PI = y_pred +- t * s_pred, t is the critical value from t-distribution, s_pred is the standard error of the prediction.
    - Some regression models provide it, or calculate s_pred manually from RSE or boostrap

### Explain Type I and Type II error
- Type I: false positive, false alarm
- Type II: false negative, miss

### Explain parametric and non-parametric model
- Parametric: assume underlying distribution, can't learn complex relationships in data
- Non-parametric: no assumption of underlying distribution, adapt and flexible

### What is multicolinearity and how to handle it in regression models?
Multicollinearity refers to the situation where two or more independent variables in a regression model are highly correlated with each other. 
- Identify:
    - Correlation Matrix
    - Variance Inflation Factor (VIF)
- Treatment:
    - feature engineering: remove or combine
    - dimensional deduction
    - regularization
    - cross validation

### How to find the optimal threshold for classifier?
- ROC, AUC
- Track and compare F-score

### Explain loss function and cost function
- Loss Function:
    - Measures individual prediction errors for each sample. 
    - Used during model training to update parameters iteratively.
- Cost Function: 
    - Aggregates the losses across all samples to provide a global measure of model performance.
    - Used as the optimization objective to minimize during training.

### What is essemable learning
Ensemble learning is a machine learning technique where multiple models are combined to improve the overall performance and robustness of the system. Instead of relying on a single model, ensemble methods leverage the collective wisdom of multiple models to make predictions or classifications. 

- Bagging (Bootstrap Aggregating):
    - train multiple base learners independently on different random subsets of the training data (bootstrap samples).
    - Examples: Random Forest, Bagged Decision Trees.

- Boosting: 
    - train base learners sequentially, where each subsequent learner focuses more on the examples that previous models struggled with, thereby reducing overall error.
    - Examples: GBM, XGBoost, LightGBM.

- Stacking:
    - combine predictions from multiple base learners using a meta-model (higher-level model). The meta-model learns how to best combine the predictions of base learners.

- Voting and Averaging:
    - aggregate predictions from multiple base learners through voting (for classification) or averaging (for regression).

### Explain Stochastic Gradient Descent (SGD) and Gradient Descent (GD)
- GD: Computes gradients using the entire dataset at each iteration, suitable for small to medium-sized datasets but computationally expensive for large datasets.
- SGD: Uses a single training example per iteration, faster for large datasets but noisy updates and may not converge to the global minimum.
- Mini-Batch GD: Uses small batches of data, balancing efficiency and stability for training.


### What is exploding gradient problems in ML
- Situation: the gradients of the loss function with respect to the model parameters grow exponentially during training, leading to extremely large gradient values.
- Cause:
    - Deep Networks
    - Large Initial Weights
    - Activation Functions: Certain activation functions, such as the sigmoid function, can saturate for large input values, causing gradients to become very small. This can lead to gradient vanishing in some layers and exploding gradients in others.
    - High Learning Rates: Using a learning rate that is too high can exacerbate the exploding gradient problem. Large learning rates cause large updates to the model parameters, amplifying the gradients.
- Treatment:
    - Weight Initialization
    - Gradient Clipping: set a threshold and clip
    - Batch Normalization: Apply batch normalization layers in deep neural networks to normalize the inputs to each layer, reducing the likelihood of exploding gradients.
    - Activation Functions: ReLU or Leaky ReLU
    - Reduce Learning Rate or use adaptive learner like Adam
    - Gradient Regularization: Apply gradient regularization techniques, such as L2 regularization or weight decay, to penalize large gradients and promote smoother optimization.

### Explain sigmoid and softmax
- Output Range:
    - Sigmoid: 0 and 1
    - Softmax: probability cross multi-class which sum up to 1.

- Application:
    - Sigmoid: binary classifiers or logistic regression models.
    - Softmax: multi-class classification tasks.
- Decision Boundary:
    - Sigmoid: threshold
    - Softmax: Provides probabilities for each class, allowing for more nuanced decisions in multi-class scenarios.


## Data Processing Techniques
### How to handle missing data?
- Why: check why they are missing. It may be caused by systematic error or intentionally left out. Ot it may be truly randomly missing.
- Handle:
    - Systematic: add an indicator for the model to know they are missing for the same reason
    - Random: choose the most reasonable method
        - fillin: mean/median/mode, knn inputation, use a small range of features to predict
        - allow-missing models: tree-based models
    - Don't drop data samples unless they really have no value.

### How to handle data suffering from high variance?
- Investigate
    - nvestigate and analyze the sources of high variance, such as noisy data or outliers, and take corrective actions such as data cleaning or outlier removal.
- Reduce variability
    - feature selection and dimention reduction
    - regularization
    - cross validation
    - esamble like random forest 
    - boosting like GBM
    - regularized models: SVM, NN at kernal level

### Explain PCA
- transform correlated data into uncorrelated smaller set, ensure features independent from each other and preserve variance.

### How to discover outliers
- Visualization: box plot, scatter plot
- Statistics: mean standard deviation, IQR, z-score

### What is Fourier Transform
- Fourier Transform is based on the idea that any periodic function can be expressed as a sum of sine and cosine functions with different frequencies.
- The Fourier Series deals with periodic functions, while the Fourier Transform extends this concept to non-periodic functions.
- Time Series Analysis:
    - Financial data, such as stock prices, often exhibit periodic patterns and seasonality. Fourier analysis can help in decomposing time series data into its frequency components, revealing underlying cyclic patterns.
    - By analyzing the frequency domain characteristics of financial data, traders and analysts can gain insights into cyclical behavior, trends, and recurring patterns that may impact pricing.

### How to handle outliers
- Transformation: log, square root, box-cox
- log: more agreesive on large values
- box-cox: less agreesive on large values
- log and square root: only work for positive values


## Model Specifics
...



