This is the second and last part of the project developed and submitted in August 2025 for the End-of-Course Assignment in Analysing Data For Business Success course at Republic Polytechnic.
We will build a churn prediction model using KNIME and evaluate its results.
You can find the [first part of the project here](https://cheeweeng.github.io/Data-Transformation-and-Visualization/).  

## Decision Tree Workflow  
<img width="702" height="206" alt="Image" src="https://github.com/user-attachments/assets/bc15be30-ba61-412e-87ba-30f48e086ab1" />

In KNIME, create this node sequence:
>  CSV Reader → Column Filter → Partitioning → Decision Tree Learner → Decision Tree Predictor → Scorer (JavaScript)

In the CSV Reader node, load the customer summary data created in the first part of the project.  

<p align="center">
  <img src="https://github.com/user-attachments/assets/c77139d5-62f2-4024-9a4e-0a4fa9a3baec" width="45%" />
  <img src="https://github.com/user-attachments/assets/67557794-9864-4dc4-97f4-49f449dacac0" width="45%" />
</p>

In Column Filter node, Customer ID is excluded. Keep Customer Age, Total_Purchases, Transaction_Count, Return_Rate, Churn.  
In Partitioning node, we keep 70% training and 30% testing. 

<p align="center">
  <img src="https://github.com/user-attachments/assets/f875cd9d-3071-438a-a92a-1cc0c789b174" width="45%" />
  <img src="https://github.com/user-attachments/assets/df2922cd-c6c6-4a14-aa3d-f2b18d8c67ae" width="45%" />
</p>

In Decision Tree Learner node, make sure Target column = Churn.  
In the Decision Tree Predictor node, adjust the "Maximum number of stored patterns" to 55,000 to fit in the dataset.  

## Confusion Matrix
<img width="1000" height="480" alt="Image" src="https://github.com/user-attachments/assets/eab2fec1-81f0-48a5-8b5d-7ae14a7a628e" />

The confusion matrix showed the model was strong in predicting class 0 (81%) but performed very poorly in predicting class 1 (19%).  
This is not a good classification performance and can even be dangerous if predicting Class 1 is important (e.g. fraud detection, medical diagnosis).
This is a result of class imbalance in the dataset as there are many more active customers (0) than churned customers (1) in the dataset.  

## Improved Workflow  

<img width="900" height="300" alt="Image" src="https://github.com/user-attachments/assets/e6833512-6a04-4634-8fbd-ff57fc4b71ad" />

To rebalance the dataset, we will deploy a SMOTE node and change Decision Tree mdoel to Random Forest. 

<img width="433" height="393" alt="Image" src="https://github.com/user-attachments/assets/25977e49-84b9-4703-b3ad-a29688b9b4a7" />

In the SMOTE node, target column is Churn and keep the default settings.

## Random Forest Confusion Matrix (with SMOTE node)  
scorer
Before balancing, the model was missing most of the Churners (Class 1).  After applying SMOTE, the model showed much improved performance from pre-SMOTE. For Class 1, there are 3806 True Positives (correctly predicted 1s) and 5106 False Negatives (model failed to predict churn when the actual was churned). With recall at 42%, the model still misses more than half of customers who are actually at risk of churning.  
The model is now better at identifying potential churners, but not perfect. We can still make actionable business recommendations to reduce churn, focusing on those correctly identified churners (TP = 3,806) and considering the missed churners (FN = 5,106).  

attribute imge
Out of the input variables considered by the Random Forest, Transaction_Count has the highest split count at level 2 among all features. This shows how many times a customer transact is the strongest predictor in the model.  
Followed closely as high influential features are Return_Rate and Avg_Order_Value.  

In summary, customer transaction frequency is the key driver of the model. Return behaviour and spending amount per order add significant predictive power.  

## Recommendations  
  1. Targeted campaign prioritized for the 43% correctly identify as churners to reduce the chance of them leaving.
  2. The variable importance in the attribute statistics showed certain behaviour correlates with customer churn. Since the Return rate was flagged as a strong predictor of the model, then the ecommerce company could conduct regular product quality audit as well as making product returns less of a pain point for the customers and providing exchanges and refunds in a hassle-free and fast process.

Back to [Projects portfolio](https://cheeweeng.github.io)
