![](../commonimages/workshop_logo.png)

# Lab: Assessing Credit Risk using Oracle Analytics

In this lab we will take the perspective of a **business user** (as opposed to the expert data scientist). 
Oracle Analytics lets business users build and apply ML models in a very visual and intuitive way. Oracle Analytics provides algorithms in all major ML categories, e.g. Regression, Classification, Clustering and Association Rule Mining.
In addition, there's a set of featured called "Augmented analytics" in this platform that uses ML "under the hood" to automate a lot of the common tasks in the analytics process, think about Data Preparation and Data Exploration.

## Objectives
- Become familiar with Oracle Analytics and self service analysis. 
- See how Oracle Analytics can be used to do Data Preparation and Exploration in a -visual- way, as an alternative to coding.
- Understand the impact of ML in the hands of business users.

# Prerequisites

You require the following: 
- An Oracle Cloud tenancy
- Either an Oracle Analytics Cloud instance **or** a local installation of Oracle Data Visualization Desktop. 

Please follow the [prerequisites](../prereq3/lab.md) first in case you don't have these yet.

# Data Preparation

First we have to upload the data that's required for our model. In this case, the dataset with historical Credit Risk information is mostly ready to go, without requiring any changes.

Download the dataset with the house prices and characteristics.
- Download [The training dataset](./data/MLTD2_german_credit_applications.csv)

Click on the link, then use the "Raw" button and then right click "Save As". Make sure to save these with extension CSV. Some browsers try to convert this to Excel format, which is incorrect.

The original dataset contains 1000 entries with 20 categorical and numerical attributes prepared by Professor Hofmann and each entry in the dataset represents a person who took a credit and classified as good or bad credit risk.
The dataset provided to you as part of the material was obtained from the following location: https://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)

The first task to do is to upload the MLTD2_german_credit_applicants.csv dataset provided to you into Oracle Analytics Cloud. You can find it [here](./data/MLTD2_german_credit_applicants.csv). 

- Open Data Visualization Desktop (or Oracle Analytics Cloud, if you prefer). On the top left corner click on the menu icon and Click on "Data".

![](./images/img2.jpg)

- To import the dataset click on "Create", "Data Set", and select the file that you downloaded earlier.

![](./images/img3.jpg)
![](./images/img4.jpg)

- You see a preview of the dataset. Complete the process by clicking "Add"
![](./images/img5.jpg)

- By default Oracle Analytics incorrectly treats the "recid" column as a measure. Change it to "Attribute" by clicking on "recid", then "treated as", then "attribute".
![](./images/img6.jpg)


- Oracle Analytics records all changes you make in a script. This allows it to easily repeat the process in case data is reloaded. For now, apply the script that has been created by clicking "Apply Script". This makes the change to recid effective.
![](./images/img7.jpg)


# Data Exploration

As you know, this phase in the Data Science process is for us to get to know our data, identify which columns are useful, detect any problems with the data, et cetera.

First of all, let's imagine you want to know how many credit applications have been Accepted vs Denied in the past. We can use Oracle Analytics' visualization capabilities for this.

- Create a project in order to investigate the dataset using visualizations by clicking on the burger menu associated with our dataset and "Select Project".
![](./images/img10.jpg)

- First we need a way to count the credit card applications. We do this as follows: Right-click on ‘My calculation’ folder of the dataset and select "Add Calculation".
![](./images/img11.jpg)

- The name of the field can be anything, e.g. "# Count". Then add a counter by Double-clicking on ‘Count’ in the ‘Aggregation’ list of options. 
![](./images/img12.jpg)

- Define the counter by selecting the column "recid", then click "Save".
![](./images/img13.jpg)

- Now we can find an answer to our questions. Select both the "class" and the "# Count" fields (use Control to select multiple fields). Then ‘Right-Click’ on the blue part and select "Pick Visualization". 
![](./images/img14.jpg)

- Select the ‘donut’ visualization
![](./images/img15.jpg)

- You see that 70% out of 1000 credit applications were good and 30% were bad for the target called ‘class’
![](./images/img16.jpg)

- Now let's say we have a NEW question. We'd like to know how the Credit Amount that's requested is related to to a Good or Bad credit scoring. Again, we can create a visualization to answer that question. This time, select the field "Recid", "Credit_amount" and "Class" and choose the "Boxplot" Visualization.
![](./images/img17.jpg)

- Now, you see ‘Boxplot Visualization’. You can the bulk of applications in terms Credit_amount for class=good and class=bad
It shows the bulk of credit_amounts for good and bad credit, the amount which are not in the bulk. My conclusion is that the range of credit_amount for bad credit is bigger than for good credit, although the average value seems the same.
![](./images/img19.jpg)

- Remember the colinearity issue from the previous labs? Colinearity is the effect of multiple attributes that supply similar information. When we train our model, we should try to only supply attributes that provide unique pieces of information. To investigate this issue, we will create a correlation diagram between the input features. Do this by selecting all the fields from "duration" until "num_dependants". Choose "Pick Visualization" and select "Correlation Matrix".
![](./images/img20.jpg)

- Now you see the correlation matrix visualization. Although there is some correlation between the fields, the correlation does not appear to be too high in any place. Therefore there's no colinearity and no action to be taken. 
![](./images/img23.jpg)
- Save the results of the Data Exploration. Give it a logical name.
![](./images/img25.jpg)

At the is point you are doing with the investigation of the dataset and move on the next task

# OAC Machine learning: Credit risk

In this section, you will carry out the following tasks using the point and click interface of Oracle Analytics Cloud for machine learning capability:

1.	Build a predictive model
2.	Evaluate the model
3.	Score the customer base using the model
4.	Predictions visualization

## 1.

![](./images/img26.jpg)

1.	Click on the burger menu  
2.	Click on ‘data’ in the menu

## 2.

![](./images/img27.jpg)

To define your data-flow to build a model using the ‘MLTD2_german_credit_applicants’  dataset:
1.	Click ‘Data-Flows’ tab

## 3.

![](./images/img28.jpg)

You have now to create a learning data-flow:

1.	Click on  ‘Create’
2.	Click on ‘Data-Flow’

## 4.

![](./images/img29.jpg)

To select the dataset to build the model:

1.	Select ‘MLTD2_german_credit_applicants’ dataset
2.	Click on ‘Add’

## 5.

![](./images/img30.jpg)

To select the attributes that will be considered by the machine learning algorithm:

1.	Click on ‘+’ next to the blue node
2.	Click on ‘Select Columns’

## 6.

![](./images/img31.jpg)

To remove unwanted attributes, either:
1.	Method 1:
A)	Click on ‘recid’
B)	Click on ‘Remove Selected’ to move it to left

Or 

2.	Method 2:
 Double-Click on ‘recid’ to move it to the left side
 
## 7.

![](./images/img32.jpg)

To select the machine learning technique to be used:

1.	Click on ‘+’ next to the last blue node
2.	Select ‘Train Binary Classifier’ group of algorithms since the class  only 2 values ‘good’ or ‘bad’ for credits

## 8.

![](./images/img33.jpg)

To specify the machine algorithm to be used:

1.	Select ‘Logistic Regression for model training’
2.	Click on ‘OK’

## 9.

![](./images/img34.jpg)

To define the target/class 

1.	Click on ‘select a column’
2.	Then ‘class’  column of your dataset as the target

## 10.

![](./images/img35.jpg)

1.	Make class  value is ‘bad’ corresponding to good credit applications
2.	Also notice the ‘Predict Value Threshold Value= 50 (0.5)’ 

## 11.

![](./images/img35.jpg)

To give the model a name:

1.	Click on ‘Save Model’ node
2.	Enter ‘MLTD2_trained_german_credit_LR50’ as the model name

## 12.

![](./images/img36.jpg)

To save the data-flow:

1.	Click on ‘Save’
2.	Enter ‘MLTD2_train_german_credit_DF’ as the name of the data-flow
3.	Click on ‘OK’

A message should appear saying that the data-flow is saved successfully

## 13.

![](./images/img37.jpg)

Once the data-flow was saved you can execute the data-flow:

1.	Click on ‘Run Data Flow’

## 14.

![](./images/img38.jpg)

A message will appear saying that the data flow was run successfully

## 15.

![](./images/img39.jpg)

To leave the data-flow:

1.	Click on the white back arrow


Now that you have built the model, you need to assess how good it is and decide if you are happy with it

# Model evaluation and refinement

## Oracle Analytics Cloud machine learning provides quality metrics to allow you to evaluate how god the trained models are.

## 1. 

![](./images/img40.jpg)

To go to your list of already trained models

1.	Click on the burger menu  
2.	Click on ‘Machine Learning’ in the menu

## 2. 

![](./images/img41.jpg)

To view the quality metrics associated with your model:

1.	Click on the model row to select it: ‘MLTD_trained_german_credit_LR50’
2.	Go to the end and click on the burger menu  
3.	Select ‘Inspect’

## 3. 

![](./images/img42.jpg)

To see the quality model metrics associated with your model:

1.	Click on ‘Quality’ to get to the model metrics

Now, you see the model quality metrics associated with your trained model.  Several model metrics Now the question is can we improve the model to reduce the number of bad credits to avoid complications and money.

This is exactly what you will do next.
When finished then 

1.	Click on ‘Close’

## 4. 

![](./images/img43.jpg)

Now the model metrics analysis is done of logistic regression model with threshold=50 (0.5)
Let’s see if changing the threshold has some effect on the model results

## 5. 

![](./images/img44.jpg)

1.	Click on the burger menu  
1.	Click on ‘Data’ in the main menu

## 6. 

![](./images/img45.jpg)

1.	Select ‘Data-flow’ Tab
2.	Click on your model data-flow to open it: ‘MLTD2_train_german_credit_DF’

## 7. 

![](./images/img46.jpg)

1.	Set ‘Predict Value Threshold % = 30

2.	Click on ‘Save’ and wait the green message to appear saying that it has been saved successfully

3.	Click on ‘Run data Flow’ and wait until you see the green message saying the it has been run successfully

## 8. 

![](./images/img47.jpg)

With certain machine learning techniques, It is often recommended to standardize the numerical columns:

1.	Make sure to set ‘Standardization = True’

This is avoid the domination of attributes with large spread over attributes with much smaller spread

## 9. 

![](./images/img48.jpg)

2.	Type in ‘MLTD2_trained_german_credit_LR30’

3.	Click on ‘Save’ and wait the green message to appear saying that it has been saved successfully

4.	Click on ‘Run data Flow’ and wait until you see the green message saying the it has been run successfully

## 10. 

![](./images/img49.jpg)

To go back and check the model quality metrics for the logistic regression  with threshold 30 % :

1.	Click on the burger menu

2.	Click on ‘Machine Learning’ in the menu

## 11. 

![](./images/img50.jpg)

Select the model to inspect:

1.	Click on the raw for ‘MLTD2_trained_german_credit_LR30’

2.	Click on the burger menu 

3.	Click on ‘Inspect’

## 12. 

![](./images/img51.jpg)

To access the model quality metrics:

1.	Click on ‘Quality’ 

Now you can see that for logistic regression threshold value= 0.3 then more bad credit have been captured but that also increased the number good credit being classified as bad= > it is compromise

Domain experts need to make the decision for a good compromise between what is acceptable or not.

2.	Click on ‘Close’ to leave this window.

## 13. 

![](./images/img52.jpg)

You are now done with the model assessment! :) 


Now that you have built the model for the mltd2_german_credits_applicants and refined it based the evaluation of the model quality metrics then the next step is to score the customer credit applications. 

# Apply model data-flow '
## In this section, you create s second Data Flow where the model created in the first step gets is applied to score the customer credit applications.

## 1. 

![](./images/img53.jpg)

To define your data-flow to score current credit applications using the model you have built recently:

1.	Click on the burger menu  

2.	Click on ‘Data’ in the main menu

## 2. 

![](./images/img54.jpg)

1.	Click ‘Data-Flows’ tab

## 3. 

![](./images/img55.jpg)

You now have to create a model scoring data-flow:

1.	Click on  ‘Create’

2.	Click on ‘Data-Flow’

## 4. 

![](./images/img56.jpg)

To select the dataset to apply the model:

1	Select ‘MLTD2_german_credit_applicants’ dataset

2	Click on ‘Add’

## 5. 

![](./images/img57.jpg)

1.	Click on the ‘+’ sign next to the last blue node.

2.	Select ‘Select Columns’ as the node to add to data-flow

## 6. 

![](./images/img58.jpg)

To remove unwanted attributes:

A)	Click on ‘class’

B) 	Click on ‘Remove Selected’ to move it to left

Or 

1.	Double-Click on ‘recid’ to move it to the left side

## 7. 

![](./images/img59.jpg)

You now have to specify which model to use: 

1.	Click on the ‘+’ of last node in the data-flow

2.	Select ‘Apply Model’ node

## 8. 

![](./images/img60.jpg)

Select the trained model you did earlier:

1.	Select ‘MLTD2_trained-german_credit_LR30’ that provided  better results

2.	Click on ‘OK’

## 9. 

![](./images/img61.jpg)

You have to add a node to specify which columns to include the final dataset:

1.	Click on the ‘+’ of the last node in the data-flow

2.	Select  ‘Select Columns’ node

## 10. 

![](./images/img62.jpg)

You need to remove unwanted to keep. You will remove all attributes except:
 
•	Recid

•	PredicteValue

•	PredictionConfidence 

Either by

1.	Double clicking on each attribute not listed above

Or

2.	First you have to select the columns:

A)	Using ‘Shift + Click’ on attribute ‘checking_status’

B)	Using ‘Shift + Click’ on attribute ‘foreign_worker’

C)	To move the selected attributes to the left side then either:
 
- 	Click on ‘Remove selected’
- 	Or Double click on the green

## 11. 

![](./images/img63.jpg)

You should end-up with only 3 columns kept on the left hand side:

•	Recid

•	PredicteValue

•	PredictionConfidence

## 12. 

![](./images/img64.jpg)

Now to specify the table to be saved:

1.	Click on the ‘+’ of the last node in the data-flow

2.	Select ‘Save Data’ node

## 13. 

![](./images/img65.jpg)

Set the name of the output dataset to be saved:

1.	Click on ‘Save Data’ node

2.	Set name to ‘MLTD2_Greman_credit_scored’

## 14. 

![](./images/img66.jpg)

You have to save the data-flow:

1.	Set the name of the data flow to ‘MLTD2_scoring_germany_credits_DF’

2.	Click on ‘OK’

3.	Click on ‘save’. You will get a successful message in green

## 15. 

![](./images/img67.jpg)

Now you can run the data-flow:

1.	Click on ‘Run Data Flow’

2.	Once the execution is finished you will see a successful message in green

## 16. 

![](./images/img68.jpg)

To exit the data-flow:

1.	Click on the white back arrow

## 17. 

![](./images/img69.jpg)

You now see your newly created data-flow listed in the repository

## 18. 

![](./images/img70.jpg)

You now see the newly created dataset in the repository list of available datasets

## 19. 

![](./images/img71.jpg)

Now, in order to go back to your current project and create visualization based on the scored data set then 

1.	Click on the burger menu

2.	Click on ‘Catalog’


Now, you are finished with apply model data-flow that creates a scored table for the current credit application. In the next section, you will explore the results visually.

# Credit Prediction Visualization 
## In this section, using the scored table of the previous exercize, you create 3 visuals to understand the predicted values according to some applicants attributes.

## 1. 

![](./images/img72.jpg)

Now, in order to go back to your current project and create visualization based on the cored data set then 

1.	Click on the burger menu

2.	Click on ‘Catalog’

## 2. 

![](./images/img73.jpg)

To open your current project:

1.	Click on the burger menu for the project in left right corner

2.	Click on ‘Open’

## 3. 

![](./images/img74.jpg)

To add a new canvas

1.	Click on the ‘+’ of the credit exploration canvas

## 4. 

![](./images/img75.jpg)

To name the new canvas:

1.	Click on the down arrow associated with the ‘Canvas 2’ name.

2.	Click on ‘Rename’

## 5. 

![](./images/img76.jpg)

1.	Type in ‘Prediction analysis’ as the new name

2.	Click on the check mark sign next to the new name, bottom of the canvas. 

## 6. 

![](./images/img77.jpg)

Now to create visualizations, you have to add the data set:

1.	Click on the ‘+’

2.	Select ‘Add Data Set…’

## 7. 

![](./images/img78.jpg)

To add the correct dataset to the project, the dataset containing the scored credit applications:

1.	Click on ‘MLTD2_german_credit_scored’

2.	Click on ‘Add to Project’

## 8. 

![](./images/img79.jpg)

1.	Click ‘measure’ to change ít to ‘Attribute’ so that it corresponds to the one in the other dataset

## 9. 

![](./images/img80.jpg)

You have to link the 2 dataset to create visualization on attributes from both:

1.	Click on ‘Prepare’ tab

## 10. 

![](./images/img81.jpg)

1.	Click on ‘Data diagram’ canvas

## 11. 

![](./images/img82.jpg)

2.	Click on the first dataset to select it

3.	Click on the "0" between the 2 datasets to define the link between the two

## 12. 

![](./images/img83.jpg)

1.	Click on ‘Add Another Match’

## 13. 

![](./images/img84.jpg)

1.	Select ‘recid’ for both

2.	Click on ‘OK’

## 14. 

![](./images/img85.jpg)

To go back to visualization tab:

1.	Click ‘Visualize’

## 15. 

![](./images/img86.jpg)

To create a visualization for the predicted value distribution:

1.	‘Ctrl + left click’ to select

A)	‘Predcitedvalue’ and

B)	 ‘# Count’

## 16. 

![](./images/img87.jpg)

1.	Select the ‘Donut’ visualization

## 17. 

![](./images/img88.jpg)

Now, you see the % of good and bad predicted values

## 18. 

![](./images/img89.jpg)

To create a second visual to see the predicted value according to employment length of time:

1.	‘Crtl + left click’ to select:

A)	‘Employment’

B)	‘Predictedvalue’

C)	‘# Count’

2.	Select ‘Pick visualization’

## 19. 

![](./images/img90.jpg)

As for selecting the visual:

1.	Select the ‘Bar’ visual option

## 20. 

![](./images/img91.jpg)

Now, you the predicted value according to employment duration.

It seems that people with employment duration of 1 year or less are high risk people

## 21. 

![](./images/img92.jpg)

To create a visual to look at predicted value according personal status:

1.	‘Crtl + left click’ to select 

A)	‘# Count’

B)	PredictedValue

C)	Persona_status

2.	Select ‘Pick Visualization’

## 22. 

![](./images/img93.jpg)

This time for visualization:

1.	Select ‘Stacked Bar’ visual option

## 23. 

![](./images/img94.jpg)

This is what you should see.

## 24. 

![](./images/img95.jpg)

To save the work so far:

1.	Click on ‘save’ and wait until the a successful green message appears

## 25. 

![](./images/img96.jpg)

Now that you are done and exit the project:

1.	Click the white back arrow 


Congratulations, you are now finished with the lab. 