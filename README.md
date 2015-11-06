# Bodyfat-Prediction-
stats 350

df = read.csv("bodyfat.csv")
head(df)
cor(df, use="complete.obs", method= "kendall")
fit<- lm(bodyfat~ weight + height + neck + chest + abdomen + hip + thigh + knee + ankle + biceps + forearm + wrist, data = df)
layout(matrix(c(1,2,3,4),2,2))
plot(fit)
newdata = data.frame(weight= 178.9, thigh= 59.4, height = 70.3, knee = 38.6, neck= 40, ankle = 23.1, chest = 100.8, biceps= 32.3, abdomen = 92.6, forearm = 28.7, hip= 99.9,  wrist =18.2)
predict(fit, newdata, interval = "predictions")
predict(fit, newdata, interval = "confidence")


Body Fat Predictive Model 

Introduction:
In this report we consider the measurements of over 200 men, this data is used to produce predictive equations for body fat percentage from other variables, 13 variables to be exact. We will be using R to illustrate these findings, including correlation and regression techniques. The average man in the study has the following measurements: Weight 178.9 Thigh 59.4, Height 70.3 Knee 38.6, Neck 40.0 Ankle 23.1, Chest 100.8 Biceps 32.3, Abdomen 92.6 Forearm 28.7, Hip 99.9 Wrist 18.2.  We will be testing the null hypothesis that there is no linear association between our variables. 

Correlation Matrix: 
cor(df, use="complete.obs", method= "kendall")

bodyfat    weight       height      neck     chest   abdomen
bodyfat  1.000000000 0.4357666 -0.001796723 0.3424459 0.4877159 0.6210920
weight   0.435766622 1.0000000  0.371704331 0.6180353 0.7213637 0.6934170
height  -0.001796723 0.3717043  1.000000000 0.2204238 0.1832363 0.1583904
neck     0.342445889 0.6180353  0.220423761 1.0000000 0.5940531 0.5526734
chest    0.487715936 0.7213637  0.183236341 0.5940531 1.0000000 0.7243114
abdomen  0.621092017 0.6934170  0.158390353 0.5526734 0.7243114 1.0000000
hip      0.439443470 0.7750551  0.305629735 0.5209491 0.6242539 0.6617261
thigh    0.385434397 0.6556194  0.238491479 0.4732102 0.5281123 0.5424959
knee     0.344728870 0.6522093  0.356986587 0.4675593 0.5340898 0.5357402
ankle    0.207587216 0.5167061  0.334170938 0.3718829 0.3955012 0.3562117
biceps   0.343856339 0.5940618  0.211479511 0.5100820 0.5461968 0.4903108
forearm  0.269742769 0.5743259  0.233275339 0.5537993 0.5023276 0.4282640
wrist    0.216480305 0.5237045  0.277112695 0.5454860 0.4799039 0.4250423
              hip     thigh      knee     ankle    biceps   forearm     wrist
bodyfat 0.4394435 0.3854344 0.3447289 0.2075872 0.3438563 0.2697428 0.2164803
weight  0.7750551 0.6556194 0.6522093 0.5167061 0.5940618 0.5743259 0.5237045
height  0.3056297 0.2384915 0.3569866 0.3341709 0.2114795 0.2332753 0.2771127
neck    0.5209491 0.4732102 0.4675593 0.3718829 0.5100820 0.5537993 0.5454860
chest   0.6242539 0.5281123 0.5340898 0.3955012 0.5461968 0.5023276 0.4799039
abdomen 0.6617261 0.5424959 0.5357402 0.3562117 0.4903108 0.4282640 0.4250423
hip     1.0000000 0.7068345 0.6304818 0.4556954 0.5485668 0.4975234 0.4326337
thigh   0.7068345 1.0000000 0.5841651 0.4466783 0.5528890 0.4924020 0.3548906
knee    0.6304818 0.5841651 1.0000000 0.5397463 0.4579685 0.4590970 0.4822934
ankle   0.4556954 0.4466783 0.5397463 1.0000000 0.3727606 0.4064680 0.4769363
biceps  0.5485668 0.5528890 0.4579685 0.3727606 1.0000000 0.6029285 0.4359483
forearm 0.4975234 0.4924020 0.4590970 0.4064680 0.6029285 1.0000000 0.4900083
wrist   0.4326337 0.3548906 0.4822934 0.4769363 0.4359483 0.4900083 1.0000000

The correlation matrix above displays correlations among the variables of body fat. As we can see above as well as the plots provided below, body fat and height have almost no correlation (-0.001796723). While variables such as the abdomen (0.621092017) is highly correlation with body fat. Other variables like are highly correlated with each other as well: hip & weight( 0.7750551 ) , chest & weight (0.7213637  ), and abdomen & hip (0.6617261. )

Matrix Plots:





Summary(Bodyfat): 
bodyfat          	   weight         	     height                  neck          	            chest       
Min.   : 0.00   	   Min.   :118.5      Min.   :64.00      Min.   :31.10        Min.   : 79.30  
1st Qu.:12.47    1st Qu.:159.0    1st Qu.:68.25    1st Qu.:36.40       1st Qu.: 94.35  
Median :19.20  Median :176.5  Median :70.00  Median :38.00     Median : 99.65  
Mean   :19.15    Mean   :178.9    Mean   :70.31   Mean   :37.99       Mean   :100.82  
3rd Qu.:25.30   3rd Qu.:197.0    3rd Qu.:72.25  3rd Qu.:39.42       3rd Qu.:105.38  
Max.   :47.50   	   Max.   :363.1      Max.   :77.75    Max.   :51.20         Max.   :136.20  
abdomen            hip                     thigh                   knee                    ankle     
Min.   : 69.40       Min.   : 85.0      Min.   :47.20      Min.   :33.00       Min.   :19.1  
1st Qu.: 84.58     1st Qu.: 95.5    1st Qu.:56.00    1st Qu.:36.98     1st Qu.:22.0  
Median : 90.95   Median : 99.3  Median :59.00  Median :38.50   Median :22.8  
Mean   : 92.56     Mean   : 99.9    Mean   :59.41    Mean   :38.59    Mean   :23.1  
3rd Qu.: 99.33    3rd Qu.:103.5  3rd Qu.:62.35    3rd Qu.:39.92   3rd Qu.:24.0  
Max.   :148.10     Max.   :147.7    Max.   :87.30      Max.   :49.10     Max.   :33.9  
biceps        	       forearm       	   wrist      
Min.   :24.80   	       Min.   :21.00             Min.   :15.80  
1st Qu.:30.20        1st Qu.:27.30           1st Qu.:17.60  
Median :32.05      Median :28.70         Median :18.30  
Mean   :32.27        Mean   :28.66           Mean   :18.23  
3rd Qu.:34.33       3rd Qu.:30.00           3rd Qu.:18.80  
Max.   :45.00         Max.   :34.90              Max.   :21.40

Multiple Linear Regression: 
We will be using one predictor technique called multiple linear regression. This technique allows us to model the relationship between a single independent variable, body fat, and one or more predictors (our 13 variables) as well as the plane of best fit.  By plugging values of the variables into our fitted model, it will generate the body fat, and in turn define the predicted values. There are four assumptions associated with our model: linearity, equal variance, observations are independent, and normal distribution. 

Model Formula(full bodyfat data set):
Call:
lm(formula = bodyfat ~ weight + height + neck + chest + abdomen + 
    hip + thigh + knee + ankle + biceps + forearm + wrist, data = df)

Residuals:
     Min       1Q   Median       3Q      Max 
-10.4361  -3.0780  -0.0699   3.2771   9.7268 

Comprehensive Results:
Coefficients:
             Estimate Std. Error t value Pr(>|t|)    
(Intercept) -22.80469   22.31417  -1.022   0.3078    
weight       -0.11910    0.06119  -1.947   0.0528 .  
height       -0.07222    0.17927  -0.403   0.6874    
neck         -0.43698    0.23627  -1.850   0.0656 .  
chest        -0.01016    0.10381  -0.098   0.9221    
abdomen       1.03194    0.08211  12.567   <2e-16 ***
hip          -0.20725    0.14540  -1.425   0.1554    
thigh         0.14378    0.13742   1.046   0.2965    
knee          0.13991    0.24117   0.580   0.5624    
ankle         0.13111    0.22279   0.588   0.5568    
biceps        0.20611    0.17317   1.190   0.2352    
forearm       0.39164    0.19796   1.978   0.0490 *  
wrist        -1.29922    0.50604  -2.567   0.0109 *  
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 4.337 on 239 degrees of freedom
Multiple R-squared:  0.7443,	Adjusted R-squared:  0.7315 
F-statistic: 57.98 on 12 and 239 DF,  p-value: < 2.2e-16

The output of the model provides a brief summary stating the f-value is 57.98, and the p-value is < 2.2e-16 proving to be a tiny p-value. Therefore when testing the null hypothesis that there is no linear relationship, we reject the null concluding that our model somewhat works. Likewise, the two versions of r-squared tell us how much of the variability is explained by the model, in this case the model explains about 73% of the variation of percent body fat. 

Diagnostic Plots:
 
 
The plots shown above examine the fit illustrating the residuals. The residuals versus fitted values plot is used to test our model assumptions of linearity and equal variance, the model does not fit our model assumptions as we see very large values (outliers: 207, 224, 225) and the spread is not noticeably evenly spread around 0. The scale-location plot is used to check our assumption of equal variances; in this instance we do not see a particular visible pattern.  The normal QQ plot allows us to assume that normality holds here as we see a linear relationship within the plot.  Residuals vs Leverage refers to Cook’s distance, measures how much a single variable can influence the coefficients and the model when those variables are omitted. In this plot we see observation 86 has a larger Cook’s distance than other data points in the plot, this might be worth taking a look at.

Adjusted Model:
Call:
lm(formula = bodyfat ~ weight + neck + abdomen + forearm, data = df)

Residuals:
     Min       1Q   Median       3Q      Max 
-10.2942  -3.2441  -0.0301   3.1907  10.8169 
Coefficients:
             Estimate Std. Error t value Pr(>|t|)    
(Intercept) -42.07422    6.41680  -6.557 3.19e-10 ***
weight       -0.13955    0.02539  -5.497 9.63e-08 ***
neck         -0.56334    0.21119  -2.668  0.00815 ** 
abdomen       1.02202    0.05678  17.999  < 2e-16 ***
forearm       0.45359    0.18412   2.464  0.01444 *  
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
Residual standard error: 4.381 on 247 degrees of freedom
Multiple R-squared:  0.7304,	Adjusted R-squared:  0.726 
F-statistic: 167.3 on 4 and 247 DF,  p-value: < 2.2e-16

Predictions 
fit      lwr      upr
1 18.38195 17.29563 19.46827

Analysis of Variance Table (> anova(fit1,fit2))
Model 1: bodyfat ~ weight + height + neck + chest + abdomen + hip + thigh + 
    knee + ankle + biceps + forearm + wrist
Model 2: bodyfat ~ weight + neck + abdomen + forearm
  Res.Df    RSS Df Sum of Sq      F Pr(>F)
1    239 4494.8                           
2    247 4739.8 -8   -245.06 1.6288 0.1173

We can see that when we use our adjusted model with variables, weight, neck, abdomen, and forearm, we can say with 95% certainty that the body fat of the average man should be between 18 and 19%.  As we can see with our diagnostic plots below, this allows our model to better fit our assumptions. Linearity, equal variances, and normal distribution are evenly seen throughout the first three plots, while Cook’s Distance plot seems to have no disturbing distributions. 
 


Conclusion: 
Although many variables need to be taken into account when trying to predict body fat percent, we used a multiple linear regression model to find a model for the relationship between body fat percentage and weight, abdomen, neck and forearm  (The first model was showing the linear relationship between body fat and all 13 variables). This model was chosen, when comparing all of the variables at first and slowly omitting some variables, so that the coefficients would change.  In fact they did, and so each coefficient’s p-values: <1, resulting in rejection of the null hypothesis that there is no linear association between the variables. The output of our model shows a significant linear relationship between the five variables as the p-value: < 2.2e-16 and the f-value is 167.3, further proving our model works. In this case, our model explains 73% of the variation of percent body fat. Each variable is a constant multiple predictor, weight, neck, abdomen, and forearm, therefore we can further conclude with 73% certainty that the body fat of the average man should be between 18% and 19%. 



