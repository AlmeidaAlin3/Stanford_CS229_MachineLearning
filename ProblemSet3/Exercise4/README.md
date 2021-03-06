<a href="https://i.dlpng.com/static/png/498606_preview.png"><img src="https://i.dlpng.com/static/png/498606_preview.png" title="Stanford" alt="Stanford" height="50"></a>

## Semi-supervised EM
  
**Exercise 4**  
Expectation Maximization (EM) is a classical algorithm for unsupervised learning (i.e., learning with hidden or latent variables). In this problem we will explore one of the ways in which EM algorithm can be adapted to the **semi-supervised** setting, where we have some labelled examples along with unlabelled examples.  

In the standard unsupervised setting, we have *m ∈ IN* unlabelled examples *{x^(1), ..., x^(m)}*. We wish to learn the parameters of *p(x,z;θ)* from the data, but *z^(i)*’s are not observed. The classical EM algorithm is designed for this very purpose, where we maximize the intractable
*p(x;θ)* indirectly by iteratively performing the E-step and M-step, each time maximizing a tractable lower bound of *p(x;θ)*. In the **standard unsupervised setting**, our objective can be concretely written as:

<a href="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet3/Exercise4/img/EM.png"><img src="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet3/Exercise4/img/EM.png" title="EM" alt="EM" height="125"></a>

Now, we will attempt to construct an extension of EM to the **semi-supervised** setting. Let us suppose we have an additional *m̃ ∈ IN* labelled examples *{(x^(1), z^(1)), ..., (x^(~m̃), z^(~m̃))}* where both *x* and *z* are observed. We want to simultaneously maximize the marginal likelihood of the parameters using the unlabelled examples, and full likelihood of the parameters using the labelled examples, by optimizing their weighted sum (with some hyperparameter *α*). More concretely, our semi-supervised objective *ℓsemi-sup(θ)* can be written as:

<a href="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet3/Exercise4/img/semi_sup.png"><img src="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet3/Exercise4/img/semi_sup.png" title="semi-supervised" alt="semi-supervised" height="100"></a>  

&nbsp;  
We can derive the EM steps for the semi-supervised setting using the same approach and steps as before and we end up with:  
&nbsp;  
**E-step (semi-supervised)**  
&nbsp; &nbsp; &nbsp; *For each **i** ∈ {1, ..., m}, set*

&nbsp; &nbsp; &nbsp; <a href="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet3/Exercise4/img/E_step.png"><img src="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet3/Exercise4/img/E_step.png" title="E-step semi-supervised" alt="E-step semi-supervised" height="35"></a> 


**M-step (semi-supervised)**  
&nbsp; &nbsp; &nbsp; <a href="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet3/Exercise4/img/M_step.png"><img src="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet3/Exercise4/img/M_step.png" title="M-step semi-supervised" alt="M-step semi-supervised" height="70"></a>

&nbsp;  
**4.a)**  
The [answer to the question 4.a](https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet3/Exercise4/ex4_a.md) shows that the algorithm eventually converges. In order to prove that, it is sufficient to show that our semi-supervised objective *ℓsemi-sup(θ)* monotonically increases with each iteration of E and M step, that is: 

<a href="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet3/Exercise4/img/convergence.png"><img src="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet3/Exercise4/img/convergence.png" title="convergence" alt="convergence" height="28"></a>

&nbsp;
&nbsp;  
## Semi-supervised GMM

Now we will revisit the **Gaussian Mixture Model** (GMM), to apply our semi-supervised EM algorithm. Let us consider a scenario where data is generated from **k ∈ IN Gaussian distributions**, with **unknown means μj ∈ IRd** and **covariances Σj ∈ Sd+** where **j ∈ {1, ..., k}**.  

In summary we have **m + m̃** examples, of which **m are unlabelled** data points x’s with **unobserved z**’s, and **m̃ are labelled** data points **x̃**'s with corresponding **observed labels z̃^(i)**.  

The traditional EM algorithm is designed to take only the **m** unlabelled examples as input, and learn the model parameters **μ**, **Σ**, and **φ**. Our task now will be to apply the semi-supervised EM algorithm to GMMs in order to leverage the additional **m̃ labelled examples**, and come up with **semi-supervised E-step and M-step** update rules specific to GMMs.  

&nbsp;  
&nbsp;  
**4.b)**  
In the E-step, we need to re-estimate *z^(i)* for *i = 1, ..., m*. The [answer to the question 4.b](https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet3/Exercise4/ex4_b.md) shows the **semi-supervised E-Step** expression to re-estimate all the stated latent variables.

&nbsp;  
&nbsp;  
**4.c)**  
The [answer to the question 4.c](https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet3/Exercise4/ex4_c.md) derives closed form expressions for the parameter update rules for *μ^(t+1)*, *Σ^(t+1)* and *φ^(t+1)* based on the semi-supervised objective for the **semi-supervised M-Step**.

&nbsp;  
&nbsp;  
**4.d)**  
The [code for the question 4.d](https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet3/Exercise4/ex4_d.ipynb) implements the **traditional EM algorithm** considering the **m** unlabelled examples, and run it on the unlabelled data-set until convergence. The scatter plot of three trials are shown below:

<a href="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet3/Exercise4/img/4d_plot1.png"><img src="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet3/Exercise4/img/4d_plot1.png" title="4d_plot1" alt="4d_plot1" height="200"></a>

<a href="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet3/Exercise4/img/4d_plot2.png"><img src="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet3/Exercise4/img/4d_plot2.png" title="4d_plot2" alt="4d_plot2" height="200"></a>

<a href="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet3/Exercise4/img/4d_plot3.png"><img src="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet3/Exercise4/img/4d_plot3.png" title="4d_plot3" alt="4d_plot3" height="200"></a>

&nbsp;  
&nbsp;  
**4.e)**  
The [code for the question 4.e](https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet3/Exercise4/ex4_e.ipynb) implements the **EM semi-supervised algorithm** considering both the labelled and unlabelled examples (a total of m+m̃), with 5 labelled examples per cluster, and run it until convergence. The scatter plot of three trials are shown below:


<a href="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet3/Exercise4/img/4e_plot1.png"><img src="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet3/Exercise4/img/4e_plot1.png" title="4e_plot1" alt="4e_plot1" height="200"></a>

<a href="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet3/Exercise4/img/4e_plot2.png"><img src="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet3/Exercise4/img/4e_plot2.png" title="4e_plot2" alt="4e_plot2" height="200"></a>

<a href="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet3/Exercise4/img/4e_plot3.png"><img src="https://github.com/AlmeidaAlin3/MachineLearning/blob/master/ProblemSet3/Exercise4/img/4e_plot3.png" title="4e_plot3" alt="4e_plot3" height="200"></a>

&nbsp;  
&nbsp;  
**4.e)**  
The dataset used above was sampled from a mixture of three low-variance Gaussian distributions, and a fourth, high-variance Gaussian distribution. Knowing that, lets describe the differences saw in unsupervised vs. semi-supervised EM for each of the following:  

**i. Number of iterations taken to converge**  
Unsupervised EM takes over 100 iterations to converge, while semi-supervised EM takes over 20 iterations to converge.  

**ii. Stability**    
For unsupervised EM, the clusters change for every random initialization. While for semi-supervised EM, the results are the same.  

**iii. Overall quality of assignments**    
Unsupervised EM takes two Gaussian to have high-variance, which is wrong. This is probably because high-variance will introduce more noise points. While for semi-supervised Gaussian, the results are quite accurate, with only one Gaussian that has high-variance.  

&nbsp;  

&nbsp;  
---

#### Aline Gabriel de Almeida  
<a href="https://www.linkedin.com/in/alinegalmeida/"><img src="https://cdn3.iconfinder.com/data/icons/logos-and-brands-adobe/512/201_Linkedin-512.png" title="Linkedin: alinegalmeida" alt="https://www.linkedin.com/in/alinegalmeida/" height="20"></a>
&nbsp; <a href="https://www.kaggle.com/almeidaalin3"><img src="https://cdn3.iconfinder.com/data/icons/logos-and-brands-adobe/512/189_Kaggle-512.png" title="Kaggle: almeidaalin3" alt="https://www.kaggle.com/almeidaalin3" height="20"></a>
&nbsp; <a href="mailto:aline.gabriel.almeida@gmail.com"><img src="https://cdn3.iconfinder.com/data/icons/logos-and-brands-adobe/512/147_Gmail-512.png" title="aline.gabriel.almeida@gmail.com" alt="aline.gabriel.almeida@gmail.com" height="20"></a>
&nbsp; <a href="https://github.com/AlmeidaAlin3/"><img src="https://cdn3.iconfinder.com/data/icons/logos-and-brands-adobe/512/142_Github-512.png" title="Github: AlmeidaAlin3" alt="https://github.com/AlmeidaAlin3/" height="20"></a> 

