# Requirement : Identify the key features that affects used car price. Develop a model to predict used car price using the key features. 
#               This will help the car dealer stress on these features that will  effectively meet customers' decision to chose an used car.

# ***GIT HUB REPO link***

Please use the following link to access my repository
https://github.com/chandan-banerjee/used_car_price_model/tree/main


# **Key observations/ Summary**

# **Phase EDA (Exploratory Data Analysis) & Feature Engg:**
    1. Dropped VIN & ID columns which has no relation to used car price. This reduced noise in dataset.
    2. Handled missing values appropruately using MODE  within same car and model family as appropriate
    3. Added a new column representing car-AGE. The model uses currrent date to calculate AGE. This gives DYNAMIC behavior & can be used in future years without any code change
    4. For missing odometer values uesed MODE within same car and model fsmily. If still missing value then filled in assuming average milage users drive each year(~normally ~12000 miles/yr) * AGE of the vehicle.
    5. Found data skewed in few key columns(like PRICE/ ODOMETER etc ) . Tranformed car PRICE to logarithmatic scale for better results
    6. Did PCA analysis to see main contributing features in current dataset
    7. For analysis used subset of data to reduce runtime

# **Phase Modelling**

    1. Used pipeline,column transformer & gridsearchCV to review performance and key hyper parameter values
    2.  Option 1:column selector = PCA. Used n_components=0.9 allowing model to decide the columns to generate 90% of the variance. Bcoz the PCA graph shows more feature needed to reach ~80% cut off value. 
            Best model : Ridge
            cross-validation R^2 score:  0.05499808231558767
            Mean Squared Error with PCA Feature Selection on training set:  30884010930336.04
            Mean Squared Error with PCA Feature Selection on test set:  325986526.57310754
       
        Option 2: colun selector = Polynomial degree 2
            Best model : Lasso
            Best cross-validation R^2 score for polynomial regression:  0.08375309252930645
            Mean Squared Error on training set for polynomial regression:  30883976278358.79
            Mean Squared Error on test set for polynomial regression:  318770548.042995 
        
        Option 3: column selector = Sequential feature selector, n_comonents = 5
            Best model : Ridge
            Best cross-validation R^2 score for sequential regression:  0.05014992530816287
            Mean Squared Error on training set for sequential regression:  30883944114726.297
            Mean Squared Error on test set for sequential regression:  332517267.61842513
    3.  Based on above facts Polynomial with degree 2 is best model as it gives best MSE and R^2 score is good. 

# **Phase Evaluation**

    1. Mocked up data from the original dataset that was given to me for analysis
    2. Used 3 cars data as to mimic a scenario where model never had seen the data before
    3. Used 3 models to predic prices and found polynoial feature selection using Lasso is predicting better. Details are in EVALUATION section of the notebook

# **Conclusion/NxtStep/Recommendation**

    1.  These are NOT the best models. I would say its average. The current state is much better than what I started with. The R^2 score has imporved a lot from negative to greter than ZERO.
    2. Further scope will be do more feature engineering as dataset has lot of data variation
    3. For now checked with few hyperparameter. There is scope to tune parameters for better performance , regularization and improved scores


