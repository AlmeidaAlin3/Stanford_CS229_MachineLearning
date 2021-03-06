
<a href="https://i.dlpng.com/static/png/498606_preview.png"><img src="https://i.dlpng.com/static/png/498606_preview.png" title="Stanford" alt="Stanford" height="50"></a>

## Model Calibration
  
**Exercise 3**  
In Bayesian statistics, almost every quantity is a random variable, which can either be observed, or unobserved. For instance, parameters *θ* are generally unobserved random variables, and data *x* and *y* are observed random variables. The joint distribution of all the random variables is also called the **model**, for example *p(x, y, θ)*.  

Every unknown quantity can be estimated by conditioning the model on all the observed quantities. Such a conditional distribution over
the unobserved random variables, conditioned on the observed random variables, is called the **posterior distribution**. For instance *p(θ|x, y)* is the posterior distribution in the machine learning context. 

A consequence of this approach is that, we are required to endow our model parameters, i.e. *p(θ)*, with a prior distribution. The prior probabilities are to be assigned *before* we see the data – they need to capture our prior beliefs of what the model parameters might be before
observing any evidence, and must be a subjective opinion by the person building the model.  

In the purest Bayesian interpretation, we are required to keep the entire posterior distribution over the parameters all the way until prediction, to come up with the posterior predictive distribution, and the final prediction will be the expected value of the posterior predictive distribution.  

However in most situations, this is computationally very expensive, and we settle for a compromise that is less pure (in the Bayesian sense).
The compromise is to estimate a point value of the parameters (instead of the full distribution) which is the mode of the posterior distribution.  

Estimating the mode of the posterior distribution is also called **maximum a posteriori estimation** (MAP). That is:

<a href="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet2/Exercise3/img/MAP.png"><img src="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet2/Exercise3/img/MAP.png" title="MAP" alt="MAP" height="32"></a> 

Compare this to the **maximum likelihood estimation** (MLE) we have seen previously:

<a href="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet2/Exercise3/img/MLE.png"><img src="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet2/Exercise3/img/MLE.png" title="MLE" alt="MLE" height="32"></a> 

In this exercise, we explore the connection between MAP estimation, and common regularization techniques that are applied with MLE estimation. In particular, it will shown how the choice of prior distribution over *θ* (e.g Gaussian, or Laplace prior) is equivalent to different kinds of
regularization (e.g *L2* or *L1* regularization). 

&nbsp;  
**3.a)**  
The [answer to the question 3.a](https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet2/Exercise3/ex3_a.md) shows that, if we assume that **p(θ) = p(θ|x)**, then *θMAP* is:

<a href="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet2/Exercise3/img/MAP_marg_indep.png"><img src="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet2/Exercise3/img/MAP_marg_indep.png" title="MAP for theta and x marginally independent" alt="MAP for theta and x marginally independent" height="24"></a> 

The assumption that *p(θ) = p(θ|x)* will be valid for models such as linear regression where the input *x* are not explicit modeled by *θ*. Note that this means *x* and *θ* are **marginally independent**, but not conditionally independent when *y* is given.  

&nbsp;  
**3.b)**  
Recall that *L2* regularization penalizes the *L2* norm of the parameters while minimizing the loss i.e., negative log likelihood in case of probabilistic models. 

The [answer to the question 3.b](https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet2/Exercise3/ex3_b.md) shows that MAP estimation with a zero-mean Gaussian prior over *θ*, specifically **θ ∼ Normal(0, η².I)**, is equivalent to applying *L2* regularization with MLE estimation. That is:

<a href="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet2/Exercise3/img/MAP_reg1.png"><img src="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet2/Exercise3/img/MAP_reg1.png" title="MAP L2" alt="MAP L2" height="35"></a>  

where **λ = 1/(2η²)**:

<a href="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet2/Exercise3/img/MAP_reg2.png"><img src="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet2/Exercise3/img/MAP_reg2.png" title="MAP L2" alt="MAP L2" height="45"></a> 

&nbsp;  
**3.c)**  
Now consider a specific instance, a linear regression model given by **y=(θ.T).x + err**, where **err ~ Normal(0, σ²)**. Like before, assume a Gaussian prior on this model such that *θ ∼ Normal(0, η².I)*.  
The [answer to the question 3.c](https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet2/Exercise3/ex3_c.md) came up with the closed form expression for *θMAP*:

<a href="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet2/Exercise3/img/MAP_closed_form.png"><img src="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet2/Exercise3/img/MAP_closed_form.png" title="MAP closed form" alt="MAP closed form" height="55"></a> 

&nbsp;  
**3.d)**  
Next consider the Laplace distribution, whose density is given by:

<a href="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet2/Exercise3/img/Laplace_density.png"><img src="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet2/Exercise3/img/Laplace_density.png" title="Laplace_density" alt="Laplace_density" height="55"></a>  

and a linear regression model given by **y=(θ.T).x + err**, where **err ~ Normal(0, σ²)**. Assume a Laplace prior on this model where **θ ∼ Laplace(0, b.I)**.
The [answer to the question 3.d](https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet2/Exercise3/ex3_d.md) shows that *θMAP* in this case is equivalent to the solution of linear regression with *L1* regularization:

<a href="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet2/Exercise3/img/MAP_L1.png"><img src="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet2/Exercise3/img/MAP_L1.png" title="MAP L1" alt="MAP L1" height="48"></a>  

where **λ = 1/b** and whose loss is specified as:


<a href="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet2/Exercise3/img/MAP_L1_loss.png"><img src="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet2/Exercise3/img/MAP_L1_loss.png" title="MAP L1 loss" alt="MAP L1 loss" height="30"></a>  
 
Note: A closed form solution for linear regression problem with *L1* regularization does not exist. To optimize this, we use gradient descent with a random initialization and solve it numerically.

&nbsp;  
*Remark:*  

*Linear regression with **L2** regularization is also commonly called **Ridge regression**, and when **L1** regularization is employed, is commonly called **Lasso regression**. These regularizations can be applied to any Generalized Linear models just as above (by replacing *log p(y | x, θ)* with
the appropriate family likelihood).*  

*Regularization techniques of the above type are also called **weight decay**, and **shrinkage**. The Gaussian and Laplace priors encourage the parameter values to be closer to their mean (i.e., zero), which results in the shrinkage effect.*  
  
***Lasso regression** is known to result in sparse parameters, where most of the parameter values are zero, with only some of them non-zero.*



&nbsp;  
---

#### Aline Gabriel de Almeida  
<a href="https://www.linkedin.com/in/alinegalmeida/"><img src="https://cdn3.iconfinder.com/data/icons/logos-and-brands-adobe/512/201_Linkedin-512.png" title="Linkedin: alinegalmeida" alt="https://www.linkedin.com/in/alinegalmeida/" height="20"></a>
&nbsp; <a href="https://www.kaggle.com/almeidaalin3"><img src="https://cdn3.iconfinder.com/data/icons/logos-and-brands-adobe/512/189_Kaggle-512.png" title="Kaggle: almeidaalin3" alt="https://www.kaggle.com/almeidaalin3" height="20"></a>
&nbsp; <a href="mailto:aline.gabriel.almeida@gmail.com"><img src="https://cdn3.iconfinder.com/data/icons/logos-and-brands-adobe/512/147_Gmail-512.png" title="aline.gabriel.almeida@gmail.com" alt="aline.gabriel.almeida@gmail.com" height="20"></a>
&nbsp; <a href="https://github.com/AlmeidaAlin3/"><img src="https://cdn3.iconfinder.com/data/icons/logos-and-brands-adobe/512/142_Github-512.png" title="Github: AlmeidaAlin3" alt="https://github.com/AlmeidaAlin3/" height="20"></a> 
