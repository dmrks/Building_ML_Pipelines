# Building_ML_Pipelines

In this project, we will be using a dataset containing bone marrow transplantation characteristics for pediatric patients from UCI’s Machine Learning Repository.

We will this dataset to build a pipeline, containing all preprocessing and data cleaning steps, and then selecting the best classifier to predict patient survival.

Let’s get started!


# Investigate the data

1.
The dataset has been loaded for you in script.py and saved as a dataframe named df. Some of the input and output features of interest are:

donor_age - Age of the donor at the time of hematopoietic stem cells apheresis
donor_age_below_35 - Is donor age less than 35 (yes, no)
donor_ABO - ABO blood group of the donor of hematopoietic stem cells (0, A, B, AB)
donor_CMV - Presence of cytomegalovirus infection in the donor of hematopoietic stem cells prior to transplantation (present, absent)
recipient_age - Age of the recipient of hematopoietic stem cells at the time of transplantation
recipient_age_below_10 - Is recipient age below 10 (yes, no)
recipient_age_int - Age of the recipient discretized to intervals (0,5], (5, 10], (10, 20]
recipient_gender - Gender of the recipient (female, male)
recipient_body_mass - Body mass of the recipient of hematopoietic stem cells at the time of the transplantation
…
survival_status - Survival status (0 - alive, 1 - dead)
We will build a classification pipeline to predict the survival status. As part of the pipeline, we will process the numerical and categorical columns separately. First, we will define lists for each of these columns. However, one thing to note that the data imported is ALL numeric – binary columns, like donor_age_below_35, are encoded as numerical values (0 and 1). Similarly, columns like donor_ABO, with four categories, are encoded as -1,0,1, and 2. So we cannot just look for columns of numeric types or object types to define these lists.

First, calculate the number of unique values for each column – how might we use this to determine categorical variables?

2.
Save the target, survival_status, as y and the remaining columns (minus survival_time) as X.


3.
After exploring the unique value counts in each column, we will use 7 as a threshold – for columns with more than 7 unique values, we will consider this a numeric variable. For columns with 7 or less unique values, we will consider this a categorical variable. Define num_cols as a list of columns in X with more than 7 unique values and cat_cols as a list of columns in X with 7 or fewer unique values.



4.
Check to see what, if any, columns in X have missing values and print them.


5.
Split the data into a train and test set with a test size of 20%.



# Create Preprocessing Pipeline

6.
Create a categorical preprocessing pipeline called cat_vals that contains two steps – the first will fill in missing values using the mode and the second will one-hot-encode the variables. Make sure to use parameters sparse=False, drop='first', handle_unknown = 'ignore' for the OneHotEncoder.


7.
Create a numerical preprocessing pipeline called num_vals that contains two steps – the first will fill in missing values using the mean and the second will scale features using StandardScaler().


8.
Create a column transformer named preprocess that will preprocess the numerical and categorical features separately. This will contain the previous two pipelines, cat_vals and num_vals, as transformers on their respective columns, cat_cols and num_cols.


# Create Classification Pipeline and Tune
9.
Now that we have finished all the preprocessing, let’s create a classification pipeline called pipeline – it will contain three steps. The first is the preprocess created above. The second is PCA() – this will select a number of principal components from the processed data features. The third and last step will be the classifier, a logistic regression classifier.


10.
Fit pipeline on the training data and predict the accuracy score on the test data.


11.
Update the search space of hyperparameters (in the dictionary search_space) to contain the number of PCA dimensions for each classifier. Use np.linspace(30,37,3).astype(int) for the values of the dimensions.


12.
Search over the hyperparameters in search_space for the pipeline using GridSearchCV. Fit on the training set.


13.
Save the best estimator from the grid search as best_model.


Stuck? Get a hint
14.
Print attributes of best_model – the type of classifier it is, the hyperparameters of the classifier, and the number of components selected from PCA.


Stuck? Get a hint
15.
Evaluate the best estimator on the test set and print the final accuracy score. How does this compare to the initial model?
