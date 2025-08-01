# PROJECT TITLE 
**Customer Churn Prediction Model**

## NON-TECHNICAL EXPLANATION OF YOUR PROJECT
This project uses smart technology to identify customers most likely to leave our telecom service. By focusing on those at risk, we can offer personalized support and retain them, saving costs compared to finding new customers. We carefully chose the KNN model because it excels at detecting potential churners accurately while minimizing unnecessary offers to loyal customers. This balance helps protect our revenue and strengthens customer loyalty. Adopting this predictive model means smarter decisions, better resource use, and a stronger business. Your support ensures we keep our customers happy and our company thriving.

## DATA
**1-Summary of Customer Churn Dataset**
The dataset contains 7,043 customer records from a synthetic dataset simulating a U.S. telecommunications company, originally generated by IBM Analytics and released via an IBM community blog around 2018. Each record represents a unique billing account at a specific snapshot in time, with no explicit date field but tenure data indicating up to 72 months of customer history. The dataset is synthetic, with values simulated or perturbed to remove personally identifiable information, eliminating the need for direct consent.

**2-Features: The dataset includes 21 features:**
Numerical (3): 
tenure: Number of months with the company (integer).
MonthlyCharges: Current monthly fee (float).
TotalCharges: Lifetime spend (float), with 11 missing values where tenure = 0.
Categorical/Binary (18): Includes customerID, gender, SeniorCitizen, Partner, Dependents, PhoneService, MultipleLines, InternetService, OnlineSecurity, OnlineBackup, DeviceProtection, TechSupport, StreamingTV, StreamingMovies, Contract, PaperlessBilling, PaymentMethod, and Churn (target variable).
Sensitive Attributes: gender and SeniorCitizen (age proxy) could be considered legally protected classes.

**3-Class Balance: The target variable Churn is imbalanced:**
Churn = "Yes": 1,869 records (26.5%).
Churn = "No": 5,174 records (73.5%).

**4-Collection Process:**
Source: Generated by IBM Analytics, mimicking a U.S. telco schema.
Sampling Strategy: Likely convenience sampling to reflect realistic churn rates, though details are undisclosed.
Privacy: As the data is synthetic, no personal data or consent is involved.

**5-Citation:** IBM Analytics, IBM Community Blog, c. 2018.

## MODEL 
I've chosen the K-Nearest Neighbors (KNN) model for predicting customer churn based on its superior performance among evaluated algorithms, which included Logistic Regression, Decision Tree, Random Forest, Support Vector Classifier, and Gradient Boosting. The decision was driven by:
	- Highest Recall Score: KNN excelled at detecting most churners, ensuring minimal missed opportunities to retain customers.
	- Balanced Error Rates: It effectively minimized both false positives (reducing wasted retention incentives) and false negatives (avoiding overlooked churners).
	- Competitive Performance: KNN provided efficient resource allocation, making it a practical choice for optimizing churn prediction.

This selection aligns with the dataset's characteristics, such as its imbalanced churn distribution (26.5% "Yes" vs. 73.5% "No"), as described in the provided data summary from IBM Analytics (c. 2018).

## HYPERPARAMETER OPTIMSATION
KNN Hyperparameters and Optimization
# Hyperparameters:
n_neighbors: Number of neighbors ([3, 5, 7, 9, 11]).
weights: Neighbor contribution method (['uniform', 'distance']).

# Optimization:
Used GridSearchCV with 5-fold cross-validation to test all combinations.
Optimized for recall to maximize churner detection.
Selected the best n_neighbors and weights based on highest average recall.

# Why:
Recall focus ensures most churners are caught, per model selection goals.
n_neighbors range suits dataset size (7,043 records); weights tests equal vs. distance-based influence.
Cross-validation prevents overfitting.

# Outcome:
If KNN had the highest default recall, the tuned model used optimal parameters.
Evaluated on test set for recall, ROC AUC, and confusion matrix.

## RESULTS
# 1-Default Model Performance:
Logistic Regression: Time: 0.1067s, ROC AUC: 0.8419, Recall: 0.5588
Decision Tree: Time: 0.0338s, ROC AUC: 0.6573, Recall: 0.5053
KNN: Time: ~0s, ROC AUC: 0.7899, Recall: 0.5749 (highest, best recall model)
Random Forest: Time: 0.8208s, ROC AUC: 0.8164, Recall: 0.4759
SVC: Time: 6.6919s, ROC AUC: 0.7905, Recall: 0.4840
Gradient Boosting: Time: 0.9787s, ROC AUC: 0.8432 (highest), Recall: 0.5241

# 2-Tuning Results:
**KNN (Best Recall Model):**
Best Parameters: n_neighbors=11, weights='uniform'
Tuning Time: 5.8820s
Optimized for recall using GridSearchCV, aligning with the goal of maximizing churner detection.

**Gradient Boosting (Best ROC AUC Model):**
Best Parameters: learning_rate=0.1, max_depth=7, n_estimators=50
Tuning Time: 262.8054s
Not selected, as recall was prioritized over ROC AUC.

# 3-Why KNN?
Highest Recall (0.5749): KNN outperformed other models in detecting churners, crucial for minimizing missed retention opportunities.
Tuned Performance: Using n_neighbors=11 and weights='uniform', KNN likely improved recall further, balancing false positives and negatives for efficient resource allocation, as per the model selection rationale.

Conclusion: KNN was selected for its superior recall, optimized via GridSearchCV to enhance churn detection on the imbalanced dataset (26.5% churners).

For screenshots of the results, please refer to the Jupyter Notebook.

## CONTACT DETAILS
For inquiries, incidents, or retraining requests, contact: sabri.bensaber@gmail.com 

