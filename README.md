# GA Project 2 - Ames Housing Data and Kaggle Challenge
## Jetnipat Sarawongsuth 
Please Note: The project consists of 2 Jupyter Notebook files. 
- Project 2 - Ames Housing Data and Kaggle Challenge (MAIN FILE)
- Project 2 - Appendix (ADDITIONAL MODELS)
### Problem Statement

This project comprises of the exploration of the exploration of the Housing Prices and the different features of the houses sold in Ames, Iowa. This will explore some important features that affect the sale price of the houses. Additionally, we will also be creating several machine learning models that can be used to predict the sale prices of the houses in Ames, Iowa based on the different features of the house. The models that we are comparing will include OLS Regression (no penalties) and Elastic Net (L1/L2 Penalty) to see how they affect the predictions we get.

The study and the models created from this model could potentially be used by real estate/property development firms that would like some insights into how to make the property more valuable. For example, which features of a house has the biggest impact on the sale price or which feature has negative impact on house prices. The regression model generated from the project could additionally be used to provide some guideline into how to price new properties accordingly to maximise the chance of being sold.

### Datasets

The project contains 2 usable datasets:

- train.csv - 2051 rows, 81 columns
- test.csv - 879 rows, 80 columns

The datasets contain categorical and numerical features for houses that were sold in Ames, Iowa between 2006 and 2010.

The data dictionary can be found [here](http://jse.amstat.org/v19n3/decock/DataDocumentation.txt).



### Evaluation

|         | Training R2 | Cross Val R2 | Training RMSE | Cross Val RMSE | Kaggle Private RMSE |
|---------|-------------|--------------|---------------|----------------|---------------------|
| Model 1 | 0.922       | 0.893        | 22180         | 25738          | 27713               |
| Model 2 | 0.951       | -2.214       | 17428         |$5×10^{15}$     |N/A                  |
| Model 3 | 0.939       | 0.902        | 19514         | 24505          | 27505               |
| Model 4 | 0.930       | 0.905        | 20921         | 24251          | 25412               |

Overall, out of the four models constructed, the best model is Model 4. This model uses elastic net with optimal l1 being 1 (and therefore, is Lasso). The model is similar to the other three models in how the features were transformed. The missing values have been treated the same way (mean/mode). They were given Polynomial Features (degree of 3) based on features that had strong correlation to the target feature. They were scaled using Standard Scaler. The one difference is that the encoding proces. Unlike the features in other models that were encoded using just OneHotEncoder, the features that went into Model 4 had been encoded using Target Encoder for ordinal columns and OneHotEncoder for the remaining categorical columns. This resulted in a model that balances between bias and variance. It may not have the lowest training rmse but it does much better at unseen data as shown by the cross val rmse and Kaggle private RMSE.

#### Metrics
Model 4's R2 value for both the training dataset and cross validation are not too far off of each other (3%). The cross validation r2 shows that it is much better at predicting the sale price compared to the base model of just predicting the mean sale price. When we look at the RMSE scores which indicates the average residual/error for the predictions, it can be seen that in the Model 2, which uses OLR Regression, performed the best in the training set but severely struggled on unseen data. It performed worse than the baseline model.

Evidently, despite the fact that it scored worse on training data RMSE than Model 2 and 3, it performed the best on unseen data, both from cross valudation and on Kaggle. The reduction in performance for the training and cross val/Kaggle does indicate an overfit - high variance. It is acceptable (from ~21000 for training to ~25000 cross val/Kaggle). The bias is also the lowest amongst the models on unseen data.


### Conclusion

In conclusion, we have learnt is that the distribution of the prices overall are right skewed. The finding shows that half of all of the sale prices in the dataset lie between around 130000 and 214000. The mean price is 181469 USD with the sale price ranging from 12789 USD up to 611657 USD. We have seen that Floating Villages Residentials (FV) have the highest starting Sale Price when compared to other Zoning categories at 144152 USD. The Zoning Type that has the highest Sale Price on average is also FV at 218618 USD. Interestingly, the Zoning Type that has the largest maximum sale price does not belong to FV but rather RL (Residential Low Density) at 611657. The cheapest Zoning type on average is A (Agriculture) at 47300. We have also identified that residential properties (RH, RL, RM) tend to have higher sale price on average when compared to the other categories except for FV.

The study has also identified the of the interesting features that real estate/development firms should be focusing on in order to increase the values of the houses. Our best model (Model 4), has given us the insight of the importance of the size of the living area when it comes to house pricing. In fact, an incrase of 1 square feet of the living area (above ground) would increase the sale price by 19505 USD. Other factors include the overall quality of the house (Overall Qual) and the quality of the kitchen. Some of the features that were shown to have moderate negative correaltion with the sale price are Year Built and Year Remod/Add, -0.57 and -0.55 respectively. Model 4 also provide us with some insights confirming this. An increase one year to the age of the house results in a reduction of 6871 USD from the sale price, while an increase of one year since last house remodel/addition decreases the price by 1702 USD. This means that to incrase the value of the house before sale, it should either be relatively newly built or it should be modified/remodelled recently.

Finally, real estate firms should be able to use Model 4 to give a rough guideline on the sale prices for new properties entering the market. Since the Model has around 24000 RMSE, it means the errors in the prediction could be +/- 24000 on average. The model could additionally be used on existing properties in the market to give insights into why some properties remain unsold. This could be because the sale price is too high (very far from Model 4's prediction level) or it could be needing some refits, for instance. 










