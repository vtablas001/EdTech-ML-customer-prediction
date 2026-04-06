# EdTech Lead Conversion Prediction

![Status](https://img.shields.io/badge/Status-Completed-success.svg)

## Context
The EdTech industry has experienced immense growth over the past decade, a transformation heavily accelerated by the global disruptions of the Covid-19 pandemic. According to UNESCO (2020) in the report *National education responses to COVID-19: Summary report of UNESCO's online survey*, at the peak of the pandemic, remote learning became a necessary lifeline for over 1.5 billion students globally, permanently shifting consumer attitudes toward digital and distance education (p. 1). 

This momentum has carried into the post-pandemic era. The World Bank (2020), in the document *Reimagining human connections: Technology and innovation in education*, emphasizes that EdTech is no longer just a temporary stopgap but a core component for building resilient, personalized, and scalable educational systems worldwide (p. 8). Furthermore, the Inter-American Development Bank (IDB, 2021) highlights in its report *Education Technology in Latin America and the Caribbean* the critical role these platforms play in the modern labor market, noting that online education is essential for closing the global tech and digital skills gap through the continuous upskilling and reskilling of the professional workforce (p. 12). 

Driven by these macro trends, the Online Education market continues to expand rapidly, with forecasts projecting sustained compound annual growth rates (CAGR) exceeding 10%. However, this explosive growth has led to a highly competitive landscape. EdTech companies must leverage sophisticated digital marketing strategies to reach wide audiences, generating "leads"—individuals who show interest by browsing websites, downloading brochures, or interacting via email and social media. In this saturated market, the critical challenge for businesses is no longer just acquiring leads, but efficiently allocating resources and deploying data-driven strategies to convert those prospects into paid customers.

***

## Objective
An initial-stage startup offering cutting-edge technology programs, generates a large volume of leads daily. To optimize resource allocation, this project aims to:
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

### References
Inter-American Development Bank & HolonIQ. (2021). *Education Technology in Latin America and the Caribbean*. Washington, DC: IDB.
UNESCO. (2020). *National education responses to COVID-19: Summary report of UNESCO's online survey*. Paris: UNESCO.
World Bank. (2020). *Reimagining human connections: Technology and innovation in education at the World Bank*. Washington, DC: World Bank.
