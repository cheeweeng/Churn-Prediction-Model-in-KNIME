This is the second and last part of the project developed and submitted in August 2025 for the End-of-Course Assignment in Analysing Data For Business Success course at Republic Polytechnic.
We will build a churn prediction model using KNIME and evaluate its results.
You can find the [first part of the project here](https://cheeweeng.github.io/Data-Transformation-and-Visualization/).  

1
In KNIME, create this node sequence:
>  CSV Reader → Column Filter → Partitioning → Decision Tree Learner → Decision Tree Predictor → Scorer (JavaScript)

In the CSV Reader node, load the customer summary data created in the first part of the project.  

8 & 10
In Column Filter node, Customer ID is excluded. Keep Customer Age, Total_Purchases, Transaction_Count, Return_Rate, Churn
In Partitioning node, we keep 70% training and 30% testing. 

11 & 12
In Decision Tree Learner node, make sure Target column = Churn.  
In the Decision Tree Predictor node, adjust the "Maximum number of stored patterns" to 55,000 to fit in the dataset.  

13
The confusion matrix showed the model was strong in predicting class 0 (81%) but performed very poorly in predicting class 1 (19%).
This is a result of class imbalance in the dataset as there are many more active customers (0) than churned customers (1) in the dataset.  

## Improved Workflow  
To rebalance the dataset, we will deploy a SMOTE node and change Decision Tree mdoel to Random Forest. 

imp image
SMOTE
In the SMOTE node, target column is Churn and keep the default settings.



Back to [Projects portfolio](https://cheeweeng.github.io)
