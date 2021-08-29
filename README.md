# Credit Line Increase Model Card

### Basic Information

* **Person or organization developing model**: Jiaqi Bai, `jiaqi_bai@gwu.edu`
* **Model date**: August, 2021
* **Model version**: 1.0
* **License**: MIT
* **Model implementation code**: [project.ipynb](project.ipynb)

### Intended Use
* **Primary intended uses**: This model is an *example* probability of default classifier, with an *example* use case for determining eligibility for a credit line increase.
* **Primary intended users**: Students in GWU DNSC 6301 bootcamp.
* **Out-of-scope use cases**: Any use beyond an educational example is out-of-scope.

### Training Data

* Data dictionary: 

| Name | Modeling Role | Measurement Level| Description|
| ---- | ------------- | ---------------- | ---------- |
|**ID**| ID | int | unique row indentifier |
| **LIMIT_BAL** | input | float | amount of previously awarded credit |
| **SEX** | demographic information | int | 1 = male; 2 = female |
| **RACE** | demographic information | int | 1 = hispanic; 2 = black; 3 = white; 4 = asian |
| **EDUCATION** | demographic information | int | 1 = graduate school; 2 = university; 3 = high school; 4 = others |
| **MARRIAGE** | demographic information | int | 1 = married; 2 = single; 3 = others |
| **AGE** | demographic information | int | age in years |
| **PAY_0, PAY_2 - PAY_6** | inputs | int | history of past payment; PAY_0 = the repayment status in September, 2005; PAY_2 = the repayment status in August, 2005; ...; PAY_6 = the repayment status in April, 2005. The measurement scale for the repayment status is: -1 = pay duly; 1 = payment delay for one month; 2 = payment delay for two months; ...; 8 = payment delay for eight months; 9 = payment delay for nine months and above |
| **BILL_AMT1 - BILL_AMT6** | inputs | float | amount of bill statement; BILL_AMNT1 = amount of bill statement in September, 2005; BILL_AMT2 = amount of bill statement in August, 2005; ...; BILL_AMT6 = amount of bill statement in April, 2005 |
| **PAY_AMT1 - PAY_AMT6** | inputs | float | amount of previous payment; PAY_AMT1 = amount paid in September, 2005; PAY_AMT2 = amount paid in August, 2005; ...; PAY_AMT6 = amount paid in April, 2005 |
| **DELINQ_NEXT**| target | int | whether a customer's next payment is delinquent (late), 1 = late; 0 = on-time |

* **Source of training data**: GWU Blackboard, email `jphall@gwu.edu` for more information
* **How training data was divided into training and validation data**: 50% training, 25% validation, 25% test
* **Number of rows in training and validation data**:
  * Training rows: 15,000
  * Validation rows: 7,500

### Test Data
* **Source of test data**: GWU Blackboard, please email my professor's address `jphall@gwu.edu` for more information
* **Number of rows in test data**: 7,500
* **State any differences in columns between training and test data**: None. They have the same columns but have different rows


### Model details
* **Columns used as inputs in the final model**:19
* **Column(s) used as target(s) in the final model**: 1
* **Type of model**: Dictionary
* **Software used to implement the model**: Python, doing it on the google colab
* **Version of the modeling software**: 0.22.2.post1
* **Hyperparameters or other settings of your model**: ccp_alpha=0.0, class_weight=None, criterion='gini',
                       max_depth=6, max_features=None, max_leaf_nodes=None,
                       min_impurity_decrease=0.0, min_impurity_split=None,
                       min_samples_leaf=1, min_samples_split=2,
                       min_weight_fraction_leaf=0.0, presort='deprecated',
                       random_state=12345, splitter='best'
### Quantitative analysis
* **Metrics used to evaluate your final model**: 
When validation AUC becomes max, training AUC becomes higher, accuracy_score becomes higher, and Hispanic-to-White AIR is greater than 0.8, the model is suitable. 
* **State the final values of the metrics for all data: training, validation, and test data**:

| Data type | AUC | accuracy score when cutoff is 0.15|
| ---- | ------------- | ---------------- |
| Training data |  0.7837 | 0.6482 |
| Validation data | 0.7496 | 0.6321 |
| Test data | 0.7438 | 0.6341 |
 
Hispanic-to-White AIR: 0.833205
* **Provide any plots related to your data or final model -- be sure to label the plots!**:

![Histograms](https://github.com/Mystery6/6301project/blob/main/image/Histograms.png)
![Heat map](https://github.com/Mystery6/6301project/blob/main/image/Heat_map.png)
![Iteration Plot](https://github.com/Mystery6/6301project/blob/main/image/Iteration_plot.png)

<p align="center">Decision Tree</p>

![Decision Tree](https://github.com/Mystery6/6301project/blob/main/image/Decision_tree.png)


![Variable Importance](https://github.com/Mystery6/6301project/blob/main/image/Variable_Importance.png)

![Adjust Iteration Plot](https://github.com/Mystery6/6301project/blob/main/image/Adjust_Iteration_plot.png)

### Ethical considerations
* **Describe potential negative impacts of using your model**:
* ■ Math or software problems: 
* ■ Real-world risks: who, what, when or how
* **Describe potential uncertainties relating to the impacts of using your model**:
* ■ Math or software problems:
* ■ Real-world risks: who, what, when or how?
* **Describe any unexpected or results**:
