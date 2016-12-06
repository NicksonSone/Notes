# Statistical Machine Learning

terms:
input variables, predictors, independent variables, features, variables  
ouput variables, response, dependent variable

# Intro to Machine Learning
## Accuracy on Model Errors
measure in two types of error
* Reducible error: error which can be reduce by choosing a more appropriate statistical learning method  
* Irreducible error:  a better estimator cannot help, because of some unaccounted infomation

e.g. We want to estimate a unknown function, F. Given input variables, X and an estimate, f.  
![equation](http://www.sciweavers.org/upload/Tex2Img_1480674218/render.png)  
![equation](http://www.sciweavers.org/upload/Tex2Img_1480674354/render.png)  
The distance between F(X) and f(X) is reducible by coming up a better estimate, f. However, difference between Y and y also contains ![](http://www.sciweavers.org/upload/Tex2Img_1480674530/render.png)


![](http://www.sciweavers.org/upload/Tex2Img_1480674860/render.png)
The first part, reducible error, distance between F(X) and f(X). The second part, irreducible.

## Contrast between linear and non-linear model
* Linear: better interpretability and easier for inference, less flexible
* Non-linear: more accurate but less interpretable, and not good for inference, more flexible

## Parametric vs Non-parametric methods
* Parametric:
  1. Make assumption on functional form, or shape.
     Like assume F to be a linear model: ![](http://www.sciweavers.org/upload/Tex2Img_1480991776/render.png)
  2. fit the model on training data, to optimize parameters
* Non-parametric:
  Make no explicit assumption about functional form. They instead try estimate F that get as close to data points as possible.

**Pros and Cons**
* Parametric:
estimated F might be hugely different from true F, but it requires less data to model than * non-parametric methods.
* Non-parametric:
very close to true F, but need a lot more data.

## Flexibility vs Interpretability
More flexible model can be more accurate but also tend to overfit and less interpretable.
![FlexVsIntre][FlexVsIntre]

Lasso: relies on linear model, but use different fitting procedure, more restrictive in estimating coefficients. Some coefficients will be zero.
GAM: extend linear model to allow for non-linear relationships.
Bagging, Boosting, SVM with non-linear kernels: least interpretable.

## Supervised, Unsupervised, Semi-supervised
* Unsupervised: seek relationships between variables or relationships between observations
* Semi-supervised: a total of n observations, with only m of them having response. To utilize this whole set to train a model.

## Estimation on Accuracy
Mean square error for regression  
![MSE][MSE]

Error rate for classification  
![ErrorRate][ErrorRate]

**Example**
* Bayes   
  The error rate is minimized when we assign with the most probable class. It is the case with bayes classifier.  
  Bayes probability:  
  ![BayesPro][BayesPro]  
  Error rate: the expectation averages the probability over all possible values of X.  
  ![BayesError][BayesError]  

* KNN
  Because unknown conditional distribution of Y given X, direct Bayes classifier is impossible. KNN is one of approaches to intimate Bayes classifier.

  1. Given positive integer K and test observation x.
  2. Find K data points closest to x, as N.
  3. Compute pro of each class j from N.  
  ![KNNpro][KNNpro]
  4. Assign the class with largest pro.

  <br/>
  Effect of K: K control variance(bias), flexibility. More bias with larger K.
  ![KNN_K10]  
  ![KNN_Ks]

# Linear Regression






<!--- Images of math symbols --->

<!--- Images of equations --->
[MSE]:MSE.png
[ErrorRate]:ErrorRate.png
[VarBias]:VarBias.png
[BayesPro]:BayesPro.png
[BayesError]: BayesError.png
[KNNpro]:KNNpro.png
[KNN_K10]:KNN_K10.png
[KNN_Ks]:KNN_Ks.png

<!--- Images of graphs --->
[FlexVsIntre]:flexiblilityVsInterpre.png








View extension
