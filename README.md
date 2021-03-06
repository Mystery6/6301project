# Credit Line Increase Model Card

### Basic Information

* **Person or organization developing model**: Jiaqi Bai, `jiaqi_bai@gwu.edu`
* **Model date**: August, 2021
* **Model version**: 1.0
* **License**: MIT
* **Model implementation code**: [project.ipynb](project.ipynb)

### Intended Use
* **Primary intended uses**: This model is an *example* probability of default classifier, with an *example* use case for determining eligibility for a credit line increase. It can predict whether people in the data will pay the bill on time (education only).
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

* **Source of training data**: GWU Blackboard, please email my professor's address `jphall@gwu.edu` for more information
* **How training data was divided into training and validation data**: 50% training, 25% validation, 25% test
* **Number of rows in training and validation data**:
  * Training rows: 15,000
  * Validation rows: 7,500

### Test Data
* **Source of test data**: GWU Blackboard, please email my professor's address `jphall@gwu.edu` for more information
* **Number of rows in test data**: 7,500
* **State any differences in columns between training and test data**: None. They have the same columns but have different rows


### Model details
* **Columns used as inputs in the final model**: There are 19 columns. The columns are 'amount of previously awarded credit', 'history of past payment', 'amount of previous payment', and 'amount of bill statement'. Detailed names are 'LIMIT_BAL', 'PAY_0', 'PAY_2', 'PAY_3', 'PAY_4', 'PAY_5', 'PAY_6', 'BILL_AMT1', 'BILL_AMT2', 'BILL_AMT3', 'BILL_AMT4', 'BILL_AMT5', 'BILL_AMT6', 'PAY_AMT1', 'PAY_AMT2', 'PAY_AMT3', 'PAY_AMT4', 'PAY_AMT5', 'PAY_AMT6'.
* **Column(s) used as target(s) in the final model**: There is 1 column, which is 'DELINQ_NEXT'. 'DELINQ_NEXT' means whether a customer's next payment is delinquent (late), when 'DELINQ_NEXT' = 1 means late and when 'DELINQ_NEXT' = 0 means on-time 
* **Type of model**: Decision Tree
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
When validation AUC becomes max, training AUC becomes higher, accuracy_score becomes higher, and all AIR in validation data is greater than 0.8, the model is suitable. 
* **State the final values of the metrics for all data: training, validation, and test data**:


| Data type | AUC |Accuracy score when cutoff is 0.18|
|:--:|:--:|:--:|
| Training data |  0.7837 | 0.7567 |
| Validation data | 0.7496 | 0.7384 |
| Test data | 0.7438 | 0.7461 |
 

The min AIR: 0.8332>0.8. Then all AIR in validation data is greater than 0.8.

* **Provide any plots related to your data or final model -- be sure to label the plots!**:

<p align="center">
<img width="700" src="https://github.com/Mystery6/6301project/blob/main/image/Histograms.png">
<img width="700" src="https://github.com/Mystery6/6301project/blob/main/image/Heat_map.png">
<img width="500" src="https://github.com/Mystery6/6301project/blob/main/image/Iteration_plot.png">
</p>

<p align="center">Decision Tree</p>

<p align="center">
<img src="https://github.com/Mystery6/6301project/blob/main/image/Decision_tree.png">
<img width="600" src="https://github.com/Mystery6/6301project/blob/main/image/Variable_Importance.png">
<img width="500" src="https://github.com/Mystery6/6301project/blob/main/image/Adjusted_Iteration_plot.png">
</p>

### Ethical considerations
* **Describe potential negative impacts of using your model**:

* ??? Math or software problems: 

1. The model may be over-fitted. Perform well in training data, but not real data.
2. For the accuracy score, although when setting higher cutoff, the accuracy score will increase, the problem is higher cutoff means lending more money, so the risk of a big deliquent also increases.
3. Each decision boundary involves only a single feature. So sometimes the efficiency may not be that high. 
4. There are many hyper-parameters to tune. But there is no regression coefficients, standard errors or confidence, which will be useful to test the validity of the model.
5. Single decision trees can be unstable.
6. Due to the greedy nature of splitting criterion, interacting features that can distinguish between classes together but not individually may be passed over in favor of other features that are less powerful.
7. Some varibles may have a close relationship like amount of bill and history payment. If the amount of bill is big, their delayment may be longer. The model may ignore these problem of multicolinearity.
8. If given a useless variable, which has a clear trend like temperature. When getting into summer, the temperature will increase, but it may not have any impact for people behavior. But from the model, it may use this as a classified principle, which may influence the low accuracy in the real data.

* ??? Real-world risks:
1. Model is based on the previous behavior and data. It cannot reflect the latest status of people. Once someone suddenly get rich with bad behavior before, he or she is more likely to be regarded as delinquent from the model. However, the real result is more likely to be pay on time based on his or her wealth now. On the other hand, once someone always paid on time from the former experience, but maybe someday he or she has problem on finance or even decides to cheat the bank. The model cannot reflect their latest situation and their thoughts now. So it will bring negative impact of the bank on losing the high quality of customers and has risks of being cheated by other 'on time' customers.
2. The marriage and education are not as stable as the gender or race. But when the model predicts their behavior next time, these variables are changed in this period. These changes may influence the results of the model, so when adding these changes, the predicted result may be different. However, the csv file is confirmed. Maybe someone gets his or her PhD right now, he is not willing to let other blame him on the delinquent or maybe he or she gets a good job and have the ability to pay on time. So the model cannot update these changes directly and reflect their influence.
3. When we measured AIR and tried to improve AIR by changing the cutoff, from the model, we change the cutoff from 0.15 to 0.18, we were attempting to ensure Black and Hispanic customers would receive more loans. The result show the AIR increases, which means our remediation tactics worked, but only to a small degree. Black and Hispanic AIR was still less than 1, which means there is still some kind of racial bias in the model. So, people should be careful when using this model in the future as it still has some racial bias.

* **Describe potential uncertainties relating to the impacts of using your model**:

* ??? Math or software problems: 
1. The model may perform well with huge data, but when the amount of data is small, the model may have much error.
2. The model requires the depth of the model to be set as a suitable value. If the depth is set by 5, then we cannot find the best 6. So to prevent the local optima, the depth should be set in a little big value to get the global optima.
* ??? Real-world risks: 
1. For the initial card holder who have no former records, I cannot predict correctly whether they will pay on time or delinquent from the model. As they do not have the data like pay_0. So, the model may not fits well for these people.
2. It will bring the privilege or prejudice of others. For these regarded as 'on time', they will get more benefits not only from the bank. Once they are trying to apply for school or hunt a job, if these data is exposed to the interviewers, they may have a first impression about these people without meeting them. This first impression is not easy to be changed and more likely to influence the results. Needless to say, 'on time' is better than 'delinquent' from many people's view. But it cannot reflect the status and quality now. So with these privilege or prejudice in advance, it is not fair for the people in an interview.
3. About the decision model, this kind of model may offer a reference for the final decision, but on the importatnt thing, like detecting crime, this thing cannot be only determined by the former record. As when someone has had a crime, he or she may be regarded as criming again for the rest of life. But they may not have a crime again. Besides, for those people who has the first crime, the model cannot detect their bad behaviors because they have no record for criminal, so they may not be regarded as the criminal.


* **Describe any unexpected or results**:

This model performs well after 6 iterations. 
The results of the first model are following:


| Data type | AUC |
| ---- | ------------- | 
| Training data |  0.7693 |
| Validation data | 0.7425 | 


The standard deviation of the model is 0.0199. **The hispanic-to-white AIR is 0.76, which is problematic and lower than 0.8**. So I adjust the model.

When cutoff is 0.18, the results of adjusted model are following:

| Data type | AUC | Accuracy score when cutoff is 0.18|
|:--:|:--:|:--:|
| Training data |  0.7837 | 0.7567 |
| Validation data | 0.7496 | 0.7384 |
| Test data | 0.7438 | 0.7461 |

The standard deviation of the model is 0.0177. **And the min AIR: 0.8332>0.8. All the AIR is greater than 0.8, which is pretty good. It shows the bidas remediation is effective.**


Considered the cutoff is 0.18, the validation AUC is max at that time, the accuracy of the test data is 0.7461, and the AUC of test data is 0.7438. So the model is pretty good.

Question: 
1. I would like to know how to predict the 'on time' or 'delinquent' of initial credit card holder. 
2. I search on the internet for a long time but cannot find a way to put my form in the center of the page.

**In all, I learn a lot from your course and it really arouses my interest to dig deeper in this field. I have no other group members but I still made it. I am proud of myself. Last but not least, sincerely thank you for your dedication and hope to be someone professional and friednly as you.**

