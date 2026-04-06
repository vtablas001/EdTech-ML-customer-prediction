# EdTech Lead Conversion Prediction

![Status](https://img.shields.io/badge/Status-Completed-success.svg)

## Context
The EdTech industry has experienced immense growth over the past decade, heavily accelerated by the Covid-19 pandemic. With a compound annual growth rate (CAGR) of 10.26%, the market is highly competitive. EdTech companies leverage digital marketing to reach wide audiences, generating "leads"—individuals who show interest by browsing the website, downloading brochures, or interacting via email and social media. The critical challenge is efficiently nurturing these leads and converting them into paid customers.

## Objective
ExtraaLearn, an initial-stage startup offering cutting-edge technology programs, generates a large volume of leads daily. To optimize resource allocation, this project aims to:
1. Analyze and build a Machine Learning model to identify which leads are most likely to convert to paid customers.
2. Uncover the underlying factors driving the lead conversion process.
3. Create a data-driven profile of high-probability leads to inform marketing and sales strategies.

## Tech Stack
* **Language:** ![Python](https://img.shields.io/badge/python-3670A0?style=flat&logo=python&logoColor=ffdd54)
* **Data Manipulation:** ![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=flat&logo=pandas&logoColor=white) ![NumPy](https://img.shields.io/badge/numpy-%23013243.svg?style=flat&logo=numpy&logoColor=white)
* **Data Visualization:** ![Matplotlib](https://img.shields.io/badge/Matplotlib-%23ffffff.svg?style=flat&logo=Matplotlib&logoColor=black) ![Seaborn](https://img.shields.io/badge/Seaborn-blue?style=flat&logo=python&logoColor=white)
* **Machine Learning Dependencies:** ![scikit-learn](https://img.shields.io/badge/scikit--learn-%23F7931E.svg?style=flat&logo=scikit-learn&logoColor=white)

## Data Overview
The dataset consists of 4,612 records and 15 variables with no missing values. It captures demographic data, engagement metrics, and interaction history.

* **Target Variable:** `status` (1 = Converted to paid customer, 0 = Not Converted)
* **Key Features:** `age`, `current_occupation`, `first_interaction`, `profile_completed`, `website_visits`, `time_spent_on_website`, `page_views_per_visit`, `last_activity`.

## Methodology
1. **Exploratory Data Analysis (EDA):** Analyzed distributions, checked for skewness, and evaluated feature correlations. 
2. **Data Preprocessing:** Handled categorical encoding using dummy variables. No scaling was applied as tree-based models rely on vector space splits rather than distance metrics.
3. **Model Building:** * Baseline Decision Tree Classifier.
    * Cost Complexity Pruning (ccp_alpha) to control tree depth and overfitting.
    * Random Forest Classifier with Hyperparameter Tuning via GridSearchCV.
4. **Evaluation:** Prioritized **Recall for Class 1 (Converted)**. In a business context, missing an actual conversion (False Negative) represents lost revenue, making Recall the most critical metric for this specific problem.

## Key Insights from EDA
* **Website Engagement is Crucial:** `time_spent_on_website` and `website_visits` are highly right-skewed but represent genuine user behavior. These engagement metrics are the strongest predictors of conversion.
* **Demographics:** 56.7% of the leads are professionals. Professionals and unemployed individuals (likely job-seeking professionals) show a higher propensity to convert compared to full-time students.
* **Interaction Channels:** Over 55% of users first interacted via the website. Leads whose last activity was digital (email or website) converted at higher rates than those contacted via phone.
* **Marketing Channels:** Traditional print media and broad digital ads had negligible correlation with lead conversion.

## Modeling and Performance
### 1. Pruned Decision Tree
* **Training Accuracy:** 91% | **Test Accuracy:** 83%
* **Test Recall (Class 1):** 73%
* **Insight:** The tree structure revealed that if a prospect's first interaction is through the website and they spend more than 414 seconds (6.9 minutes) navigating, the probability of conversion spikes significantly.

### 2. Tuned Random Forest Classifier
* **Training Accuracy:** 95% | **Test Accuracy:** 85%
* **Test Recall (Class 1):** 79% (Improved via balanced class weights and grid search)
* **Insight:** While the Random Forest provided a more robust and generalized prediction, it confirmed the feature importance findings from the Decision Tree: `time_spent_on_website`, `first_interaction_Website`, and `profile_completed` are the primary drivers of success.

## Actionable Recommendations
1. **Focus on Website Engagement:** Leads spending > 6.9 minutes on the platform are highly likely to convert. Implement strategies to increase dwell time, such as interactive content, free trial modules, or gamified onboarding.
2. **Prioritize Professional Leads:** Tailor marketing copy to highlight career growth, upskilling, and immediate ROI to resonate with the professional and job-seeking demographics.
3. **Optimize the Digital Funnel:** Shift budget away from low-performing print media. Invest in optimizing the website's user experience (UX) and email nurturing campaigns, as these channels demonstrably close more sales than phone calls.
4. **Implement Lead Scoring:** Use the model's probabilities to rank incoming leads. Sales representatives should immediately prioritize individuals who have high website engagement and medium-to-high profile completion.
